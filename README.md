<div align="center">

# Decoding Children's Gait Behavior

**Fine-grained analysis of children's gait from standard RGB video**

### ECCV 2026

[![Conference](https://img.shields.io/badge/ECCV-2026-1A4E8A)](https://pediamedai.github.io/ChildrenGait/)
[![Project Page](https://img.shields.io/badge/Project-Page-1A4E8A)](https://pediamedai.github.io/ChildrenGait/)
[![arXiv](https://img.shields.io/badge/arXiv-coming%20soon-CB2F10)](https://arxiv.org/abs/ARXIV_ID)
[![Dataset](https://img.shields.io/badge/Hugging%20Face-Dataset-FFD21E?logo=huggingface&logoColor=000)](https://huggingface.co/datasets/PediaMedAI/ChildrenGait)
[![License: CC BY-NC 4.0](https://img.shields.io/badge/Data%20License-CC%20BY--NC%204.0-lightgrey)](https://creativecommons.org/licenses/by-nc/4.0/)

Yifan Shen<sup>1,2,&ast;</sup>,
Boyi Li<sup>1,&ast;</sup>,
Meihuan Huang<sup>2,3,4,&ast;</sup>,
Yuanzhe Liu<sup>1,&ast;</sup>,
Xu Cao<sup>1,2,&ast;,§</sup>,
Jinyang Jin<sup>1</sup>,
Zhengyuan Li<sup>1</sup>,
Anglin Liu<sup>5</sup>,
Junho Kim<sup>1</sup>,
Jingyuan Zhu<sup>2</sup>,
Fangzhou Lan<sup>2</sup>,
Jianguo Cao<sup>2,3</sup>,
Jintai Chen<sup>5</sup>,
Ismini Lourentzou<sup>1</sup>,
James M. Rehg<sup>1,†</sup>

<sup>1</sup> University of Illinois Urbana-Champaign &nbsp;
<sup>2</sup> PediaMed AI &nbsp;
<sup>3</sup> Shenzhen Children's Hospital <br>
<sup>4</sup> Hong Kong Polytechnic University &nbsp;
<sup>5</sup> The Hong Kong University of Science and Technology (Guangzhou)

<sub><sup>&ast;</sup>Equal contribution &nbsp; <sup>§</sup>Project lead &nbsp; <sup>†</sup>Corresponding author</sub>

</div>

---

## Overview

We introduce a new problem domain for human action recognition: the **fine-grained analysis of children's gait behaviors from standard RGB video**, targeting the ambulatory patterns of children aged **3–17 years**. Such behaviors arise naturally in the diagnosis and treatment of critical developmental and neuromuscular disorders, such as cerebral palsy and hemiplegia. Current 3D sensor-based gait analysis systems are expensive, intrusive, and often impractical for young subjects.

To address this, we release the **Children Gait Video (CGV)** dataset — over 1,100 high-frame-rate (60 FPS) video sequences from 110 subjects with synchronized, anonymized pose sequences. We show that current state-of-the-art gait foundation models and Multimodal Large Language Models (MLLMs) **fail to resolve these clinical nuances**, and we present **ChildGait-Video**, a unified end-to-end framework for decoding the fundamental components of pediatric gait.

## Abstract

> We introduce a new problem domain for human action recognition: the fine-grained analysis of children's gait behaviors from standard RGB video. We specifically target the ambulatory patterns of children aged 3–17 years. Such behaviors arise naturally in the diagnosis and treatment of several critical developmental and neuromuscular disorders, such as cerebral palsy and hemiplegia. Despite their clinical value, current 3D sensor-based gait analysis systems are expensive, intrusive, and often impractical for young subjects. To address this, we introduce a new dataset comprising over 1,100 high-frame-rate (60 FPS) video sequences from 110 subjects, accompanied by synchronized, anonymized pose sequences. In each session, the child performs a 5-second "walk-around" task, capturing the gait cycle from multiple viewpoints. Crucially, we demonstrate that current state-of-the-art approaches, including gait foundation models and Multimodal Large Language Models (MLLMs), fail to effectively resolve these clinical nuances. We identify the key technical challenges in analyzing these erratic and subtle motor patterns and describe a unified end-to-end framework for decoding fundamental components of pediatric gait. Through comprehensive experimental results, we demonstrate the potential of this dataset to drive novel research questions and establish a rigorous baseline for automated child gait assessment.

## Contributions

1. **Children Gait Video (CGV) dataset** — the largest repository of multi-camera gait videos of children with developmental motor conditions, containing both clinically relevant assessments (EVGS and GVS) and rich frame-level annotations.
2. **Benchmarking SoTA VLMs** — the first comprehensive assessment of open and closed VLMs on decoding subtle signs of gait abnormalities from video; out-of-the-box models are ineffective for this task.
3. **ChildGait-Video** — a novel video analysis method, the current SoTA for automated inference of EVGS and GVS scores from children's videos.

## The CGV Dataset

| Pediatric patients | Videos | Frames (2K) | EVGS items / subject | Age range |
|:------------------:|:------:|:-----------:|:--------------------:|:---------:|
| 110 | 1,185 | 339,236 | 2 × 17 | 3–17 yrs |

- **Capture.** A primary camera at the end of an 8-meter walkway records the **coronal** (frontal & posterior) view; an orthogonal secondary camera captures the **sagittal** (lateral) view, calibrated to cover 2–3 complete gait cycles. Each child performs a brief 3–5 second walk at high frame rate.
- **Annotation.** Bounding boxes and instance masks via **SAM 3** (human-verified), 2D keypoints via **Sapiens-2B** (manually refined), and **17 EVGS sub-items per limb** graded by an expert pediatrician and reviewed by a senior pediatrician with 40 years of clinical experience.
- **Labels.** The 3-point EVGS ordinal scale (0/1/2) is **binarized** into "typical" vs. "atypical" to build a robust benchmark over all 34 bilateral items.
- **Privacy.** Irreversible de-identification (RetinaFace + SAM 3 mosaic on all identifiable regions), released under a tiered access strategy.

## Method: ChildGait-Video

A two-stage adaptation paradigm built on the **VideoMAE v2** encoder (pre-trained on Kinetics-710, fine-tuned on CGV):

- **Token-Level Kinematic Prompting** — joint coordinates and their connectivity graph are rendered onto each RGB frame so that, after patchification, the skeleton patches act as kinematic prompts injecting anatomical priors of the developing body.
- **Mask-Guided Patch Pruning** — binary instance masks keep only foreground patches, focusing self-attention on the subject's gait and cutting fine-tuning cost.

**Result:** ChildGait-Video achieves **SoTA across all baselines**, reaching a **70%–93%** accuracy range over all 34 scoring items (average gains of **+15% / +12%** on the left / right limbs over fine-tuned VideoMAE v2, average **F1 = 0.83**).

## CVPR 2026 Workshop: Computer Vision for Children (CV4CHL)

This work is part of our broader effort to advance computer vision for pediatric health. At **CVPR 2026**, we organized the **Workshop on Computer Vision for Children (CV4CHL)**, which hosted **The 1st AI Children Challenge** — bringing the community together to build and benchmark vision systems for children-centered tasks.

- 🌐 Workshop page: **https://pediamedai.com/cv4chl/**
- 📄 Challenge report: **[The 1st AI Children Challenge (CVPRW 2026)](https://openaccess.thecvf.com/content/CVPR2026W/CV4CHL/papers/Li_The_1st_AI_Children_Challenge_CVPRW_2026_paper.pdf)**

## Citation

If you find this work useful, please cite our paper and the CV4CHL challenge:

```bibtex
@article{shen2026decoding,
    title   = {Decoding Children's Gait Behavior},
    author  = {Shen, Yifan and Li, Boyi and Huang, Meihuan and Liu, Yuanzhe and Cao, Xu and Jin, Jinyang and Li, Zhengyuan and Liu, Anglin and Kim, Junho and Zhu, Jingyuan and Lan, Fangzhou and Cao, Jianguo and Chen, Jintai and Lourentzou, Ismini and Rehg, James M.},
    journal = {arXiv preprint arXiv:XXXX.XXXXX},
    year    = {2026}
}

@inproceedings{li20261st,
    title     = {The 1st AI Children Challenge},
    author    = {Li, Boyi and Shen, Yifan and Yang, Houze and Cao, Xu and Yun, Guojun and Gao, Li and Chen, Turong and Xu, Long and Cao, Jianguo and Huang, Meihuan},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
    pages     = {5564--5570},
    year      = {2026}
}
```
