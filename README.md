# Hawkeye Paper

VLM-based Automated MDS-UPDRS Motor Assessment for Parkinson's Disease

## Overview

This repository contains experiment code, evaluation scripts, and documentation for the Hawkeye VLM research project. We evaluate Vision-Language Models (VLMs) on MDS-UPDRS Part III motor tasks using video-based assessment.

**Research Gap**: No prior study has applied VLMs to PD motor scoring (MDS-UPDRS). This project addresses that gap.

**IRB**: SNUH 신청 완료 (승인 대기 중)

## Research Pipeline (2/24 확정)

```
Teacher (Gemini 2.5 Pro / GPT-4.1) → Rationale 생성 → GT 검수 → Qwen3-VL-8B 학습 → Test
```

- **Exp A**: Qwen-VL + Rationale only → Test
- **Exp B**: Qwen-VL + Rationale + Kinematic Features → Test

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
| Baseline 1 | Gemini 2.5 Pro / GPT-4.1 Zero-shot | Teacher 성능 = upper bound |
| Baseline 2 | CORAL Ordinal (기존 ML) | Traditional ML 비교 |
| Ablation | FPS (1, 8, 15, 30) | 최적 temporal resolution |

## VLM Models

### Teacher (Rationale Generation)
| Model | Provider | Video Input | Context | Cost (Input/1M) |
|-------|----------|-------------|---------|-----------------|
| **Gemini 2.5 Pro** | Google | Native video (1fps) | 1M | $1.25 |
| **GPT-4.1** | OpenAI | Frames only | 1M | $2.00 |
| Gemini 3.1 Pro Preview | Google | Native video | 1M | $2.00 |

### Student (Fine-tuning Target)
| Model | Size | Video | Fine-tune | VRAM |
|-------|------|-------|-----------|------|
| **Qwen3-VL-8B** | 8B | Native | DoRA/DPO/GRPO | ~16GB |

### Budget Options (Batch Processing)
| Model | Cost/20s video | 260 videos |
|-------|---------------|------------|
| Gemini 2.5 Flash-Lite | $0.0007 | $0.18 |
| Gemini 2.5 Flash | $0.003 | $0.78 |
| GPT-4.1-mini | $0.009 | $2.34 |

## Evaluation Metrics

- **Primary**: Spearman rho + QWK (Quadratic Weighted Kappa)
- **Secondary**: MAE, MA-MAE, Exact Accuracy, OBO Accuracy
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
