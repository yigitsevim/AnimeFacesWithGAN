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

| Step 50 | Step 100 |
|:--------------:|:--------------:|
| ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v1/generated/generated-images-0050.png) | ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v1/generated/generated-images-0100.png) |

| Score Plot | Loss Plot |
|:----------:|:----------:|
| ![Score Plot](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/b62e8c9d-a7f5-4b19-8ada-3bbfa72ee2d4) | ![Loss Plot](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/e3ed3fe8-7252-4769-b318-cc7c53f608e8) |

# v2

Changes from v1: 
- Switched to LeakyReLU (from ReLU) on generator with the aim of achieving a stronger Generator model. However, that resulted into mode collapse so this change is reverted on the next experiments.

| Step 50 | Step 100 |
|:--------------:|:--------------:|
| ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v2/generated/generated-images-0050.png) | ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v2/generated/generated-images-0100.png) |

| Score Plot | Loss Plot |
|:----------:|:----------:|
| ![Score Plot](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/99872d5b-a4fa-4784-9bb6-6c936129ad8d) | ![Loss Plot](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/828bfe1e-5252-4a4b-b2fe-b12163007beb)|

# v3
  
Changes from v2: 
- Reverted back to ReLU for the Generator.
- Applied one-sided label smoothing to the Discriminator network: *The idea of one-sided label smoothing is to replace the target for the real examples with a value slightly less than one, such as 0.9. This prevents extreme extrapolation behavior in the discriminator.* - [NIPS 2016 Tutorial: Generative Adversarial Networks, 2016.](https://arxiv.org/abs/1701.00160) 

| Step 50 | Step 100 |
|:--------------:|:--------------:|
| ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v3/generated/generated-images-0050.png) | ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v3/generated/generated-images-0100.png) |

| Score Plot | Loss Plot |
|:----------:|:----------:| 
|![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/103bc25b-580a-4e1b-bafd-e954b242ab62) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/3a50f973-e090-4b88-a46e-00541aa4d354)|

# v4

Changes from v3: 
- Label smoothing is applied to both Generator and Discriminator networks. Smoothing value is selected uniform randomly between 0 - 0.2.

| Step 50 | Step 100 |
|:--------------:|:--------------:|
| ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v4/generated/generated-images-0050.png) | ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v4/generated/generated-images-0100.png) |

| Score Plot | Loss Plot |
|:----------:|:----------:| 
|![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/0137416f-a1a9-4838-a37a-4580cde4145c) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/bd5a257d-d4a6-483a-a345-c8c91ed11017)

# v5
Changes from v4: 
- Used SGD for D, ADAM for G network.
- Label Smoothing values are set between (0.1, 0.3)

| Step 50 | Step 100 |
|:--------------:|:--------------:|
| ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v5/generated/generated-images-0050.png) | ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v5/generated/generated-images-0100.png) |

| Score Plot | Loss Plot |
|:----------:|:----------:| 
|![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/25c01fee-2c6f-4c5a-aa9c-8d5e3f4541b2) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/f384cdcf-c8dd-49f7-9fac-300ce8756a4b)

# v6 (WGAN)
Changes from v5:
- Switched to WGAN
- Clipped Gradients between [-0.01, 0.01]
- N_critic = 2
- Added a linear layer at the end of the discriminator network instead of sigmoid.
- For both networks, optimizer is changed to RMSprop.
- LR = 0.00005
Most of these settings are found by the authors of the [Wasserstein GAN paper](https://arxiv.org/abs/1701.07875).
| Step 50 | Step 100 |
|:--------------:|:--------------:|
| ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v6/generated/generated-images-0050.png) | ![](https://github.com/yigitsevim/AnimeFacesWithGAN/blob/main/v6/generated/generated-images-0100.png) |

| Score Plot | Loss Plot |
|:----------:|:----------:| 
|![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/78568cad-95f1-4fa4-98cd-640e7cbdb4fe) | ![image](https://github.com/yigitsevim/AnimeFacesWithGAN/assets/58977041/fc0ad3b0-72ce-4850-9221-2dc6b65bef4e)
