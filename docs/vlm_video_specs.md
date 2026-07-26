# VLM Video Processing Specifications

> Last updated: 2026-02-25
> Use case: PD4T 20-second assessment videos, 30fps, 720p

## Research Gap (2026.02 확인)

| 접근 | PD Screening (PD/non-PD) | UPDRS 0-4 Scoring |
|------|--------------------------|-------------------|
| **VFM** (VideoPrism, V-JEPA) | 1편 (arXiv:2602.13507) | **0편** |
| **VLM** (GPT, Gemini, Qwen) | 0편 | **0편** |
| Traditional (MediaPipe + ML) | 다수 | 다수 |

## Video Input Method

| Model | Native Video | Frames Only | Internal FPS | Custom FPS |
|-------|:-:|:-:|-------|:-:|
| Gemini 2.5 Pro | O | O | 1fps fixed | O (as images) |
| Gemini 2.5 Flash | O | O | 1fps fixed | O |
| Gemini 2.5 Flash-Lite | O | O | 1fps fixed | O |
| Gemini 3.1 Pro Preview | O | O | 1fps fixed | O |
| GPT-4.1 | X | O | - | O |
| GPT-4.1-mini | X | O | - | O |
| GPT-4.1-nano | X | O | - | O |
| GPT-4o | X | O | - | O |
| Claude Opus 4.6 | X | O | - | O |
| Claude Sonnet 4.6 | X | O | - | O |
| Qwen3-VL-8B | O (local) | O | ~2fps dynamic | O (configurable) |
| Qwen2.5-VL-72B | O (local) | O | ~2fps dynamic | O |
| InternVL3-8B | X | O | - | O |
| LLaVA-Video-7B | O (local) | O | uniform ~64f | O |

## Tokens & Context Window (720p)

| Model | Tokens/Frame (default) | Tokens/Frame (low) | Max Context | Max Frames (720p) |
|-------|-------|------|---------|-------|
| Gemini 2.5 Pro | 258 | 66 | 1M (2M) | 3,600+ |
| Gemini 2.5 Flash | 258 | 66 | 1M | 3,600+ |
| Gemini 2.5 Flash-Lite | 258 | 66 | 1M | 3,600+ |
| Gemini 3.1 Pro Preview | 258 | 66 | 1M | 900 images |
| GPT-4.1 | ~1,085 | ~85 | 1M | ~920 |
| GPT-4.1-mini | ~1,085 | ~85 | 1M | ~920 |
| GPT-4.1-nano | ~1,085 | ~85 | 1M | ~920 |
| GPT-4o | ~765 | ~85 | 128K | ~166 |
| Claude Opus 4.6 | ~1,229 | - | 200K (1M beta) | ~162 (200K) |
| Claude Sonnet 4.6 | ~1,229 | - | 200K (1M beta) | ~162 (200K) |
| Qwen3-VL-8B | ~660 | configurable | 256K | ~388 |
| Qwen2.5-VL-72B | ~660 | configurable | 131K | ~198 |
| InternVL3-8B | ~512-1024 | - | 33K (64K ext.) | ~32-64 |
| LLaVA-Video-7B | 144 | 576 | 32K | 64 max |

## Cost per 20-Second Video (720p, 500-token response)

### Native Video (where supported)

| Model | Tokens (20s) | Input Cost | Output Cost | Total |
|-------|-------------|-----------|------------|-------|
| Gemini 2.5 Flash-Lite | ~5,800 | $0.001 | $0.000 | **$0.001** |
| Gemini 2.5 Flash | ~5,800 | $0.002 | $0.001 | **$0.003** |
| Gemini 2.5 Pro | ~5,800 | $0.007 | $0.005 | **$0.012** |
| Gemini 3.1 Pro Preview | ~5,800 | $0.012 | $0.006 | **$0.018** |

### 16-Frame Approach

| Model | Input $/M | Output $/M | Tokens (16f) | Total |
|-------|----------|-----------|-------------|-------|
| Gemini 2.5 Flash-Lite | $0.10 | $0.40 | 4,128 | **$0.001** |
| Gemini 2.5 Flash | $0.15 | $0.60 | 4,128 | **$0.001** |
| GPT-4.1-nano | $0.10 | $0.40 | 17,360 | **$0.002** |
| GPT-4.1-mini | $0.40 | $1.60 | 17,360 | **$0.008** |
| Gemini 2.5 Pro | $1.25 | $10.00 | 4,128 | **$0.010** |
| Gemini 3.1 Pro Preview | $2.00 | $12.00 | 4,128 | **$0.014** |
| GPT-4o | $2.50 | $10.00 | 12,240 | **$0.036** |
| GPT-4.1 | $2.00 | $8.00 | 17,360 | **$0.039** |
| Claude Sonnet 4.6 | $3.00 | $15.00 | 19,664 | **$0.067** |
| Claude Opus 4.6 | $15.00 | $75.00 | 19,664 | **$0.333** |

### 30fps Full Frame (600 frames, GPT-4.1)

| Model | Detail | Tokens | Cost/Video | 260 Videos |
|-------|--------|--------|-----------|-----------|
| GPT-4.1 | high | 651,000 | $1.30 | $338 |
| GPT-4.1 | low | 51,000 | $0.10 | $26 |
| GPT-4.1-mini | high | 651,000 | $0.26 | $67.60 |
| GPT-4.1-mini | low | 51,000 | $0.02 | $5.20 |

### PD4T Full Dataset (260 test videos)

| Model | Method | Total Cost |
|-------|--------|-----------|
| Gemini 2.5 Flash-Lite | native video | **$0.26** |
| GPT-4.1-nano | 16 frames | **$0.52** |
| Gemini 2.5 Flash | native video | **$0.78** |
| GPT-4.1-mini | 16 frames | **$2.08** |
| Gemini 2.5 Pro | native video | **$3.12** |
| GPT-4.1 | 16 frames | **$10.14** |
| Claude Opus 4.6 | 16 frames | **$85.80** |

## Fine-tuning Support

| Model | Vision FT | Video FT | Methods |
|-------|:-:|:-:|--------|
| Qwen3-VL-8B | O | O | Full/LoRA/DoRA/DPO/GRPO |
| LLaVA-Video-7B | O | O | Full/LoRA |
| InternVL3-8B | O | O | Full/LoRA |
| GPT-4.1-mini | O | X (images) | Vision SFT + DPO |
| Gemini 2.5 Flash | O | X (text/img) | Vertex AI SFT |
| Claude | X | X | No fine-tuning API |

## Supported Formats

| Model | Video Formats | Image Formats |
|-------|-------------|--------------|
| Gemini family | mp4, mpeg, mov, avi, webm, wmv, 3gpp | png, jpg, webp |
| GPT family | N/A | png, jpg, gif, webp |
| Claude family | N/A | png, jpg, gif, webp |
| Qwen family | mp4, avi, mkv (decord/opencv) | png, jpg |
| InternVL3 | N/A (frame extraction) | png, jpg |
| LLaVA-Video | mp4 (decord) | png, jpg |

## Recommendations for PD4T

| Use Case | Best Choice | Runner-Up |
|----------|------------|-----------|
| Cheapest (commercial) | Gemini Flash-Lite ($0.001) | GPT-4.1-nano ($0.002) |
| Best quality (commercial) | Gemini 2.5 Pro | Gemini 3.1 Pro Preview |
| Best for 30fps analysis | GPT-4.1-mini (600f=$0.26) | Gemini Pro (images, 600f=$0.78) |
| Student fine-tuning | Qwen3-VL-8B (DoRA) | LLaVA-Video-7B |
| Batch processing (260) | Gemini Flash-Lite ($0.26) | GPT-4.1-nano ($0.52) |
