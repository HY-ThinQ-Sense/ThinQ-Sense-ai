# LG-EYEAR-ai — Multimodal EYEAR Node Perception

AI and sensing research repository for EYEAR, Hanyang University (CSE406 / ITE351, Fall 2026).

> **Status:** Proposed pipeline and evaluation plan. Candidate models, available sensor data, and measured performance will be recorded as they are validated.

## EYEAR Node Concept

A proposed **EYEAR Node** is a room-level device with **camera + microphone + mmWave radar + local compute + secure communication**. Rather than running one large end-to-end multimodal model, it uses specialized local components:

| Modality | Inputs | Candidate method | Structured outputs |
| --- | --- | --- | --- |
| Vision | Video frames | Pretrained person / pose detection; optional face embedding | Presence, tracks, posture, activity candidates, identity candidates |
| Audio | Local audio | Voice Activity Detection; optional consented speaker embedding | Speech activity, registered speaker candidate, ambiguous/unknown |
| mmWave | Radar measurements | Vendor target output + tracking/calibration | Target presence, position/range, motion/velocity |
| Fusion | Timestamped modality outputs | Temporal alignment, calibration, association, confidence handling | Semantic Event for each observed target/room |

Radar does **not** automatically identify people, detect through every wall, or reliably recognize fine posture. Continuous speech in a singly occupied room is not definitive evidence of a call or meeting; it may only support a `call_or_meeting_candidate` hypothesis.

## Research Tasks

1. **Pretrained-model baseline** — Run person, pose and optional face/voice embeddings without training foundation models from scratch.
2. **Posture/activity classification** — Extract pose/ROI/temporal features; compare transparent rules against small classical classifiers if labeled data are available.
3. **Radar integration** — Evaluate a compatible mmWave UART device such as HLK-LD2450 where available; parse time-stamped targets, not hypothetical through-wall or identity outputs.
4. **Late fusion** — Compare camera-only, radar-only, and combined presence/position estimates, with synchronized timestamps and coordinate calibration.
5. **Semantic Event Publisher** — Pass only structured observations to the central [LG-EYEAR system](https://github.com/HY-LG-EYEAR/LG-EYEAR).
6. **Optional experiments** — Speaker verification, next-room prediction, learned activity recognition; only when data and time justify them.

## Datasets and Reproducibility

- Public pose/activity references (e.g. COCO Keypoints, NTU RGB+D) are candidates; validate license, label mapping and sensor compatibility before use.
- Record consented short scenarios for posture/activity classification and multi-node replay.
- Store structured radar measurements and ground-truth annotations separately from inference outputs.
- Split train/test by **recording session or participant**, not by randomly splitting adjacent video frames.
- Report accuracy/F1, latency, resource use, position error, tracking stability and uncertainty.

**Do not commit** personal face/voice recordings, biometric embeddings, raw household video, device credentials, or large model artifacts to public GitHub.

## Suggested Structure

```text
src/
  vision/
  audio/
  radar/
  fusion/
  event_publisher/
configs/
experiments/
  vision/
  audio/
  radar/
  fusion/
results/
tests/
datasets/README.md    # access rules and schema; no private raw media
```

## Integration Contract

```text
sensor streams → specialized inference → late fusion
→ timestamped Semantic Events → central context API
```

A Node processing failure should yield `unavailable` or `unknown` rather than a fabricated observation. Raw camera/audio data should not be passed to the central context interface.

## Evaluation and Course Materials

- [CSE406 documents / specification](https://github.com/HY-LG-EYEAR/LG-EYEAR-docs)
- [ITE351 technical blog](https://github.com/HY-LG-EYEAR/LG-EYEAR-blog)
- [Main backend + 3D simulator](https://github.com/HY-LG-EYEAR/LG-EYEAR)
