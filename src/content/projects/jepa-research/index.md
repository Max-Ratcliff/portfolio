---
title: "Neuromorphic Computing Research (JEPA)"
description: "Aligning Spiking Neural Networks with biological latent manifolds using Joint-Embedding Predictive Architectures."
date: "Jan 10 2026"
demoURL: ""
repoURL: ""
---

This research project explores a novel approach to understanding neural population codes, which often change dramatically across brain states (active vs. passive), causing traditional decoders to fail. My team and I proposed a solution using **Joint-Embedding Predictive Architectures (JEPA)** to discover "ground truth" latent dynamics from real neural recordings while filtering out noise. We then test whether biologically-constrained **Spiking Neural Networks (SNNs)** can implement these same computations.

### The Research Problem
A major challenge in neuroscience is that we don't fully understand the underlying circuit mechanisms driving shifts in neural population codes. While deep learning models achieve high decoding accuracy, they often lack interpretability. By using SNNs—which are inherently more interpretable—we can test whether imposed biological constraints are sufficient for the computations that JEPA discovers.

### Methodology: A Two-Phase Approach
Our approach, which we are currently implementing using the **Allen Institute Neuropixels Visual Behavior** dataset (200,000 neurons), is divided into two main phases:

1.  **Teacher Model (Phase 1):** We train a **LeJEPA** model on binned spike data (10ms) to predict future latent states. This allows the model to discover the essential latent dynamics of the mouse visual cortex without representational collapse.
2.  **Student Model (Phase 2):** We "distill" these learned dynamics into a bio-constrained SNN. Using **snntorch** and **Leaky Integrate-and-Fire (LIF)** neurons, we match the teacher's latent representations via **Rotationally-invariant Canonical Correlation Analysis (CCA)**.

### Biological Constraints & Success Metrics
To ensure biological plausibility, we implement several constraints:
- **Homeostatic Firing Rate Penalty:** Keeps mean firing rates in the 5-20Hz biological range.
- **Surrogate Gradient Methods:** Enables backpropagation through discrete spikes.
- **Dale's Principle:** Distinguishing between excitatory and inhibitory populations to study E/I balance.

We define success by achieving a CCA similarity of >0.7 between the SNN and JEPA latents while maintaining stable, biologically accurate firing patterns. 

### Current Status
We have successfully completed **Phase 0 (Data Pipeline & Infrastructure)**, including the implementation of spike binning and data quality validation. We are now moving into the training phase for the LeJEPA baseline, with the ultimate goal of publishing our findings over the next two quarters.

### Credits
This research is a collaborative effort by:
- **Max Ratcliff**
- **Yul Hui Han**
- **Jacob Poschl**
