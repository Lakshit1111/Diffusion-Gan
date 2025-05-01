🧠 Super-Resolution with Diffusion-GAN Hybrid and Wavelet Attention
This repository implements a hybrid super-resolution model that combines the strengths of denoising diffusion models, wavelet-based attention, and GAN-based upsampling for high-fidelity image restoration.

🧱 Architecture Overview
1. Combined Generator
The CombinedGenerator is composed of two stages:

DiffusionGenerator: Uses a UNet-based denoiser trained to progressively reverse a noise process, refining the structure and content of the low-resolution input.

GAN Generator: A wavelet-enhanced upsampling network that learns residual mappings and performs two-stage upsampling with sharpening and feature fusion.

2. WaveletBlock
A module that applies a discrete wavelet transform (DWT) to extract high-frequency details, followed by a 1×1 convolution to project these features into the feature space.

3. UNetDenoiser
A UNet architecture with:

Sinusoidal time embeddings

Residual convolutional blocks with instance normalization

Self-attention at the bottleneck layer This module denoises inputs at different timesteps during diffusion inference.

4. PatchGAN Discriminator
A spectral-normalized PatchGAN that returns both a real/fake prediction map and intermediate feature activations to support feature matching loss for stable GAN training.

🧪 Loss Functions
Adversarial Loss (LSGAN): Stabilizes GAN training using least squares.

Feature Matching Loss: Encourages the generator to match discriminator feature statistics, improving perceptual quality.

Optional Auxiliary Losses (not shown but easily extendable):

Perceptual loss (e.g., VGG-based)

Edge or TV loss

Wavelet-domain losses

📦 Components
Module	Description
WaveletBlock	Extracts high-frequency detail via Haar DWT
ResBlock	Standard residual block with BatchNorm
Generator	Two-stage upsampling with wavelet-enhanced residual learning
Discriminator	PatchGAN with spectral norm + feature return support
UNetDenoiser	Time-aware UNet for denoising diffusion inference
DiffusionGenerator	Wraps UNetDenoiser to iteratively denoise images
CombinedGenerator	Pipeline of Diffusion → GAN Generator
