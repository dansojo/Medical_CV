
# CT 의료 영상 분석

## 1. 기본 개념
- **원리**: CT(Computed Tomography) 이미지는 X-ray를 다양한 각도에서 투과하여 2D 슬라이스 이미지로 재구성됩니다. 각 슬라이스를 결합하면 **3D 구조를 확인**할 수 있어, 해부학적 위치와 병변의 크기, 밀도 등을 세밀하게 평가할 수 있습니다.
- **장점**: 고해상도 이미지로, 뼈와 연부 조직 등 밀도가 다른 구조를 명확히 구분할 수 있으며, 종양의 위치와 크기, 내부 장기 상태를 정확히 확인할 수 있습니다.
- **단점**: 방사선 노출이 있어 방사선량을 신중하게 조절해야 하며, 촬영 장비가 고가이기 때문에 사용 시 비용이 발생할 수 있습니다.

## 2. 특성
- **밀도 기반 명암 표현**: CT 이미지는 **Hounsfield Unit(HU)**으로 측정되며, 각 픽셀의 값이 조직의 밀도를 나타냅니다. 예를 들어, 공기는 -1000 HU, 물은 0 HU, 뼈는 1000 HU 이상으로 표시됩니다.
- **고해상도와 3D 정보**: 2D 슬라이스를 쌓아올려 3D 이미지를 만들 수 있어, 종양 크기나 위치 등 구조적 정보를 명확히 파악할 수 있습니다.
- **노이즈와 방사선 노출**: 방사선량에 따라 노이즈가 발생할 수 있으며, 낮은 방사선량 설정 시 화질 저하의 문제가 있을 수 있습니다.

## 3. 해당 이미지에 적합한 전처리 방법
- **강도 조정 및 정규화**
  - CT 이미지의 HU 값을 정규화하여 다른 이미지와 비교하거나, 모델 학습에 적합한 범위로 맞춥니다.
  - Min-Max Scaling을 통해 HU 값을 [0,1] 범위로 변환하여 대비를 높이고 이미지 일관성을 유지합니다.
- **노이즈 제거**
  - Gaussian 필터와 Median 필터를 통해 고주파 노이즈를 줄이고, CT 이미지의 세부 구조를 유지하면서 이미지의 품질을 향상시킵니다.
- **Edge Enhancement (경계 강조)**
  - Sobel 또는 Laplacian 필터를 사용해 구조의 경계를 강조하여 병변을 명확히 구분할 수 있도록 합니다.

## 4. 주요 응용 분야 및 활용 예시
- **종양 진단 및 분석**: CT는 종양의 위치와 크기를 정밀하게 파악하여, 종양의 성격(양성 또는 악성)을 구분하거나, 치료 후 추적 관찰에 유리합니다.
- **내부 장기 상태 평가**: 폐, 간, 신장 등 내부 장기의 손상 여부나 상태를 파악하는 데 유용하며, 빠르고 정밀한 진단이 가능합니다.
- **심혈관 질환 진단**: 관상동맥의 석회화 수준이나 혈관의 폐색 여부를 파악하여 심혈관 질환을 진단할 수 있습니다.

## 5. 데이터셋 예시와 주요 특징
- **LIDC-IDRI**: 폐 결절 검출을 위한 데이터셋으로, 종양 크기 및 위치에 대한 라벨이 포함되어 있어 폐 질환 연구에 유용합니다.
- **Pancreas-CT**: 췌장 CT 이미지를 포함한 데이터셋으로, 췌장 주변의 조직을 포함해 다양한 장기와의 관계를 파악하는 데 도움이 됩니다.
- **NSCLC Radiomics**: 비소세포 폐암 환자의 CT 이미지 데이터로, 암의 종류 및 위치 정보를 제공하며, 종양 연구 및 분석에 적합합니다.

## 6. 전처리 시 고려할 잠재적 문제점 및 해결 방법
- **HU 값 범위 조정**
  - 해결 방법: HU 값을 정규화하거나 클리핑하여 이미지 대비를 높이고, 일관성 있는 데이터로 변환합니다.
- **노이즈 제거 및 디테일 보존**
  - 해결 방법: Gaussian 및 Median 필터를 통해 노이즈를 줄이고, 과도한 노이즈 제거로 인해 중요한 디테일이 손상되지 않도록 주의합니다.
- **방사선 노출에 따른 화질 저하**
  - 해결 방법: 저선량 CT의 경우, Super-Resolution을 통해 저해상도를 보완하고 화질을 개선할 수 있습니다.

## 7. 딥러닝 모델의 추천 아키텍처 및 적용 방법
- **3D CNN, ResNet**: 3D 슬라이스 데이터를 활용해 종양 탐지 및 장기 상태 분석을 위한 분류 작업에 적합합니다.
- **U-Net, V-Net**: CT 이미지의 병변 영역을 세분화하기 위한 모델로, 특히 종양이나 장기의 윤곽을 명확히 잡아내는 데 유리합니다.
- **모델 적용 방법**
  - 슬라이스 별로 전처리된 CT 데이터를 모델에 입력하여 종양 또는 병변을 탐지하고, 연속된 슬라이스를 활용해 3D 구조를 학습시킵니다.
  - Pre-trained 모델을 사용해 Fine-tuning하거나, 대량의 CT 이미지로 훈련된 Radiomics 모델을 적용하여 전이 학습을 수행할 수 있습니다.

## 8. 최신 연구 동향 요약
- **3D CNN과 Transformer 융합 모델**: 3D CNN의 공간 정보를 학습하는 능력과 Transformer의 전체적 맥락 이해 능력을 결합하여 더 정확한 병변 탐지와 구조 세분화 성능을 보여줍니다.
- **Radiomics와 AI 융합 연구**: CT 영상에서 병변의 질감, 모양, 크기 등 다양한 특징을 추출해 암 예후 예측 및 치료 반응 분석에 활용하는 연구가 활발히 진행 중입니다.
- **Self-supervised 및 Transfer Learning**: 큰 데이터 없이도 전이 학습을 통해 성능을 높이며, 병변 탐지의 정확도를 개선하는 방식으로 사용되고 있습니다.
- **Low-Dose CT Reconstruction**: 저선량 CT의 화질을 개선하기 위해, Super-Resolution이나 노이즈 제거 네트워크를 적용하여 환자 안전을 유지하면서도 고품질 CT 영상을 생성하는 연구가 진행 중입니다.