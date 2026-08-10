# Face Parsing using U-Net

> [!IMPORTANT]
> ## Academic Integrity
>
> This repository contains my implementation and work for an academic
> course project at NTU Singapore.
>
> If you use any ideas, code, or material from this repository in an
> academic submission, please provide appropriate attribution and citations
> as required by the course, instructor, and institution.
>
> **NTU's Academic Integrity and Plagiarism Rules must be strictly followed.**
> I do not permit this repository to be submitted, in whole or in part, as
> another student's original work.
>
> Users are solely responsible for ensuring that their use of this
> repository complies with NTU's academic-integrity and plagiarism
> requirements. I will not be held responsible for any academic-integrity
> or plagiarism violations resulting from the use or misuse of this
> repository.

# Face Parsing using U-Net

## Overview

This project implements a U-Net-based semantic segmentation model for
19-class face parsing using a subset of the CelebAMask-HQ dataset.

This project was completed as part of an NTU course and was evaluated
through a Codabench challenge.

The project focuses on evaluating different architectural and training
choices under a fixed parameter budget of 1.82M.

## Dataset

CelebAMask-HQ was used for face parsing.

- Training images: 1,000
- Validation images: 100
- Image size: 512 × 512
- Classes: 19
- Input: RGB images
- Target: Single-channel segmentation masks

## Model

A U-Net architecture was used for pixel-level face parsing.

Various configurations were evaluated including loss function, decoder design (upsampling method), normalization, data augmentations, learning rate scheduling and dropout. The following choices were made based on the experiments for the final model

- Loss function : Cross Entropy + Dice Loss
- Upsampling : Bilinear Upsampling (Instead of Transpose Convolution)
- Normalization : Dataset Mean and Standard Deviation (Instead of 0.5 as Mean and Standard Deviations)
- Data augmentation : RandomCropResize + Color Jitter + RandomGrayscale + GaussianBlur + RandomAdjustSharpness
- Optimizer : Adam
- Learning-rate scheduling : Cosine Annealing
- Learning Rate : 6e-4 (Starting), 1e-5 (Minimum)
- Epochs : 250
- Batch Size : 8
- Feature-map scaling : [16, 32, 64, 128, 192] 
- Dropout : p = 0.2 at bottleneck layer

The final architecture was constrained to a parameter budget of
approximately 1.82M parameters.

## Experimental Results


## Final Model Results

The final model achieved:

- **F1 Score (Validation):** 83.3%
- **F1 Score (Training):** 87.73%
- **Pixel Accuracy (Training):** 96.38%
- **Parameter count:** ~1.81M
- **Parameter budget:** 1.82M