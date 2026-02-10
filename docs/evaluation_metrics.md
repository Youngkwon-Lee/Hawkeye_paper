# Evaluation Metrics & Target Venues

## Metric System

### Primary Metrics

| Metric | Why | Domain Standard |
|--------|-----|-----------------|
| **Spearman rho** | Rank correlation for ordinal scores | AQA standard (56/96 papers) |
| **QWK** | Inter-rater agreement with ordinal penalty | MDS-UPDRS clinical studies |

### Secondary Metrics

| Metric | Purpose |
|--------|---------|
| **MAE** | Average absolute error (interpretable) |
| **MA-MAE** | Macro-averaged MAE (handles class imbalance) |
| **Exact Accuracy** | % exactly correct |
| **OBO Accuracy** | % within +/-1 (clinically meaningful) |

### QWK (Quadratic Weighted Kappa)

Measures agreement between predicted and actual scores, penalizing larger disagreements quadratically:

- Pred=1, GT=2: penalty = (2-1)^2 = 1
- Pred=0, GT=3: penalty = (3-0)^2 = 9

| Range | Interpretation |
|-------|---------------|
| < 0.20 | Poor |
| 0.21-0.40 | Fair |
| 0.41-0.60 | Moderate |
| 0.61-0.80 | Substantial (clinically meaningful) |
| 0.81-1.00 | Almost perfect |

### H1 vs H2 Metric Focus

| Paper | Primary | Secondary | Rationale |
|-------|---------|-----------|-----------|
| **H1 (UPDRS Scoring)** | Spearman + QWK | MAE, MA-MAE, Exact/OBO Acc | Clinical audience wants agreement metrics |
| **H2 (MotorExam Benchmark)** | Spearman + QWK | + Per-level accuracy (L1-L5) | Benchmark needs fine-grained breakdown |

---

## Target Venues

### H1: 2026 Apr-May (UPDRS Scoring Only)

| Venue | IF | Review | Fit |
|-------|-----|--------|-----|
| **npj Digital Medicine** | 15.1 | ~2 months | AI+clinical assessment = perfect match |
| **JAMA Network Open** | 13.8 | ~1.5 months | "AI vs Doctor" framing, high visibility |
| IEEE TNSRE | 4.8 | ~3 months | Rehabilitation engineering, safer option |

### H2-A: 2026 Benchmark Track

| Venue | IF | Deadline | Fit |
|-------|-----|----------|-----|
| Scientific Data | 5.8 | Rolling | Dataset/benchmark paper |
| NeurIPS D&B 2027 | - | Jun 2027 | Top-tier benchmark venue |

### H2-B: 2026 Nov-Dec (Clinical + SNUH)

| Venue | IF | Fit |
|-------|-----|-----|
| **Movement Disorders** | 7.6 | PD specialist journal |
| **Lancet Digital Health** | 24.1 | Ambitious, needs SNUH clinical validation |

### Timeline

```
Feb  Mar  Apr  May  Jun  Jul  Aug  Sep  Oct  Nov  Dec
 |----+----+----+----|----+----+----+----+----+----+---|
 [Exp + Writing] [H1 Submit]                [H2 Submit]
  VLM eval        npj/JAMA    [SNUH Data]   NeurIPS/
  4 tasks         review      collection    Lancet DH
```
