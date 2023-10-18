# AnimeFacesWithGAN
Building a GAN to generate anime faces.


In this repository, I am trying to improve the performance of the GAN model which was introduced here: https://jovian.com/aakashns/06b-anime-dcgan

I've created multiple versions and for each version, I have experimented over different approaches on training GAN's.

## v1

Version 1 is the exact notebook that was introduced on Jovian.
## Discriminator Network Architecture

The discriminator is a convolutional neural network designed for image classification in a Generative Adversarial Network (GAN) setup. It's responsible for distinguishing between real and generated images.

### Architecture Overview

- Input: 3-channel images of size 64x64 pixels.

### Layers

1. Convolutional Layer 1:
   - Number of Filters: 64
   - Kernel Size: 4x4
   - Stride: 2
   - Padding: 1
   - Activation: Leaky ReLU with a slope of 0.2
   - Batch Normalization

2. Convolutional Layer 2:
   - Number of Filters: 128
   - Kernel Size: 4x4
   - Stride: 2
   - Padding: 1
   - Activation: Leaky ReLU with a slope of 0.2
   - Batch Normalization

3. Convolutional Layer 3:
   - Number of Filters: 256
   - Kernel Size: 4x4
   - Stride: 2
   - Padding: 1
   - Activation: Leaky ReLU with a slope of 0.2
   - Batch Normalization

4. Convolutional Layer 4:
   - Number of Filters: 512
   - Kernel Size: 4x4
   - Stride: 2
   - Padding: 1
   - Activation: Leaky ReLU with a slope of 0.2
   - Batch Normalization

5. Convolutional Layer 5 (Output Layer):
   - Number of Filters: 1
   - Kernel Size: 4x4
   - Stride: 1
   - Padding: 0

### Output

- The output of the network is a single scalar value that represents the probability that the input image is a real image.

### Activation Function

- The final output is passed through a sigmoid activation function to produce a probability value in the range [0, 1].

### Network Output Size

- The output is a 1x1x1 tensor, which corresponds to a single scalar value.

This discriminator is a crucial component in a GAN and is trained to become increasingly better at distinguishing real images from fake ones during the training process.
