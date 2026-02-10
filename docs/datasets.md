# Datasets

## PD4T (Parkinson's Disease 4 Tasks)

**Source**: Li et al. 2024
**Tasks**: 4 MDS-UPDRS Part III motor tasks

### Overview

| Property | Value |
|----------|-------|
| Subjects | 50 PD patients |
| Tasks | 4 (Finger Tapping, Gait, Hand Movement, Leg Agility) |
| Total videos | 2,932 |
| Score range | UPDRS 0-4 |
| Video format | MP4 |
| Split | Stratified (train/valid/test, no patient overlap) |

### Video Counts by Task

| Task | Videos | Subjects |
|------|--------|----------|
| Finger Tapping | 807 | 30 |
| Gait | 426 | 30 |
| Hand Movement | 848 | 30 |
| Leg Agility | 851 | 30 |

### Score Distribution (Stratified Split)

#### Finger Tapping
| Split | Total | Score 0 | Score 1 | Score 2 | Score 3 | Score 4 |
|-------|-------|---------|---------|---------|---------|---------|
| Train | 561 | 109 | 324 | 111 | 15 | 2 |
| Valid | 117 | 21 | 70 | 24 | 2 | 0 |
| Test | 128 | 22 | 71 | 29 | 6 | 0 |

#### Gait
| Split | Total | Score 0 | Score 1 | Score 2 | Score 3 | Score 4 |
|-------|-------|---------|---------|---------|---------|---------|
| Train | 298 | 137 | 111 | 45 | 5 | 0 |
| Valid | 62 | 29 | 23 | 9 | 1 | 0 |
| Test | 66 | 30 | 24 | 10 | 2 | 0 |

#### Hand Movement
| Split | Total | Score 0 | Score 1 | Score 2 | Score 3 | Score 4 |
|-------|-------|---------|---------|---------|---------|---------|
| Train | 591 | 163 | 286 | 123 | 16 | 3 |
| Valid | 126 | 36 | 56 | 29 | 4 | 1 |
| Test | 131 | 35 | 65 | 27 | 3 | 1 |

#### Leg Agility
| Split | Total | Score 0 | Score 1 | Score 2 | Score 3 | Score 4 |
|-------|-------|---------|---------|---------|---------|---------|
| Train | 593 | 284 | 264 | 37 | 5 | 3 |
| Valid | 124 | 59 | 55 | 6 | 4 | 0 |
| Test | 134 | 64 | 57 | 11 | 2 | 0 |

### Annotation Format

CSV format: `video_id_subject,frame_count,score`

```
15-005087_l_042,168,3
│           │ │    │
│           │ │    └── UPDRS score (0-4)
│           │ └── Subject ID (folder name)
│           └── video_id
└── File: Videos/{task}/042/15-005087_l.mp4
```

### Key Characteristics

- **Class Imbalance**: Score 0-1 dominant (~80%), Score 3-4 rare (<5%)
- **Data Leakage in Original Split**: Use `stratified/` only
- **Bilateral**: Finger Tapping has left/right (`_l`, `_r`) variants

---

## TULIP (CVPR 2024)

**Source**: CVPR 2024 Workshop
**Focus**: Multi-camera tracking for clinical UPDRS

### Overview

| Property | Value |
|----------|-------|
| Subjects | 15 PD patients |
| Tasks | 25 MDS-UPDRS items |
| Cameras | 6 synchronized views |
| Score range | UPDRS 0-4 |
| Unique feature | Multi-view, full UPDRS coverage |

### Relevance to Our Work

- **Cross-dataset evaluation**: Train on PD4T, test on TULIP
- **Multi-view analysis**: VLM performance across camera angles
- **Broader UPDRS coverage**: 25 items vs PD4T's 4 tasks

### Limitations

- Small sample size (15 subjects)
- Different recording environment from PD4T
- May need domain adaptation
