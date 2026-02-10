# Hawkeye Paper

VLM-based Automated MDS-UPDRS Motor Assessment for Parkinson's Disease

## Overview

This repository contains experiment code, evaluation scripts, and documentation for the Hawkeye VLM research project. We evaluate Vision-Language Models (VLMs) on MDS-UPDRS Part III motor tasks using video-based assessment.

**Research Gap**: No prior study has applied VLMs to PD motor scoring (MDS-UPDRS). This project addresses that gap.

## Repository Structure

```
Hawkeye_paper/
├── docs/                        # Documentation
│   ├── datasets.md              # Dataset descriptions (PD4T, TULIP)
│   ├── evaluation_metrics.md    # Evaluation metrics & target venues
│   └── literature_review.md     # Related work survey
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
| **PD4T** | Li et al. 2024 | 50 | 4 (FT, Gait, HM, LA) | 2,932 | UPDRS 0-4 |
| **TULIP** | CVPR 2024 | 15 | 25 UPDRS items | Multi-view (6 cam) | UPDRS 0-4 |

> Raw data is NOT included in this repo. See `data/README.md` for access instructions.

## Evaluation Metrics

- **Primary**: Spearman rho + QWK (Quadratic Weighted Kappa)
- **Secondary**: MAE, MA-MAE, Exact Accuracy, OBO Accuracy

## Target Venues

| Period | Venue | IF | Paper Focus |
|--------|-------|----|-------------|
| H1 2026 (Apr-May) | npj Digital Medicine | 15.1 | VLM UPDRS Scoring |
| H1 2026 (Apr-May) | JAMA Network Open | 13.8 | AI vs Clinician |
| H2 2026 (Nov-Dec) | NeurIPS D&B 2027 | - | MotorExam Benchmark |
| H2 2026 (Nov-Dec) | Lancet Digital Health | 24.1 | Clinical + SNUH Data |

## VLM Models

| Model | Provider | Video Support | Context |
|-------|----------|---------------|---------|
| GPT-4o | OpenAI | Native | 128K |
| Gemini 2.0 Flash | Google | Native | 1M |
| Claude 3.5 Sonnet | Anthropic | Frame sampling | 200K |
| Qwen2.5-VL-72B | Alibaba | Native | 128K |
| LLaVA-Video-72B | Open-source | Native | - |

## Team

- YoungKwon Lee (Lead, PT/SNUH)
- JaeHyun (VLM), DongSung (QA/Data), HyunMin (Skeleton)
- SeungWon (EDA), SangHu (Clinical), InHo (Infra)

## Related Repositories

- [Hawkeye (Main)](https://github.com/Youngkwon-Lee/Hawk_I) - Full system with backend/frontend
