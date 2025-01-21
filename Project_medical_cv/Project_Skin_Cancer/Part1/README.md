# Part 1: 피부암 분류 (Classification)

## **개요**
Part 1에서는 HAM10000 데이터셋의 5,000개 이미지를 활용하여 피부암 분류 모델을 학습하고 평가합니다. 이 작업에서는 두 가지 대표적인 딥러닝 모델인 **EfficientNet-b0**와 **Vision Transformer (ViT)**를 사용하여 각각의 성능을 비교하고, 데이터 증강이 분류 성능에 미치는 영향을 분석합니다.

---

## **작업 흐름**

### **1. 데이터 전처리 및 증강**
HAM10000 데이터셋의 이미지는 다음과 같은 과정을 거쳐 전처리 및 증강됩니다:
- 모든 이미지는 **224x224** 크기로 리사이즈.
- **훈련 데이터 증강 기법**:
  - **수평 뒤집기** (50% 확률)
  - **수직 뒤집기** (20% 확률)
  - **회전** (최대 ±20도, 50% 확률)
  - **색상 조정** (밝기, 대비, 채도: 20% 범위)
  - **탄성 변환** (30% 확률)
- **검증 및 테스트 데이터 전처리**:
  - 크기 리사이즈 및 정규화만 수행.

### 증강 기법
```python
def get_data_transforms():
    train_transform = Compose([
        Resize(224, 224),
        HorizontalFlip(p=0.5),
        VerticalFlip(p=0.2),
        Rotate(limit=20, p=0.5),
        ColorJitter(brightness=0.2, contrast=0.2, saturation=0.2, p=0.5),
        ElasticTransform(p=0.3),
        Normalize(mean=(0.485, 0.456, 0.406), std=(0.229, 0.224, 0.225)),
        ToTensorV2()
    ])
    val_test_transform = Compose([
        Resize(224, 224),
        Normalize(mean=(0.485, 0.456, 0.406), std=(0.229, 0.224, 0.225)),
        ToTensorV2()
    ])
    return train_transform, val_test_transform
```
### 클래스 매핑
```python
class_map = {
    "bkl": 0,  # 양성 각화증
    "nv": 1,   # 모반
    "df": 2,   # 피부섬유종
    "mel": 3,  # 흑색종
    "vasc": 4, # 혈관병변
    "bcc": 5,  # 기저세포암
    "akiec": 6 # 광선각화증 및 상피내암
}
```

## **2. 모델 및 결과**

### EfficientNet-b0 결과
| Class    | Precision | Recall | F1 Score | Support |
|----------|-----------|--------|----------|---------|
| bkl      | 54.00%    | 62.00% | 58.00%   | 113     |
| nv       | 90.00%    | 92.00% | 91.00%   | 687     |
| df       | 21.00%    | 36.00% | 27.00%   | 11      |
| mel      | 64.00%    | 32.00% | 43.00%   | 87      |
| vasc     | 50.00%    | 77.00% | 61.00%   | 13      |
| bcc      | 64.00%    | 81.00% | 72.00%   | 53      |
| akiec    | 63.00%    | 33.00% | 44.00%   | 36      |

| Metric          | Value |
|------------------|-------|
| Test Accuracy    | 80.10% |
| Weighted F1 Score| 79.00% |

---

### ViT 결과
| Class    | Precision | Recall | F1 Score | Support |
|----------|-----------|--------|----------|---------|
| bkl      | 40.00%    | 49.00% | 44.00%   | 113     |
| nv       | 82.00%    | 93.00% | 87.00%   | 687     |
| df       | 0.00%     | 0.00%  | 0.00%    | 11      |
| mel      | 50.00%    | 17.00% | 26.00%   | 87      |
| vasc     | 100.00%   | 15.00% | 27.00%   | 13      |
| bcc      | 43.00%    | 19.00% | 26.00%   | 53      |
| akiec    | 19.00%    | 14.00% | 16.00%   | 36      |

| Metric          | Value |
|------------------|-------|
| Test Accuracy    | 72.60% |
| Weighted F1 Score| 69.00% |




