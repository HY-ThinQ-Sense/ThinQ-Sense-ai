# ThinQ Sense — Spatial Perception & Predictive Intelligence

**AI Research and Perception Repository**

> CSE406 Software Engineering · ITE351 AI & Applications  
> Hanyang University, Fall 2026

## Overview

This repository investigates AI techniques for multimodal spatial perception, human activity understanding, and household state prediction in the ThinQ Sense project.

The main objective is to transform local sensor observations into reliable, structured contextual information that supports proactive home appliance orchestration.

The repository focuses on perception and prediction models rather than final appliance decisions.

## Research Objectives

1. Detect and track human occupants using camera-based perception.
2. Estimate posture and activities from visual observations and temporal features.
3. Explore radar-assisted presence and position sensing.
4. Evaluate multimodal late fusion under varying environmental conditions.
5. Predict future room transitions and human activity states.
6. Measure model accuracy, latency, robustness, and resource requirements.

## AI Pipeline

```text
RGB Camera
   |
   +-- Person Detection & Tracking
   |
   +-- Pose Estimation
   |
   +-- Activity Recognition
   |
   +-- Optional Identity Recognition
                    |
                    v
              Vision Context
                    |
mmWave Radar --> Radar Tracking
                    |
Optional Audio --> Acoustic Context
                    |
                    v
              Late Fusion
                    |
                    v
              Semantic Events
                    |
                    v
              Prediction Models
                    |
                    v
           Home Context Integration
```

## Model Candidates

| Task | Candidate Approaches | Expected Output |
|---|---|---|
| Person Detection | Lightweight object/person detector | Bounding boxes, detection confidence |
| Person Tracking | SORT / ByteTrack | Temporary tracking IDs |
| Pose Estimation | MediaPipe Pose Landmarker | Human body landmarks |
| Posture Classification | Rules / Classical ML | Standing, sitting, lying, unknown |
| Activity Recognition | Temporal features, GRU/LSTM | Activity labels and confidence |
| Identity Recognition | Consent-based face embeddings | Known / unknown resident ID |
| Radar Processing | Device firmware output and tracking | Presence, position, velocity |
| Sensor Fusion | Temporal association and late fusion | Unified contextual observations |
| Next-State Prediction | Markov baseline / GRU | Future room and activity probabilities |

All model choices are provisional and will be evaluated before being finalized.

## Dataset Strategy

### Public Datasets

Potential datasets include:

- COCO Keypoints
- NTU RGB+D
- CASAS Smart Home datasets
- MM-Fi

Dataset selection will depend on the target task, data format, availability, and usage license.

### Local Experimental Data

Controlled experiments may be conducted with consenting participants under different conditions:

- Standing, walking, sitting, and lying
- Normal and low lighting
- Different observation angles
- Partial occlusion
- Camera-only and radar-assisted sensing

### Synthetic Behavioral Data

The household simulator will generate event histories for activity and room-transition prediction.

Synthetic data will be labeled explicitly and will not be presented as real-world observations.

## Research Experiments

### Experiment A — Vision Baseline

Evaluate pose and posture recognition accuracy and inference latency.

### Experiment B — Radar Sensing

Evaluate presence, target position, and motion observations from an affordable radar module.

### Experiment C — Sensor Fusion

Compare:

- Vision only
- Radar only
- Vision + Radar late fusion

### Experiment D — Household State Prediction

Compare simple probabilistic baselines and optional recurrent sequence models for next-room and next-activity prediction.

## Evaluation Metrics

- Precision, Recall, F1-score
- Per-class classification performance
- Room occupancy accuracy
- Position estimation error
- Tracking continuity and identity switches
- Model inference latency
- CPU/GPU/RAM usage
- Prediction accuracy and calibration
- Robustness to occlusion and sensor failures

## Proposed Structure

```text
src/
  perception/
  tracking/
  posture/
  activity/
  identity/
  audio/
  radar/
  fusion/
  prediction/
  event_publisher/

experiments/
  vision/
  radar/
  fusion/
  prediction/

datasets/
  README.md

configs/
models/
tests/
results/
```

## Privacy and Research Ethics

Sensitive audiovisual recordings must not be committed to public repositories.

Human data collection requires appropriate participant consent and restricted storage.

The system aims to generate semantic observations locally while limiting raw media exposure to the perception boundary.

Face recognition and speaker identification remain optional, consent-based extensions.

## Integration

This repository produces validated semantic events and prediction outputs for the main [ThinQ-Sense](https://github.com/HY-ThinQ-Sense/ThinQ-Sense) system.

The central orchestrator is responsible for appliance planning and execution decisions.

## Development Status

Research design and baseline implementation are in progress.

Results will be published with documented experimental settings, limitations, and reproducibility information.
