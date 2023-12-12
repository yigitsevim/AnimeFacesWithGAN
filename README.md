# AnimeFacesWithGAN
Building a GAN to generate anime faces.

In this repository, I tried to improve the performance of the GAN model which was introduced here: https://jovian.com/aakashns/06b-anime-dcgan

I've experimented over multiple versions and for each version, I have changed few settings to achieve a more stable training process and to avoid problems such as mode collapse and overfitting.

# v1
Version 1 is based on the notebook that was introduced on Jovian with my improvements on the training loop with keeping track of the training logs and creating useful charts to analyze the performance of the models.

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

## Generator Network Architecture

The generator is a convolutional neural network responsible for generating images in a Generative Adversarial Network (GAN) setup. It takes random noise (latent vectors) as input and generates images.

### Architecture Overview

- Input: Latent vector of size `latent_size x 1 x 1`.

### Layers

1. Transposed Convolution Layer 1:
   - Number of Filters: 512
   - Kernel Size: 4x4
   - Stride: 1
   - Padding: 0
   - Activation: Leaky ReLU with a slope of 0.2
   - Batch Normalization

2. Transposed Convolution Layer 2:
   - Number of Filters: 256
   - Kernel Size: 4x4
   - Stride: 2
   - Padding: 1
   - Activation: Leaky ReLU with a slope of 0.2
   - Batch Normalization

3. Transposed Convolution Layer 3:
   - Number of Filters: 128
   - Kernel Size: 4x4
   - Stride: 2
   - Padding: 1
   - Activation: Leaky ReLU with a slope of 0.2
   - Batch Normalization

4. Transposed Convolution Layer 4:
   - Number of Filters: 64
   - Kernel Size: 4x4
   - Stride: 2
   - Padding: 1
   - Activation: Leaky ReLU with a slope of 0.2
   - Batch Normalization

5. Transposed Convolution Layer 5 (Output Layer):
   - Number of Filters: 3
   - Kernel Size: 4x4
   - Stride: 2
   - Padding: 1
   - Activation: Tanh

### Output

- The output of the network is a color image with 3 channels and a size of 64x64 pixels.

### Activation Function

- The final output is passed through a hyperbolic tangent (Tanh) activation function to ensure pixel values are in the range [-1, 1].

### Network Output Size

- The output of the generator is a 3x64x64 tensor, representing the generated image.

The generator plays a key role in the GAN framework by learning to create realistic images from random noise, with the goal of fooling the discriminator.

# v2

Changes from v1: 
- Switched to LeakyReLU (from ReLU) on generator. Kept LeakyReLU for the rest of the versions.

# v3
  
Changes from v2: 
- Updated Discriminator Gradients only if Loss_d > Threshold (0.2). 

# v4.1

Changes from v3: 
- Decreased the discriminator loss treshold to 0.1 from 0.2.

# v4.2

Changes from v3: 
- Increased the discriminator loss treshold to 0.3 from 0.2.

# v4.3

Changes from v3: 
- Discriminator Loss threshold is set to 0.2,
- Updated Generator gradients only if Loss_g > Threshold (4.0).
