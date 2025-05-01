# Super-Resolution with Diffusion-GAN Hybrid

![License: All Rights Reserved](https://img.shields.io/badge/license-All--Rights--Reserved-red.svg)

This project implements a hybrid super-resolution architecture that combines a UNet-based diffusion model with a GAN enhanced by wavelet feature extraction and residual refinement. The model is trained for high-fidelity image super-resolution on the DIV2K dataset.

---

## 🧠 Architecture Overview

**CombinedGenerator** = `DiffusionGenerator` → `Wavelet+Residual GAN Generator`

- **DiffusionGenerator**: Uses a UNet denoiser with self-attention and sinusoidal time embedding. Runs partial denoising steps (25/100) for efficient refinement.
- **GAN Generator**: Applies wavelet-based feature extraction, deep residual blocks, and upsampling layers to produce sharp HR outputs.
- **Discriminator**: A PatchGAN-style model with spectral normalization, trained using a combination of real/fake adversarial losses.

---

## 📦 Components

- `WaveletBlock`: Extracts high-frequency wavelet features (Haar) for texture preservation.
- `ResBlock`: Standard residual blocks with batch normalization.
- `UNetDenoiser`: Time-aware encoder–decoder for diffusion denoising.
- `CombinedGenerator`: Sequentially applies diffusion then GAN stages.
- `PatchGAN Discriminator`: Spectrally-normalized conv net for adversarial training.

---

## 🔧 Losses Used

- **Diffusion**: L1 + optional BCEWithLogitsLoss (if predicting noise mask).
- **Generator**: Combination of pixel loss, adversarial loss, perceptual loss (if used), and wavelet loss.
- **Discriminator**: `BCEWithLogitsLoss` for real/fake classification.

---

## 🖼️ Results

- The hybrid design improves both **fine details** and **structural coherence**.
- Diffusion stage aids in global structure refinement; GAN sharpens edges and textures.

---

## 🧪 Dataset

- **DIV2K** for training and evaluation.
- Input: LR images
- Output: Super-resolved HR images (typically 4× scale)

---

## 🚀 Training

You can train the model using your custom loop with multi-loss support. The model is designed to scale on 2× T4 GPUs using PyTorch.

---

## License

This repository is strictly **All Rights Reserved**.

You may not use, copy, modify, distribute, or reproduce any part of this codebase without **explicit written permission** from the author.

© 2025 **Lakshit Kumawat** (lakshitkumawat16@gmail.com). All rights reserved.
