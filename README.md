Model's architecture is absolutly the same as in the article https://arxiv.org/abs/1606.03657 

# InfoGAN (PyTorch Implementation)

Implementation of **InfoGAN** from the paper:

**InfoGAN: Interpretable Representation Learning by Information Maximizing Generative Adversarial Nets**  
Xi Chen et al., 2016

The goal of InfoGAN is to learn **disentangled and interpretable latent representations** in a fully unsupervised setting by maximizing mutual information between latent codes and generated samples.

# Overview

This repository contains a PyTorch implementation of:

- **InfoGAN architecture**
  - Generator
  - Discriminator
  - Auxiliary Q-network for mutual information maximization
- **Vanilla GAN baseline** for comparison
- **Quantitative and qualitative evaluation**

The experiments are conducted on the **MNIST handwritten digit dataset**.

The project demonstrates how mutual information maximization enables the generator to learn interpretable latent factors without labels.

# Method

The latent input vector is composed of three parts:

- **z** — random noise sampled from a normal distribution  
- **c_cat** — categorical latent code representing discrete factors (digit identity)  
- **c_cont** — continuous latent codes representing smooth variations (style, stroke thickness)

To maximize mutual information between the latent code and generated samples, InfoGAN introduces an auxiliary **Q-network** that predicts the latent variables from generated images.

Objective:
I(c ; G(z, c))

This encourages the generator to produce samples where specific latent variables control interpretable attributes.

# Architecture

Generator:
- Fully connected layers
- Deconvolutional layers

Discriminator:
- Convolutional network
- Real / fake classification

Q-network:
- Shares features with the discriminator
- Predicts categorical and continuous latent codes

Hyperparameters:

- z ~ N(0,1), size 62
- c_cat — 10 categories
- c_cont — 2 continuous latent variables
- Full vector: 74
- Generator and discriminator as DCGAN
- The Q-network is built on top of the discriminator, as in the article
- β1 = 0.5, lr = 2e−4 — as in DCGAN/InfoGAN
- λ_MI = 1.0 — as in the appendix to the article

# Dataset

Experiments are performed on **MNIST**:

- 60,000 training images
- grayscale images
- resolution: 28×28
- normalized to [-1, 1]

Training is **fully unsupervised** (labels are not used during training).

# Evaluation

Two types of evaluation were performed.

### Quantitative metrics

| Metric | Description |
|------|------|
| Category Consistency Accuracy | Measures how well the categorical latent code controls digit identity |
| Macro F1-score | Balanced evaluation across digit classes |
| FID (optional) | Measures realism and diversity of generated samples |

Results:

| Model | Accuracy | Macro F1 |
|------|------|------|
| Vanilla GAN | ~0.10 | ~0.10 |
| InfoGAN | ~0.78 | ~0.73 |

InfoGAN significantly improves alignment between latent variables and generated digit identity.

### Qualitative evaluation

Latent traversal experiments demonstrate disentanglement:

- **categorical code** controls digit identity
- **continuous codes** control style variations such as stroke thickness and rotation





