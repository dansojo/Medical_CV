
# MRI 의료 영상 분석

## 1. 기본 개념
- **원리**: MRI(Magnetic Resonance Imaging)는 강한 자기장을 사용하여 인체 내 수소 원자핵의 반응을 측정합니다. 인체 내 수분 함량에 따라 다른 신호를 발생시키며, 이를 통해 **연부 조직을 정밀하게 시각화**할 수 있습니다.
- **다양한 모드**: MRI는 T1, T2, FLAIR 등 여러 모드로 촬영할 수 있으며, 각 모드는 특정 조직이나 병변을 강조하는 데 유리합니다.
- **장점**: 방사선 노출이 없고, 연부 조직과 신경계 구조를 매우 선명하게 표현할 수 있습니다.
- **단점**: 촬영 시간이 길고, 금속을 포함한 인체 부위에서는 촬영이 어려우며, 노이즈가 발생하기 쉽습니다.

## 2. 특성
- **고대비 연부 조직 표현**: MRI는 뇌, 근육, 신경 등 연부 조직을 선명하게 표현하며, 각 모드(T1, T2 등)에 따라 다른 세부 사항을 강조합니다.
- **노이즈와 왜곡**: 자기장 불균형이나 움직임으로 인해 노이즈와 왜곡이 발생할 수 있습니다.
- **다양한 해상도와 깊이**: 다양한 스캔 방식에 따라 해상도와 깊이가 다르게 표현됩니다.
- **3D 데이터 활용**: MRI는 단일 슬라이스뿐 아니라 다중 슬라이스를 활용하여 **3D 구조를 재구성**할 수 있습니다.

## 3. 해당 이미지에 적합한 전처리 방법
- **강도 조정 및 정규화**:
  - MRI 이미지는 서로 다른 스캐너나 촬영 조건에 따라 밝기와 강도가 다르기 때문에, **정규화를 통해 이미지 밝기를 조정**하여 일관성을 확보합니다.
  - 정규화 외에도 **Bias Field Correction**을 통해 강도 불균형을 보정할 수 있습니다.
- **노이즈 제거**:
  - Gaussian 및 Median 필터 외에도, MRI 특유의 노이즈를 줄이기 위해 **Non-Local Means Denoising**과 같은 고급 필터가 사용됩니다.
- **세그멘테이션 (Segmentation)**:
  - 뇌와 같은 주요 조직의 구조를 분리하기 위해 **U-Net**과 같은 세그멘테이션 모델이 자주 사용됩니다.
  - FLAIR 이미지를 활용한 병변 분할이나 뇌종양 탐지에서 특히 유용합니다.

## 4. 주요 응용 분야 및 활용 예시
- **뇌 질환 진단**: MRI는 뇌종양, 뇌출혈, 다발성 경화증(MS) 등을 진단하고 추적 관찰하는 데 유용합니다.
- **근육 및 신경계 진단**: 근육 질환이나 신경계 손상을 평가하는 데 사용되며, 척추 및 관절 상태를 확인하는 데도 자주 활용됩니다.
- **심장 MRI**: 심장과 혈관 상태를 평가하고, 심근경색이나 관상동맥 질환을 진단할 수 있습니다.

## 5. 데이터셋 예시와 주요 특징
- **BraTS**: 뇌종양 세그멘테이션을 위한 데이터셋으로, 다중 MRI 모드를 포함해 뇌종양의 위치와 크기를 라벨링합니다.
- **IXI**: 뇌 MRI 데이터셋으로 다양한 스캐너에서 촬영된 데이터를 포함하고 있어 일반화 연구에 유용합니다.
- **OASIS**: 알츠하이머 환자와 정상인의 뇌 MRI를 포함한 데이터셋으로, 치매 연구와 분류 모델 학습에 자주 사용됩니다.

## 6. 전처리 시 고려할 잠재적 문제점 및 해결 방법
- **강도 불균형 문제**:
  - 해결 방법: Bias Field Correction을 적용하여, MRI 이미지에서 강도가 불균형하게 나타나는 부분을 보정합니다.
- **노이즈와 왜곡 문제**:
  - 해결 방법: Non-Local Means Denoising 및 Gaussian 필터로 노이즈를 줄이며, 필요에 따라 움직임 보정(Motion Correction)을 수행합니다.
- **해상도 차이 문제**:
  - 해결 방법: 해상도가 다른 MRI 데이터를 일관된 해상도로 리샘플링하여 모델 학습 시 일관성을 유지합니다.

## 7. 딥러닝 모델의 추천 아키텍처 및 적용 방법
- **U-Net, 3D U-Net**: 2D 및 3D 세그멘테이션 모델로, 뇌 구조 분할, 병변 탐지 등에서 널리 사용됩니다.
- **ResNet, DenseNet**: 뇌 질환 분류나 병변 유무 판단을 위한 분류 모델로 적합합니다.
- **모델 적용 방법**:
  - 다중 모드 MRI(T1, T2 등)를 입력으로 사용하여 다양한 조직을 강조하며, 모델에 더 많은 정보를 제공합니다.
  - FLAIR 이미지는 특히 병변 탐지에 유리하므로, FLAIR를 추가 입력으로 사용하여 모델 성능을 높일 수 있습니다.

## 8. 최신 연구 동향 요약
- **Transformer 기반 모델**: MRI 이미지의 전체 구조적 패턴을 학습해 병변을 탐지하고 분할하는 데 효과적입니다.
- **Self-supervised Learning**: 레이블이 적거나 없는 데이터에서 유용한 특징을 학습해 전이 학습을 통해 성능을 높입니다.
- **3D Segmentation**: 2D보다 3D 데이터로 접근하여 뇌와 장기의 세부 구조를 더 정확히 분할하는 연구가 진행 중입니다.
- **GAN을 활용한 해상도 개선**: GAN을 통해 해상도를 높이고, 데이터 증강을 통해 모델 성능을 높입니다.
