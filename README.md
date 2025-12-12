# LSTM Autoencoder on MNIST

This project implements an LSTM-based autoencoder for reconstructing MNIST images by treating each image as a sequence. Each 28×28 image is reshaped into **28 timesteps × 28 features**, enabling sequence-to-sequence learning.

During experiments, I verified that removing activation functions inside the model significantly improved the reconstruction quality. MNIST is a simple and almost linear dataset, so a linear autoencoder learns its structure effectively, while nonlinear activations introduce unnecessary complexity.


## Project Overview
This project explores how an LSTM autoencoder can learn to reconstruct MNIST digit images by treating each image as a temporal sequence. Instead of processing images spatially using convolutional layers, each 28×28 MNIST image is reshaped into **28 timesteps**, each containing **28 pixel values**. This allows the model to learn sequential dependencies that represent the visual structure of the digits.

## How the Autoencoder Works
The autoencoder consists of two main components:

### Encoder
The encoder receives a (28, 28) sequence and compresses it through stacked LSTM layers. Each layer extracts increasingly abstract temporal patterns. The final LSTM layer outputs a **64-dimensional latent vector** that represents a compact version of the image.

### Decoder
The decoder takes the latent vector and expands it back into a full sequence. To do this, the latent vector is repeated across 28 timesteps. This sequence is then passed through LSTM layers that gradually reconstruct the structure of the original digit. A final linear layer generates the pixel values for each timestep, producing a (28, 28) output image.

## Training Process
The model is trained using Mean Squared Error (MSE) loss between the original and reconstructed images. Since MNIST digits are simple and consistent, the LSTM autoencoder quickly learns to produce smooth and recognizable reconstructions.

## Experimental Verification
A key part of the project involved comparing different configurations of the model. I found that **removing activation functions inside the LSTM stack** led to significantly better reconstruction quality.

### Why this happens
- MNIST is a simple, highly structured, and almost **linear** dataset.
- Linear autoencoders behave similarly to **PCA**, which is well-suited for MNIST.
- Adding nonlinear activations (like ReLU) can introduce:
  - Saturation
  - Harder optimization
  - Dead neurons
  - Blurry outputs

Without activations, the model remains linear and can fit MNIST’s structure more effectively. This demonstrates the importance of aligning model complexity with dataset complexity.
