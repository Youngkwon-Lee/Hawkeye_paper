# PT_dataset - Dataset Catalog

> Google Drive 공유 폴더 데이터셋 카탈로그
> 최종 업데이트: 2026-02-10

## Drive 폴더 구조

```
PT_dataset/
├── 1_disease_specific/       ← 질환 특이적 (5개)
│   ├── 1_PD4T/
│   ├── 1_TULIP/
│   ├── 1_care_pd/
│   ├── 1_REMAP/
│   └── 1_WearGait-PD/
├── 2_rehabilitation/         ← 재활 (10개)
│   ├── 2_Clinical_Gait_Signals/
│   ├── 2_FineRehab/
│   ├── 2_IntelliRehabDS/
│   ├── 2_keraal/
│   ├── 2_KIMORE/
│   ├── 2_KINECAL/
│   ├── 2_REHAB24-6/
│   ├── 2_UCO_physical_Rehabilitation/
│   ├── 2_UI-PRMD/
│   └── 2_UL-RED/
├── 3_action_recognition/     ← 일반 동작 (4개)
│   ├── 3_Kinetics-700/
│   ├── 3_NTU_RGB+D/
│   ├── 3_PKU-MMD/
│   └── 3_ROSE_DATASET/
├── _project/                 ← 프로젝트 관리
│   ├── docs/
│   ├── reference/
│   └── 연구/
├── _legacy/
└── dataset_catalog.md
```

## 분류 기준

| 접두사 | 카테고리 | 설명 |
|--------|----------|------|
| **1_** | 질환 특이적 (Disease-specific) | 파킨슨병, Dyskinesia 등 특정 질환 데이터 |
| **2_** | 재활 (Rehabilitation) | 물리치료, 운동 품질 평가, 센서 기반 재활 |
| **3_** | 일반 동작 (Action Recognition) | 범용 동작 인식, 스포츠, 일상 동작 |

---

## 1_ 질환 특이적 (Disease-specific)

### 1_PD4T
- **논문**: Li et al., 2024
- **질환**: Parkinson's Disease
- **피험자**: 50명 PD 환자
- **Tasks**: 4 (Finger Tapping, Gait, Hand Movement, Leg Agility)
- **영상 수**: 2,932개 (MP4)
- **점수**: MDS-UPDRS 0-4
- **크기**: ~4.63GB (zip)
- **비고**: 프로젝트 핵심 데이터셋. Stratified split 사용 필수 (원본에 data leakage 있음)

### 1_TULIP
- **논문**: CVPR 2024 Workshop
- **질환**: Parkinson's Disease
- **피험자**: 12명 (Subject 01,02,05-08,10-15)
- **Tasks**: 26개 MDS-UPDRS items (양측 포함)
- **카메라**: 6개 동기화 뷰
- **점수**: UPDRS 0-4
- **비고**: Cross-dataset 평가용, multi-view 분석 가능

### 1_care_pd
- **논문**: CARE-PD (NeurIPS 2025 D&B)
- **질환**: Parkinson's Disease - Gait
- **피험자**: 362명, 9개 센터
- **데이터**: SMPL mesh 기반 3D body model
- **점수**: UPDRS Gait score
- **비고**: 유일한 cross-dataset PD 논문, 다기관 데이터

### 1_REMAP
- **논문**: Nature Scientific Data, 2023
- **질환**: Parkinson's Disease
- **데이터**: Multimodal (wearable sensors, video, clinical)
- **초점**: Real-world mobility activities
- **비고**: 실제 생활 환경에서의 PD 운동 데이터

### 1_WearGait-PD
- **논문**: Anderson et al., 2024 (preprint)
- **질환**: Parkinson's Disease - Gait
- **데이터**: Wearable IMU sensors
- **피험자**: PD 환자 + age-matched 대조군
- **플랫폼**: Synapse (syn52540892)
- **비고**: 웨어러블 보행 센서 데이터, 비디오 아님

### 1_parkinson
- **질환**: Parkinson's Disease
- **크기**: ~4.9GB
- **비고**: 로컬(D:\)에서 업로드 필요

### 1_UDysRS
- **질환**: Unified Dyskinesia Rating Scale
- **크기**: 137MB
- **비고**: 이상운동증 평가 데이터, 로컬(D:\)에서 업로드 필요

### 1_pd_pose_est
- **질환**: Parkinson's Disease
- **크기**: 2.1GB
- **초점**: Pose estimation for PD
- **비고**: 로컬(D:\)에서 업로드 필요

---

## 2_ 재활 (Rehabilitation)

### 2_KIMORE
- **논문**: IEEE Trans. Neural Syst. Rehab. Eng., 2019
- **도메인**: 물리치료 재활
- **피험자**: 78명 (건강인 + 환자)
- **Exercises**: 5종 재활 운동
- **센서**: Kinect v2
- **점수**: 임상 점수 포함
- **크기**: ~5.5GB

### 2_FineRehab
- **도메인**: 재활 운동 품질 평가
- **방법**: Supervised contrastive learning
- **비고**: 운동 품질 세밀 평가

### 2_UI-PRMD
- **논문**: Liao et al., 2018 (University of Idaho)
- **도메인**: 물리치료 운동
- **피험자**: 10명 건강인
- **Exercises**: 10종 재활 운동 x 10회 반복
- **센서**: Vicon + Kinect
- **데이터**: Position + angle

### 2_UL-RED
- **논문**: Nature Scientific Data, 2025 (University of Liverpool)
- **도메인**: 상지 재활 운동
- **데이터**: Motion capture
- **비고**: 현재 Drive 폴더 비어있음, 로컬 데이터 업로드 필요

### 2_keraal
- **논문**: Blanchard et al., Biomed Research International, 2022
- **도메인**: 요통 재활 (Low-back pain)
- **피험자**: 9명 건강인 + 12명 요통 환자
- **Exercises**: 3종 요통 재활 운동
- **비고**: 임상 환자 포함, 로봇 코칭 시스템 연구
- **크기**: ~8.4GB

### 2_IntelliRehabDS
- **논문**: MDPI Data, 2021
- **도메인**: 물리치료 재활 동작
- **데이터**: Skeleton 기반
- **비고**: 재활 동작 인식 벤치마크

### 2_KINECAL
- **논문**: PhysioNet, 2023 / Nature Scientific Data, 2023
- **도메인**: 낙상 위험 평가 / 균형 장애
- **데이터**: Kinect skeleton
- **비고**: 균형 평가 특화

### 2_REHAB24-6
- **논문**: SISAP 2024
- **도메인**: 물리치료 pose estimation 분석
- **피험자**: 재활 환자
- **비고**: 다양한 pose estimation 방법 비교

### 2_UCO_physical_Rehabilitation
- **논문**: Sensors, 2023 (University of Cordoba)
- **도메인**: 물리치료 재활
- **데이터**: Pose estimation 기반
- **비고**: 여러 pose estimation 방법론 비교 연구

### 2_Clinical_Gait_Signals
- **도메인**: 보행 분석
- **데이터**: Wearable sensor (건강인)
- **비고**: 정상 보행 기준 데이터

### 2_lateralstepdown
- **도메인**: 측면 스텝다운 운동
- **크기**: ~6.8GB
- **비고**: 로컬(D:\)에서 업로드 필요

### 2_gait_wearable_sensor
- **도메인**: 보행 웨어러블 센서
- **크기**: ~9.7GB (9,979 files)
- **비고**: 대용량, 로컬(D:\)에서 업로드 필요

### 2_IMU_dataset
- **도메인**: IMU 센서 기반 운동 데이터
- **크기**: 356MB
- **비고**: 로컬(D:\)에서 업로드 필요

### 2_EMG_RGB
- **도메인**: EMG + RGB 멀티모달
- **크기**: 4MB
- **비고**: 로컬(D:\)에서 업로드 필요

---

## 3_ 일반 동작 (Action Recognition)

### 3_Kinetics-700
- **출처**: DeepMind
- **도메인**: 범용 동작 인식
- **Classes**: 700개 일상/스포츠 동작
- **데이터**: YouTube 비디오
- **비고**: 대규모 사전학습용

### 3_NTU_RGB+D
- **출처**: NTU (Rose Lab)
- **도메인**: 범용 동작 인식
- **Classes**: 60/120개 (RGB+D / RGB+D 120)
- **데이터**: RGB + Depth + Skeleton + IR
- **센서**: Kinect v2 x 3대
- **비고**: Skeleton 기반 action recognition 표준 벤치마크

### 3_PKU-MMD
- **출처**: Peking University
- **도메인**: Multi-modal 동작 인식
- **데이터**: RGB + Skeleton
- **비고**: 대규모 multi-modal 벤치마크

### 3_ROSE_DATASET
- **출처**: NTU Rose Lab
- **도메인**: Action recognition challenge
- **비고**: NTU RGB+D 관련 챌린지 데이터

---

## 기타 폴더

| 폴더 | 설명 |
|------|------|
| **연구** | 팀원별 개인 작업 폴더 (공영빈, 김동성, 도례미, 이영권, 최대현) |
| **docs** | IRB 문서 |
| **reference** | 의료AI 교육사업 자료, 발표자료, 회의록 |
| **legacy** | 이전 버전 자료 |

---

## 로컬 전용 데이터 (D:\, Drive 미등록)

| 폴더 | 크기 | 카테고리 | 설명 |
|------|------|----------|------|
| `triage` | 21GB | - | 응급 트리아지 |
| `tulip_vlm_experiment` | 2.4GB | 실험 | VLM 실험 결과 |
| `videos-001` | 2.6GB | - | 비디오 데이터 |
| `aihub` | 180MB | - | AI Hub 데이터 |
| `e-skin` | 14MB | 센서 | 전자피부 센서 |
| `scapula` | 9.5MB | 재활 | 견갑골 |
| `lumbar` | 4MB | 재활 | 요추 |
| `tone_rgb` | 3MB | 센서 | 근긴장도 RGB |
| `taichi` | 2.5MB | 운동 | 태극권 |
