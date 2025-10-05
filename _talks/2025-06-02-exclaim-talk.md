---
title: "Comparing rollout methods in autoregressive models"
collection: talks
type: "Talk"
permalink: /talks/exclaim2025
venue: "EXCLAIM 2025, ETH Zürich"
date: 2025-06-02
location: "Zürich, Switzerland"
---

Physics-based numerical weather simulations repeatedly integrate a system of equations and propagate the fields over time. Numerical stability constraints these global models to run with timesteps on the order of seconds to minutes, but they can be propagated for long roll-outs while maintaining physical consistency. In contrast, data-driven models often propagate hours or days per step. Since these models lack physical constraints, each pass through the model introduces errors that accumulate. This limits the accuracy of such models beyond about one week of rollout for state-of-the-art models. This is problematic, since the medium-range weather forecast is invaluable to operational weather services.

Recently published models have tackled this issue with varying methods: Graphcast trains with an autoregressive training curriculum, increasing the fine-tuned rollout to 12 days; Pangu-Weather trains four models with different lead times and stacks them upon inference. Both approaches are computationally expensive; during training, Graphcast backpropagates through time and heavily utilizes gradient checkpointing to fit this many steps in memory, and Pangu-Weather simply trains four separate---and expensive---models.

Many data-driven models use an encoder--processor--decoder structure; the encoder/decoder maps between physical and latent spaces, and the processor advances the latent state by one time step. We propose a training scheme that selects a random number of rollout steps in the processor at each step. This constrains the processor to handle the time propagation and restricts the encoder/decoder to map between the physical and latent spaces.
Our study compares three rollout methods in two Transformer-based architectures. The rollout methods are: stacking models trained for different lead times, step-wise fine-tuning for increasingly longer  rollouts, and training with randomized rollout in the latent space. These methods are evaluated for performance, memory requirements, energy consumption, and training time. Preliminary results indicate that randomizing rollout length yields better predictions than a fixed-lead-time model, drastically reducing the computational cost of training. 
Minimizing the number of encoder/decoder passes in long rollouts allows models to accumulate less error and have improved stability. Our study provides insight into how error accumulation in data-driven autoregressive models behaves, paving the way to medium-range and even subseasonal forecasting.