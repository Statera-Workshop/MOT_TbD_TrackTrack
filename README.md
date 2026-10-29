# MOT_TbD_TrackTrack

**TrackTrack** - online multi-object tracking by detection on KITTI-MOTS: 25 detectors + the detections of FairMOT.

- Paper: Shim et al., CVPR 2025; official code: `kamkyu94/TrackTrack`
- Principle: track-perspective association (TPA) + track-aware initialisation (TAI)
- **(best)**: the best of the 10 trackers on that detector; last column = that best HOTA.
- Implementation: `common/mot/trackers.py` (`tracktrack`), re-implemented after the official code, official defaults
  (the class docstring lists every value and every `[Unified]` difference). Causality check: all OK.

### Results (TrackTrack, official defaults, KITTI-MOTS val)

| detector | HOTA | DetA | AssA | MOTA | IDF1 | IDSW | car | pedestrian | tracker ms | pipeline ms | best tracker on this detector |
|---|---|---|---|---|---|---|---|---|---|---|---|
| cascade_rcnn | **0.625** (best) | 0.563 | 0.698 | 0.624 | 0.750 | 48 | 0.691 | 0.560 | 3.26 | 40.7 | 0.625 |
| libra_rcnn | **0.599** (best) | 0.533 | 0.679 | 0.530 | 0.722 | 63 | 0.693 | 0.504 | 3.38 | 32.5 | 0.599 |
| faster_rcnn | **0.582** (best) | 0.521 | 0.656 | 0.573 | 0.726 | 53 | 0.680 | 0.485 | 3.35 | 31.1 | 0.582 |
| dynamic_rcnn | **0.579** (best) | 0.516 | 0.656 | 0.539 | 0.711 | 48 | 0.669 | 0.490 | 3.33 | 31.2 | 0.579 |
| retinanet | 0.530 | 0.461 | 0.613 | 0.525 | 0.683 | 27 | 0.612 | 0.448 | 3.27 | 28.2 | 0.535 |
| atss | **0.527** (best) | 0.452 | 0.618 | 0.505 | 0.667 | 26 | 0.624 | 0.430 | 3.57 | 42.8 | 0.527 |
| gfl | 0.516 | 0.439 | 0.607 | 0.492 | 0.638 | 19 | 0.607 | 0.424 | 3.22 | 27.3 | 0.522 |
| v6 | 0.500 | 0.430 | 0.584 | 0.499 | 0.638 | 29 | 0.625 | 0.374 | 3.22 | 14.1 | 0.509 |
| tood | 0.499 | 0.414 | 0.604 | 0.455 | 0.620 | 20 | 0.606 | 0.392 | 3.20 | 32.1 | 0.506 |
| fcos | 0.487 | 0.405 | 0.590 | 0.453 | 0.607 | 20 | 0.588 | 0.387 | 3.41 | 37.2 | 0.493 |
| ppyoloe | **0.487** (best) | 0.416 | 0.578 | 0.469 | 0.607 | 32 | 0.654 | 0.321 | 3.27 | 15.0 | 0.487 |
| deformable_detr | 0.480 | 0.402 | 0.576 | 0.466 | 0.631 | 24 | 0.567 | 0.393 | 3.15 | 74.7 | 0.482 |
| x | 0.468 | 0.387 | 0.571 | 0.447 | 0.602 | 31 | 0.615 | 0.321 | 3.15 | 11.6 | 0.478 |
| v9 | 0.452 | 0.365 | 0.566 | 0.412 | 0.555 | 15 | 0.599 | 0.305 | 3.11 | 17.1 | 0.460 |
| v10 | 0.450 | 0.373 | 0.547 | 0.433 | 0.581 | 22 | 0.575 | 0.326 | 3.11 | 13.7 | 0.455 |
| rtmdet | 0.440 | 0.356 | 0.550 | 0.409 | 0.562 | 9 | 0.594 | 0.287 | 3.18 | 13.0 | 0.465 |
| v11 | 0.430 | 0.336 | 0.560 | 0.378 | 0.523 | 19 | 0.596 | 0.264 | 3.09 | 12.0 | 0.435 |
| v8 | 0.426 | 0.339 | 0.544 | 0.386 | 0.526 | 21 | 0.591 | 0.262 | 3.10 | 11.0 | 0.443 |
| x2 | 0.425 | 0.341 | 0.531 | 0.386 | 0.536 | 19 | 0.576 | 0.273 | 3.19 | 14.0 | 0.452 |
| v12 | 0.397 | 0.305 | 0.525 | 0.346 | 0.477 | 12 | 0.568 | 0.226 | 3.07 | 14.4 | 0.424 |
| v1 | **0.374** (best) | 0.314 | 0.448 | 0.352 | 0.483 | 78 | 0.481 | 0.266 | 3.09 | 11.5 | 0.374 |
| v13 | **0.372** (best) | 0.284 | 0.526 | 0.323 | 0.435 | 16 | 0.577 | 0.167 | 3.08 | 16.3 | 0.372 |
| fairmot | 0.347 | 0.260 | 0.468 | 0.312 | 0.454 | 10 | 0.478 | 0.216 | 3.01 | 11.2 | 0.387 |
| centernet | 0.331 | 0.240 | 0.464 | 0.282 | 0.417 | 7 | 0.464 | 0.198 | 2.99 | 15.0 | 0.395 |
| v26 | 0.315 | 0.254 | 0.404 | 0.295 | 0.388 | 11 | 0.562 | 0.067 | 3.05 | 14.8 | 0.390 |
| ssd | 0.275 | 0.244 | 0.312 | 0.277 | 0.348 | 22 | 0.550 | 0.000 | 3.00 | 35.0 | 0.288 |

### Score-threshold sensitivity (TrackTrack, HOTA with one common threshold)

Not run for this tracker.

Part of the *Physical AI MOT* comparison of the **Statera Working Group**: 10 trackers x 25 detectors (+ the detections of FairMOT), 3 joint
detection-and-tracking networks and 1 end-to-end tracker under one protocol. The full comparison (Pareto front,
tracker ranking, JDT / E2E against tracking-by-detection) is in `MOT_Detectors_KITTIMOTS` (`RESULTS.md`).

## Protocol (all MOT_* repositories)

- Online / causal only: every method sees the current frame and its own state; checked by re-running prefixes of
  every sequence (the output of frame t must not change when later frames are removed).
- Input 1216 x 384 (KITTI 1242 x 375 letterboxed), detectors trained from scratch on KITTI-MOTS train (12 sequences),
  30 epochs, Adam 1e-4, effective batch 8, seed 777 - the protocol of the *Physical AI Object Detection* series.
- Metrics: HOTA / DetA / AssA (TrackEval classes, car / pedestrian mean), MOTA, IDF1, IDSW.
- Latency: RTX 4070 Laptop GPU, batch 1, fp32, medians over val; pipeline = detector (forward + post-processing) +
  ReID (appearance trackers) + tracker (CPU); image decoding / letterboxing not included.
- Trackers run with their official default parameters; frame-based values given for 30 fps are scaled to 10 fps.
  A sensitivity table with one common score threshold for every tracker is reported separately (chosen on val, so it
  is analysis, not ranking).

## Data: KITTI-MOTS (box level, val = 9 sequences, 2,981 frames)

KITTI tracking images (21 training sequences) with instance / track annotations; boxes = tight boxes of the masks,
classes car and pedestrian, ignore regions (id 10000) neither rewarded nor penalised. The annotations are taken from
the **KITTI-STEP** panoptic maps (same sequences and split, car / person instances merged from KITTI-MOTS; frames,
track counts and pedestrian masks match the KITTI-MOTS paper, car masks differ by 39 of 26,899).

```bash
bash tools/mot/get_kitti_mots.sh            # KITTI tracking images + annotations (KITTI-STEP fallback)
python tools/mot/kittimots_to_voc.py        # VOC-layout copy with tracks + count report
UNIFIED_IMAGE_DATASET=kittimots python tools/mot/count_loader.py     # counts as the loaders read them
```

**Licence of the data and of every trained weight here: KITTI / KITTI-MOTS / KITTI-STEP are CC BY-NC-SA 3.0
(non-commercial).**

## Usage

```bash
pip install -r requirements.txt
pip install "git+https://github.com/JonathonLuiten/TrackEval.git@12c8791b303e0a0b50f753af204249e622d0281a"
# saved detections (+ ReID features) of the 25 detectors: Release of Statera-Workshop/MOT_Detectors_KITTIMOTS
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --trackers tracktrack --causal
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --gt-as-pred      # evaluation self-test
python tools/mot/mot_table.py                                                             # tables of all runs
```

`run_tracker.py --trackers` accepts every tracker of the comparison (iou, sort, bytetrack, ocsort, hybridsort, botsort, botsort_reid, deepsort, tracktrack, fairmot), so other
trackers can be run on the same detections. Results of this repository: `results/` (JSON per detector).

## Files

```
common/mot/trackers.py    the trackers of the comparison (default here: tracktrack)
common/mot/core.py        boxes, IoU, assignment, Kalman filters, camera-motion estimation
common/mot/evaluate.py    KITTI-MOTS ground truth and TrackEval metrics
tools/mot/run_tracker.py  run / time / evaluate trackers on saved detections (+ causality check)
tools/mot/*kitti*         data preparation
results/                  evaluation JSON of this repository's tracker(s)
THIRD_PARTY.md            sources and licences
```

## Global Collaboration

Hills Robotics is currently participating in multiple projects in Korea and internationally.

We are actively interested in building relationships with organizations that can complement our technology with global sales networks, distribution channels, system integration capabilities, manufacturing ecosystems, AI infrastructure, robotics technologies, research capabilities, or strategic investment.

Several technology and business collaborations are already underway. Some partners, projects, system architectures, and commercial programs cannot be publicly disclosed because they are subject to confidentiality and business agreements.

We believe that the emerging Physical AI ecosystem cannot be built by a single company.
It requires a global network connecting robotics companies, AI researchers, semiconductor and computing companies, sensor manufacturers, software developers, universities, system integrators, industrial customers, investors, and global distribution partners.

We have now begun our serious exploration of the Physical AI frontier, and we welcome connections with people and organizations who want to build this ecosystem together.

## Research, Contribution, and Donation

The repositories of the Statera Working Group are intended to contribute to the broader technical discussion around Physical AI.

Researchers, engineers, developers, companies, universities, and independent contributors interested in these subjects are welcome to connect with us.

If you would like to collaborate on Physical AI or autonomous robotics, participate in research or technology development, discuss international business cooperation, propose technology or platform integration, contribute technical knowledge, or support this GitHub knowledge initiative through sponsorship or donation, please contact us.

## Contact

**Richard Minsoo Go**
Head of AI, Hills Robotics
Statera Working Group

Personal / Research Contact:
[gominsoo888@gmail.com](mailto:gominsoo888@gmail.com)

Hills Robotics / Business Contact:
[minsoo.go@hillslogis.com](mailto:minsoo.go@hillslogis.com)

Hills Robotics:
https://hillslogis.com/

For inquiries regarding next-generation outdoor autonomous robotic platforms, Physical AI Spider Grid, Intelligence Cabinet, Edge AI, or On-Premise AI architectures that are not yet publicly presented on the company website, please contact us directly.
