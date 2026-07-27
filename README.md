# Hawkeye Paper

VLM-based Automated MDS-UPDRS Motor Assessment for Parkinson's Disease

## Overview

This repository contains experiment code, evaluation scripts, and documentation for the Hawkeye VLM research project. We evaluate Vision-Language Models (VLMs) on MDS-UPDRS Part III motor tasks using video-based assessment.

**Research focus**: MDS-UPDRS 순서형 채점에서 native video·frame·pose/kinematic 경로를 비교하고, 시간 근거와 외부 검증을 포함한 재현 가능한 평가를 만든다. “최초/없음” 주장은 검색식·검색일·포함 기준과 함께만 사용한다.

**IRB**: SNUH 신청 완료 (승인 대기 중)

## Research Pipeline (reviewed 2026-07-27)

```
Approved video/frame candidate → structured score + timestamp evidence → clinician review → local student candidate → locked test
```

- **V1**: approved native-video path → Test
- **V2**: fixed frame-sequence path → Test
- **V3**: local VLM + reviewed rationale + kinematic features → Test
- **V4**: quality-gated abstention → coverage and selective error

## Repository Structure

```
Hawkeye_paper/
├── docs/                        # Documentation
│   ├── datasets.md              # Dataset descriptions (PD4T, TULIP)
│   ├── dataset_catalog.md       # Comprehensive dataset inventory (30+)
│   ├── evaluation_metrics.md    # Evaluation metrics & target venues
│   ├── eda_datasets.html        # Interactive EDA report
│   ├── evaluation_metrics_venues.html
│   ├── literature_review.html   # Related work survey
│   └── paper4_vlm_plan.html     # VLM experiment plan
├── data/                        # Data documentation (NO raw data)
│   └── README.md                # Data access & setup instructions
├── experiments/
│   ├── configs/                 # Experiment configurations
│   └── results/                 # Experiment results & tables
├── scripts/
│   ├── evaluation/              # Evaluation & metric scripts
│   └── preprocessing/           # Data preprocessing
└── .gitignore
```

## Datasets

| Dataset | Source | Subjects | Tasks | Videos | Scores |
|---------|--------|----------|-------|--------|--------|
| **PD4T** | Li et al. 2024 | 35 unique (30/task) | 4 (FT, Gait, HM, LA) | 2,932 | UPDRS 0-4 |
| **TULIP** | CVPR 2024 | 15 | 25 UPDRS items | Multi-view (6 cam) | UPDRS 0-4 |

> Raw data is NOT included in this repo. See `data/README.md` for access instructions.
> IMPORTANT: Always use `stratified/` split (original has data leakage).

## Experiment Design

| Exp | Method | Purpose |
|-----|--------|---------|
| **Exp A** | Qwen3-VL + Teacher Rationale | Rationale distillation 효과 검증 |
| **Exp B** | Qwen3-VL + Rationale + Kinematic Features | 멀티모달 입력 효과 검증 |
| Baseline 1 | Approved native-video / frame zero-shot paths | Commercial-path reference; not assumed upper bound |
| Baseline 2 | CORAL Ordinal (기존 ML) | Traditional ML 비교 |
| Ablation | FPS (1, 8, 15, 30) | 최적 temporal resolution |

## VLM Models

### Teacher / commercial reference paths
| Path | Input | Evaluation rule |
|------|-------|-----------------|
| Native-video candidate | approved video input | pin model ID, API version, file handling, cost, and call date for each run |
| Frame-sequence candidate | 16/32 uniformly sampled images | store frame indices and report temporal-information loss |

### Student (Fine-tuning Target)
| Model | Size | Video | Fine-tune | VRAM |
|-------|------|-------|-----------|------|
| **Qwen3-VL-8B** | 8B | Native | DoRA/DPO/GRPO | ~16GB |

### Cost policy

Do not treat static provider prices as durable facts. Report actual tokens, duration, latency, cost, model ID, region, and run date from a frozen input manifest.

## Evaluation Metrics

- **Primary**: Spearman rho + QWK (Quadratic Weighted Kappa)
- **Secondary**: MAE, MA-MAE, Exact Accuracy, OBO Accuracy
- **Reliability/Safety**: subject-level bootstrap 95% CI, coverage/selective metrics after abstention, timestamp–rubric clinician review
- **Legacy**: Pearson r (기존 CORAL baseline 호환)

## Target Venues

### Journals (Q1)
| Field | Journal | IF |
|-------|---------|-----|
| 융합 | **npj Digital Medicine** | 15.1 |
| 공학 | **Medical Image Analysis** | 11.8 |
| 공학 | **IEEE TMI** | 9.8 |
| 임상 | **npj Parkinson's Disease** | 8.2 |
| 임상 | **Movement Disorders** | 7.6 |

### Conferences
| Conference | Deadline | Notes |
|------------|----------|-------|
| **MLHC 2026** | Apr 17 | ML x Healthcare |
| **BIBM 2026** | Jul 5 | Medical Informatics |

## Key References

- **VFM PD Screening (arXiv:2602.13507)**: 1,888명, 32,847 videos, 16 tasks - VFM benchmark (binary PD/non-PD, NOT UPDRS scoring)
- **MedScope (arXiv:2602.13332)**: Tool-using clinical video reasoning
- **GLIMPSE (EMNLP 2025)**: benchmark for temporal, rather than key-frame-only, video reasoning
- **Human motion VLM study (2026)**: fine-grained rehabilitation-motion quantification remains unreliable without task-specific safeguards
- **CARE-PD (NeurIPS 2025)**: Cross-dataset PD (Gait only, SMPL)
- **FLEX (2025)**: VLM for AQA, Qwen2.5-VL-3B

## Team

| Role | Member | Responsibility |
|------|--------|----------------|
| Team Lead | 영권 (YK) | 전체 총괄, GPT Rationale 생성, GT 검수 |
| DS Lead | 영빈 | EDA/전처리, Qwen-VL 학습 및 평가 |
| Skeleton | 대현 | Skeleton 작업, Kinematic Feature 추출, 저널 리서치 |
| 선행연구 | 연주 | 선행연구 조사, Rationale 평가 기준 |
| GT 검수 | 동성 | GT 검수 (영권과 공동) |
| Reference | 례미 | 영상/문헌 수집 |
| Data Mgmt | 두연 | 영상/데이터 관리 |

## Related Repositories

- [Hawkeye (Main)](https://github.com/Youngkwon-Lee/Hawk_I) - Full system with backend/frontend/ML models
