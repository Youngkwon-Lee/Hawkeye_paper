# Data Access Instructions

This repository does **NOT** contain raw data. Video datasets are large and subject to licensing restrictions.

## PD4T Dataset

- **Paper**: Li et al., "PD4T: A Parkinson's Disease Tremor Dataset", 2024
- **Access**: Request from authors / institutional access
- **Size**: ~30GB (video files)

### Setup

After obtaining the dataset, place it as:

```
data/raw/PD4T/
└── PD4T/
    └── PD4T/
        ├── Annotations/
        │   ├── Finger tapping/
        │   │   ├── stratified/     # Use these (no data leakage)
        │   │   │   ├── train.csv
        │   │   │   ├── valid.csv
        │   │   │   └── test.csv
        │   │   ├── train.csv       # Original (has leakage - DO NOT USE)
        │   │   └── test.csv
        │   ├── Gait/
        │   ├── Hand movement/
        │   └── Leg agility/
        └── Videos/
            ├── Finger tapping/{subject_id}/*.mp4
            ├── Gait/{subject_id}/*.mp4
            ├── Hand movement/{subject_id}/*.mp4
            └── Leg agility/{subject_id}/*.mp4
```

### Important: Use Stratified Splits Only

The original train/test split has **data leakage** (same patients in both splits):
- Finger Tapping: 1 patient overlap
- Gait: 1 patient overlap
- Leg Agility: 5 patient overlaps

Always use `stratified/` annotations.

## TULIP Dataset

- **Paper**: "TULIP: Multi-camera Multi-person Tracking for Clinical UPdrs Assessment", CVPR 2024
- **Access**: [Dataset page](https://tulip-cvpr2024.github.io/) (check availability)
- **Features**: 15 subjects, 6 camera views, 25 MDS-UPDRS tasks

### Setup

```
data/raw/TULIP/
├── videos/
├── annotations/
└── camera_params/
```

## Verification

After placing data, verify with:

```bash
# Check PD4T structure
ls data/raw/PD4T/PD4T/PD4T/Videos/
# Expected: Finger tapping/  Gait/  Hand movement/  Leg agility/

# Check annotation counts
wc -l data/raw/PD4T/PD4T/PD4T/Annotations/*/stratified/*.csv
```
