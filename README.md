# ThinQ Sense — AI & Perception

> ITE351 — AI & Applications | Hanyang University, Fall 2026

This repository investigates lightweight local perception and multimodal context inference for the ThinQ Sense prototype.

## Research Questions

1. Can person/pose recognition identify useful household states in real time?
2. Does radar-assisted late fusion improve presence or position robustness under occlusion?
3. How should latency, accuracy, and privacy be evaluated across modalities?

## Planned Pipeline

```text
Camera → person / pose inference ─┐
                                 ├→ late fusion → normalized semantic events
Radar → target position / motion ┘
Audio → optional VAD / speaker context
```

## Suggested Structure

```text
src/perception/    # camera/audio/radar adapters
src/fusion/        # temporal alignment, identity association, confidence
experiments/       # notebooks and reproducible experiments
configs/           # model and threshold settings
tests/             # unit and offline evaluation tests
results/           # non-sensitive aggregate metrics
```

## Evaluation Plan

- Accuracy/F1 for activity and room state; specify ground truth and per-class sample counts.
- Inference latency and throughput on available hardware.
- Robustness to low light, occlusion, sensor disconnection, and multiple people.
- Data privacy: do not commit identifiable face, voice, or home video recordings.

Model choices and radar support are **candidates, not completed implementations**.

See [ITE351 blog](https://github.com/HY-ThinQ-Sense/Thinq-Sense-blog) for research logs and proposal.
