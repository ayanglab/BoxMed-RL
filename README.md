# Reason Like a Radiologist: Chain-of-Thought and Reinforcement Learning for Verifiable Report Generation

[![Paper Accepted](https://img.shields.io/badge/Journal-Medical%20Image%20Analysis-blue.svg?style=for-the-badge)](https://www.sciencedirect.com/science/article/pii/S1361841525004566)

## Overview

This repository hosts the official code for **BoxMed-RL**, a novel two-phase framework for automated chest X-ray report generation that unifies structured reasoning and spatially verifiable reinforcement learning.

Current report generation models often lack the **structured reasoning** of a radiologist and struggle to **explicitly ground findings** in anatomical evidence, limiting clinical trust and explainability. BoxMed-RL addresses these critical challenges by approximating the cognitive workflow of radiologists.

The paper, "**Reason Like a Radiologist: Chain-of-Thought and Reinforcement Learning for Verifiable Report Generation**," has been accepted for publication in *Medical Image Analysis*.

---

## Key Innovations (BoxMed-RL Framework)

The BoxMed-RL framework consists of two integrated phases to generate spatially verifiable and explainable reports:

1.  **Pretraining Phase:** Integrates two core modules:
    * **Medical Concept Learning (MCL):** Forces the model to internalize the diagnostic logic of radiologists through a hierarchical Chain-of-Thought (CoT) reasoning dataset. This bridges the gap between free-form generation and clinically structured workflows.
    * **Spatially Verifiable Reinforcement (SVR):** Explicitly aligns textual descriptions with anatomical regions using Intersection-over-Union (**IoU-based rewards**). This ensures that generated phrases correspond to pixel-level anatomical evidence, enforcing textual-visual alignment.
2.  **Downstream Adapter Phase:** A lightweight adapter is fine-tuned on raw reports while the pretrained weights are frozen. This step refines linguistic fluency and clinical phrasing, ensuring the final output is a fluent and coherent report while preserving the learned reasoning and alignment.



---

## Performance Highlights

BoxMed-RL demonstrates significant improvements over state-of-the-art methods on standard chest X-ray benchmarks.

* Achieves an average **7% improvement** in both **METEOR** and **ROUGE-L** natural language generation metrics.
* Shows an average **5% improvement** in large language model-based metrics, further underscoring its robustness in generating high-quality reports.
* Consistently outperforms state-of-the-art methods across language quality, clinical accuracy, and composite evaluation metrics.

---

## Citation
If you find this work useful for your research, please consider citing our paper:

```
@article{JING2026103910,
title = {Reason like a radiologist: Chain-of-thought and reinforcement learning for verifiable report generation},
journal = {Medical Image Analysis},
volume = {109},
pages = {103910},
year = {2026},
issn = {1361-8415},
doi = {https://doi.org/10.1016/j.media.2025.103910},
url = {https://www.sciencedirect.com/science/article/pii/S1361841525004566},
author = {Peiyuan Jing and Kinhei Lee and Zhenxuan Zhang and Huichi Zhou and Zhengqing Yuan and Zhifan Gao and Lei Zhu and Giorgos Papanastasiou and Yingying Fang and Guang Yang},
keywords = {Radiology report generation, Explainability, Reinforcement learning},
abstract = {Radiology report generation is critical for efficiency, but current models often lack the structured reasoning of experts and the ability to explicitly ground findings in anatomical evidence, which limits clinical trust and explainability. This paper introduces BoxMed-RL, a unified training framework to generate spatially verifiable and explainable chest X-ray reports. BoxMed-RL advances chest X-ray report generation through two integrated phases: (1) Pretraining Phase. BoxMed-RL learns radiologist-like reasoning through medical concept learning and enforces spatial grounding with reinforcement learning. (2) Downstream Adapter Phase. Pretrained weights are frozen while a lightweight adapter ensures fluency and clinical credibility. Experiments on two widely used public benchmarks (MIMIC-CXR and IU X-Ray) demonstrate that BoxMed-RL achieves an average 7 % improvement in both METEOR and ROUGE-L metrics compared to state-of-the-art methods. An average 5 % improvement in large language model-based metrics further underscores BoxMed-RL’s robustness in generating high-quality reports. Related code and training templates are publicly available at https://github.com/ayanglab/BoxMed-RL.}
}
```
