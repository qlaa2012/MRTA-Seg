# MRTA-Seg

MRTA-Seg is a temporal instance segmentation framework for surgical
instrument scenes. It is designed for endoscopic video, where adjacent frames
contain useful motion cues but also introduce blur, occlusion, and appearance
changes.

## Overview

The framework combines a Res2Net encoder, a PAN-FPN feature pyramid, and a
motion reliability temporal alignment module. The temporal module aligns local
features from neighboring frames and injects a reliability gated residual into
the current frame representation. This allows the main spatial feature path to
remain stable while using temporal information when it is reliable.

The complete model described in the manuscript is MRTA-Seg, whose branch-aware
deployment configuration is denoted as MRTA-C. The main components are:

- **Motion Reliability Temporal Alignment (MRTA):** aligns neighboring-frame
  features and gates temporal residuals according to their reliability.
- **MRTA-C:** applies MRTA to shared P3/P4 multiscale features and to the
  mask-coefficient pathway at P3/P4/P5, while adding a lightweight prototype
  edge residual. This branch-aware deployment preserves the current-frame main
  path and the original prototype-coefficient instance-segmentation
  formulation.

## Supported experiments

The experiments cover two surgical video datasets:

- EndoVis 2017
- PhaKIR

The repository includes training, evaluation, data preparation, external
baseline comparison, temporal clip handling, EMA checkpoints, and diagnostic
tools.

The experiments use publicly available datasets for endoscopic surgical
instrument segmentation. The datasets are not redistributed in this
repository. Users should obtain them from their original sources and comply
with the corresponding licenses and terms of use.

PhaKIR is a restricted-access dataset. Users must register and sign in to
Zenodo, submit the dataset provider's access request form, and wait for the
request to be reviewed and approved. PhaKIR is distributed under the
provider-specified **CC BY-NC-SA 4.0** terms, together with any additional
access conditions stated by the provider. The dataset files are not
redistributed in this repository, and all resulting works that use PhaKIR in
whole or in part must cite the publications designated by the dataset
provider.

The EndoVis 2017 data used in our experiments were obtained through the
[corresponding Kaggle dataset page](https://www.kaggle.com/datasets/ljhstaunch/endovis2017).
Users should consult that page and the original EndoVis challenge or
data-provider documentation before downloading the data. The Kaggle listing
does not specify a separate dataset license, so users must not infer
redistribution rights from the listing alone. Use and redistribution must
comply with the applicable Kaggle terms, the original dataset terms, and any
challenge citation requirements.

## Repository layout

```text
InstanceSegmentation_EndoVis2017/   EndoVis 2017 training and evaluation
InstanceSegmentation_khakir/        PhaKIR training and evaluation
```

The model implementation is shared by the two dataset projects. The main
training and evaluation entry points are kept in each project directory so
that the dataset protocol and output paths remain explicit.

## Repository status

The accompanying manuscript is currently under review. This repository
provides an overview of MRTA-Seg and its experimental setting. To preserve the
review and publication process, the complete release package will be finalized
after the manuscript has been accepted.

Following acceptance, we intend to release the materials required to reproduce
the reported experiments, including:

- model architecture and module implementations;
- training and inference scripts;
- evaluation and metric-calculation code;
- experiment configurations and split information; and
- MRTA-Seg pretrained checkpoints, subject to repository storage limits.

Our own pretrained model weights are model artifacts and do not redistribute
the datasets. They can therefore be provided with the public implementation,
whereas the original dataset files remain the responsibility of the dataset
providers.

## Reproducibility

Experiments use video-level splits to avoid frame-level temporal leakage. The
training pipeline supports overlapping clips, synchronized clip augmentation,
EMA model weights, mixed precision, gradient accumulation, and numerical
finite-value checks. Reported comparisons should use the same dataset split,
clip protocol, input resolution, and checkpoint selection rule.

Detailed commands, environment requirements, and the final evaluation
protocol will be documented together with the public release.

## Questions and collaboration

We welcome questions, discussions, and research collaboration. For technical
questions or requests related to the experiments, please contact the first
author at **qlaa2012@163.com**, or open an issue after the public repository is
released.

## Citation

The citation entry will be added after publication. Until then, please cite the
associated manuscript and use the project name **MRTA-Seg** when referring to
this implementation.

## License

The license for the source code and released materials will be specified when
the public implementation is finalized. Dataset licenses and terms of use are
separate and continue to be governed by the original dataset providers.
