# VLM Video Evaluation Protocol

> Last reviewed: 2026-07-27
> Use case: research-only MDS-UPDRS Part III video assessment

## Rule: pin an execution, not a provider marketing claim

Model availability, pricing, file limits, and retention settings change. Every run must record:

- provider and exact model ID;
- API/version, region, date, and data-processing approval;
- original clip hash, decoding settings, sampling indices, prompt version, and seed;
- input/output tokens, cost, latency, and structured-output validation result.

Do not publish a static cost comparison as an enduring fact. Quote a measured run and its date instead.

## Comparable input paths

| Path | Input | Role |
|---|---|---|
| V0 | clinical/rule or ordinal ML baseline | establishes the non-VLM reference |
| V1 | approved native-video API | tests direct video understanding |
| V2 | 16/32 uniformly sampled frames | measures loss from frame-only input |
| V3 | RGB/frames + pose and kinematic features | tests whether fine-motion cues need structured support |
| V4 | quality-gated abstention | measures safe coverage rather than forced scoring |

V1–V4 use an identical subject-level split. Only validation data can choose prompts, model routes, or frame counts.

## Required output schema

```json
{
  "updrs_score": 0,
  "confidence": 0.0,
  "abstain": false,
  "abstain_reason": null,
  "evidence": [{"start_s": 0.0, "end_s": 0.0, "rubric_feature": ""}],
  "rationale": ""
}
```

The score is invalid when the schema fails, the referenced evidence interval is absent, or the video fails the quality gate.

## Quality gate

Record camera view, resolution/FPS, occlusion, number of people, movement visibility, and usable temporal span. Route each clip to `pass`, `review`, or `abstain`; report the reason and rate by task and dataset.

## Evaluation

- Primary: QWK and Spearman rho.
- Secondary: MAE, macro-MAE, exact and off-by-one accuracy.
- Safety/reliability: coverage, selective QWK/MAE after abstention, subject-level bootstrap 95% CI, task/score/camera-quality error strata.
- Rationale: blinded clinician assessment of timestamp grounding and MDS-UPDRS-rubric consistency. Do not use fluent prose alone as evidence of correctness.

## Service and data policy

- Use commercial APIs only after the governing IRB/DUA and data-retention conditions permit the exact transfer.
- Prefer local/HPC execution for restricted video.
- CVAT or Label Studio may pre-label tracks/pose for human correction; automatic predictions never become ground truth without review.
- Never commit raw video, raw labels, credentials, or run artifacts containing identifiers.

## Official documentation to check before every pilot

- [Gemini video understanding](https://ai.google.dev/gemini-api/docs/video-understanding)
- [OpenAI images and vision](https://developers.openai.com/api/docs/guides/images-vision)
- [Anthropic vision](https://docs.anthropic.com/en/docs/build-with-claude/vision)
- [CVAT automatic annotation](https://docs.cvat.ai/docs/annotation/auto-annotation/automatic-annotation/)
- [Label Studio ML backend](https://labelstud.io/guide/ml)
