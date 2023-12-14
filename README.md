# AnimeFacesWithGAN
Building a GAN to generate anime faces.

In this repository, I tried to improve the performance of the GAN model which was introduced here: https://jovian.com/aakashns/06b-anime-dcgan

I've experimented over multiple versions and for each version, I have changed few settings to achieve a more stable training process and to avoid problems such as mode collapse and overfitting.
Sample Image From the Dataset|
:---:|
![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/sample.png)|

# v1
Version 1 is based on the notebook that was introduced on Jovian with my improvements on the training loop with keeping track of the training logs and creating useful charts to analyze the performance and stability of the Generator and the Discriminator models.

Step 0            |  Step 20          | Step 100
:-------------------------:|:-------------------------:|:-------------------------:
![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v1/generated/generated-images-0000.png)  |  ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v1/generated/generated-images-0020.png) | ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v1/generated/generated-images-0100.png)
# v2

Changes from v1: 
- Switched to LeakyReLU (from ReLU) on generator with the aim of achieving a stronger Generator model. However, that resulted into mode collapse so this change is reverted on the next experiments.

Step 40            |  Step 70          | Step 100
:-------------------------:|:-------------------------:|:-------------------------:
![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v2/generated/generated-images-0040.png)  |  ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v2/generated/generated-images-0020.png) | ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v2/generated/generated-images-0100.png)
# v3
  
Changes from v2: 
- Applied one-sided label smoothing to the Discriminator model: The idea of one-sided label smoothing is to replace the target for the real examples with a value slightly less than one, such as 0.9. This prevents extreme extrapolation behavior in the discriminator.
    — [NIPS 2016 Tutorial: Generative Adversarial Networks, 2016.](https://arxiv.org/abs/1701.00160) 

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
