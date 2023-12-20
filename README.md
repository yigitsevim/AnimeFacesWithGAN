# AnimeFacesWithGAN
Building a GAN to generate anime faces.

In this repository, I tried to improve the performance of the GAN model which was introduced here: https://jovian.com/aakashns/06b-anime-dcgan

I've experimented over multiple versions and for each version, I have changed few settings to achieve a more stable training process and to avoid problems such as mode collapse and overfitting.

*Generative adversarial networks lack an objective function, which makes it difficult to compare performance of different models. One intuitive metric of performance can be obtained by having human annotators judge the visual quality of samples.* - [Improved Techniques for Training GANs, 2016.](https://arxiv.org/abs/1606.03498)

Sample Batch From the Dataset|
:---:|
![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/sample.png)|

# v1 (DCGAN up to v6)
Version 1 is based on the notebook that was introduced on Jovian with my improvements on the training loop with keeping track of the training logs and creating useful charts to analyze the performance and stability of the Generator and the Discriminator models.

| Step 100 Image |
|:--------------:|
| ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v1/generated/generated-images-0100.png) |

| Score Plot | Loss Plot |
|:----------:|:----------:|
| ![Score Plot](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/b62e8c9d-a7f5-4b19-8ada-3bbfa72ee2d4) | ![Loss Plot](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/e3ed3fe8-7252-4769-b318-cc


# v2

Changes from v1: 
- Switched to LeakyReLU (from ReLU) on generator with the aim of achieving a stronger Generator model. However, that resulted into mode collapse so this change is reverted on the next experiments.

Step 40            |  Step 100          | Score Plot
:-------------------------:|:-------------------------:|:-------------------------:
![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v2/generated/generated-images-0040.png)  |  ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v2/generated/generated-images-0100.png) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/5f757d9c-1697-4de3-a97d-82a661e21747)


# v3
  
Changes from v2: 
- Reverted back to ReLU for the Generator.
- Applied one-sided label smoothing to the Discriminator network: *The idea of one-sided label smoothing is to replace the target for the real examples with a value slightly less than one, such as 0.9. This prevents extreme extrapolation behavior in the discriminator.* - [NIPS 2016 Tutorial: Generative Adversarial Networks, 2016.](https://arxiv.org/abs/1701.00160) 

 Step 100| Score Plot | Loss Plot
:-------------------------:|:-------------------------:|:-------------------------:
![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v3/generated/generated-images-0100.png) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/d281a32a-295c-4547-9936-e2313c38d8bc) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/581b0ee0-1637-47b4-95d6-2ae178559b98)


# v4

Changes from v3: 
- Label smoothing is applied to both Generator and Discriminator networks. Smoothing value is selected uniform randomly between 0 - 0.2.

 Step 100| Score Plot | Loss Plot
:-------------------------:|:-------------------------:|:-------------------------:
![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v4/generated/generated-images-0100.png) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/ac066e5f-1702-49fc-9c12-75a8c7f9519a) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/f65f81dc-dcd6-4354-a027-ad765673a82a)



# v5
Changes from v4: 
- Used SGD for D, ADAM for G network.
- Label Smoothing values are set between (0.1, 0.3)

 Step 100| Score Plot | Loss Plot
:-------------------------:|:-------------------------:|:-------------------------:
![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v5/generated/generated-images-0100.png) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/5140ecbc-ca20-4c0c-b558-24e10c4e901f) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/24a5ff9a-39dc-4a5a-82aa-fe16eb1c674e)


# v6 (WGAN)
Changes from v6:
- Used Wassertein Loss
