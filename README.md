# MRTA-Seg

MRTA-Seg is a temporal instance segmentation framework for surgical
instrument scenes. It is designed for endoscopic video, where adjacent frames
contain useful motion cues but also introduce blur, occlusion, and appearance
changes.

The framework combines a Res2Net encoder, a PAN-FPN feature pyramid, and a
motion reliability temporal alignment module. The temporal module aligns local
features from neighboring frames and injects a reliability gated residual into
the current frame representation. This allows the main spatial feature path to
remain stable while using temporal information when it is reliable.

The MRTA-C family further improves the prototype mask branch with multi-scale
feature fusion and edge-aware prototype refinement. MRTA-C++ extends this
design with an independent semantic auxiliary head during training. The
semantic branch is removed from inference, so the deployed model retains the
instance segmentation interface.

## Supported experiments

The experiments cover two surgical video datasets:

- EndoVis 2017
- PhaKIR

The repository includes training, evaluation, data preparation, external
baseline comparison, temporal clip handling, EMA checkpoints, and diagnostic
tools. Dataset files and pretrained weights are not redistributed here. Please
follow the corresponding dataset licenses and place them in the paths expected
by the experiment launchers.

## Repository layout

```text
InstanceSegmentation_EndoVis2017/   EndoVis 2017 training and evaluation
InstanceSegmentation_khakir/        PhaKIR training and evaluation
```

The model implementation is shared by the two dataset projects. The main
training and evaluation entry points are kept in each project directory so
that the dataset protocol and output paths remain explicit.

## Reproducibility

Experiments use video-level splits to avoid frame-level temporal leakage. The
training pipeline supports overlapping clips, synchronized clip augmentation,
EMA model weights, mixed precision, gradient accumulation, and numerical
finite-value checks. Reported comparisons should use the same dataset split,
clip protocol, input resolution, and checkpoint selection rule.

Detailed commands and environment requirements will be documented together
with the public release.

## Code release

The complete source code, configuration files, trained model definitions, and
reproduction instructions will be released after the associated paper has been
accepted for publication. The release will be updated with the final paper
version and the exact evaluation protocol.

## Questions and collaboration

We welcome questions, discussions, and research collaboration. For technical
questions or requests related to the experiments, please contact the first
author at **qlaa2012@163.com**, or open an issue after the public repository is
released.

## Citation

The citation entry will be added after publication. Until then, please cite the
associated manuscript and use the project name **MRTA-Seg** when referring to
this implementation.
