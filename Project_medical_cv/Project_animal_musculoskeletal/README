# X-Ray 이미지를 활용한 반려동물 근골격계 질환 분류

이 프로젝트는 X-Ray 이미지를 활용하여 반려동물의 4가지 근골격계 질환을 분류하는 머신러닝 모델을 개발하는 데 초점을 맞추고 있습니다. 대상 질환은 다음과 같습니다:

- **갈비뼈골절 (Class 0)**
- **슬개골탈구 (Class 1)**
- **전십자인대파열 (Class 2)**
- **추간판질환 (Class 3)**

## 프로젝트 동기

2024년 현재 의료 영상 분석 분야에서 널리 사용되고 있는 최신 모델들을 평가하고, 
특정 분류 작업에서 가장 적합한 모델을 찾고, 이를 통해 각 모델의 장단점을 파악하는 것을 목표로 했습니다.

---

## 진행 과정

### 1. 모델 선정
다음과 같은 3가지 전이학습 모델을 선정하여 사용했습니다:
- **EfficientNetB0**: 가볍고 효율적인 CNN 기반 분류 모델.
- **CheXNet**: 흉부 X-Ray 이미지 분석을 위해 설계된 DenseNet 기반의 모델로, 본 프로젝트에 맞게 수정하여 사용.
- **ViT (Vision Transformer)**: 이미지 분류에 강점이 있는 Transformer 기반 아키텍처.

### 2. 데이터 전처리
- 모든 X-Ray 이미지는 Gaussian 스무딩을 적용하고 224x224 크기로 리사이즈했습니다.
- 이미지 정규화를 수행하여 일관성을 확보했습니다.
- 학습(train), 검증(val), 테스트(test) 데이터셋을 별도로 구성했습니다.

### 3. 학습 및 평가
- 각 모델을 전처리된 데이터를 활용하여 학습했습니다.
- 학습 중 검증 정확도(accuracy), 정밀도(precision), 재현율(recall), F1 점수를 기록했습니다.
- 테스트 데이터를 활용하여 최종 평가를 진행했습니다.
- 혼동 행렬(confusion matrix), ROC-AUC 곡선, Precision-Recall 곡선 등 다양한 평가 지표를 분석했습니다.

---

## 결과

### Model Comparisons
| Model           | Accuracy | Precision | Recall | F1 Score | Inference Time (seconds) |
|------------------|----------|-----------|--------|----------|--------------------------|
| EfficientNetB0  | 30.21%   | 43.31%    | 30.21% | 25.97%   | 2.72                     |
| CheXNet         | 99.54%   | 99.55%    | 99.54% | 99.54%   | 2.88                     |
| ViT             | 94.63%   | 96.29%    | 94.63% | 95.02%   | 7.66                     |

### 결과 분석
- **CheXNet** 가장 높은 정확도와 평가 지표를 기록하며, 이번 작업에서 가장 효과적인 모델로 나타났습니다.
- **ViT** CheXNet에 근접한 성능을 보였으나, 추론 시간이 상대적으로 길어 실시간 애플리케이션에서는 제한적일 수 있습니다.
- **EfficientNetB0** 가벼운 구조에도 불구하고, 이 특정 작업에서는 일반화 성능이 낮았습니다.

---


## 한계점과 개선 방향

### 한계점
1. **Class Imbalance**: 특정 클래스(예: Class 3)가 상대적으로 적은 데이터를 포함하고 있어 학습에 편향이 발생할 가능성이 큽니다.
2. **Overfitting**: CheXNet은 테스트 데이터에서 매우 높은 성능을 보였으나, 이는 데이터셋에 과적합되었을 가능성을 시사합니다.
3. **Data Dependency**: 전처리 및 증강 방법이 현실적인 상황을 충분히 반영하지 못했습니다.

### 개선 방향
1. **Dataset Expansion**: Include a larger dataset with more balanced class distribution.
2. **Augmentation Techniques**: Use advanced augmentation methods, such as MixUp or CutMix, to enhance model robustness.
3. **Exploration of Lightweight Models**: Investigate lightweight transformer models to balance performance and inference time.

---

## 결론

본 프로젝트에서는 CheXNet이 가장 우수한 성능을 보여주었으며, 테스트 정확도와 평가 지표에서 높은 점수를 기록했습니다. 
그러나, 클래스 불균형과 데이터 다양성 부족 등 한계점을 개선한다면 더욱 발전된 결과를 얻을 수 있을 것입니다. 
이번 프로젝트로 전이학습 기반 모델을 이용하 의료 영상 분석에 적용하는 방법을 연구했다.
---
