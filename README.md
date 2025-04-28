# Generative-assisted multi-stage integrated network
## Generative-assisted multi-stage integrated network: Tackling extreme noise in image denoising, Results in Engineering, Volume 26, 2025, 104999, ISSN 2590-1230, https://doi.org/10.1016/j.rineng.2025.104999.
Noise degrades image quality and can result in the loss of important information, making its removal or minimization essential. However, as noise levels increase, eliminating it becomes exponentially more challenging. This project proposes a **Generative-assisted  multi-stage integrated network (GainNet)** capable of restoring the textural details and patterns of original images lost due to extreme noise. We will keep you informed with additional details about this project.
## Requirements
- pytorch 1.21
- Python 3.9
- torchvision
- scikit-image
- os
- numpy

## Dataset description 
The relationship between the noisy image 𝑞, noise 𝑛, and high-quality image 𝑐 is defined as 𝑞=𝑛+𝑐. The noise 𝑛 is modeled as Gaussian noise, represented by $n \sim \mathcal{N}(\mu, \sigma^2)$, where $\sigma$ is the standard deviation. For training, the noise is randomly smapled within the range [10, 110] and added to high-quality images. 
  
The train and validation dataset are structured as below:
- Berkeley Segmentation Dataset (https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/bsds/)
- Waterloo Exploration Database (https://kedema.org/project/exploration/index.html)

The test dataset is structured as below:
- CBSD68
- Kodak24 (https://www.kaggle.com/datasets/drxinchengzhu/kodak24)
- Set5 (http://people.rennes.inria.fr/Aline.Roumy/results/SR_BMVC12.html)
- Urban100 (https://github.com/jbhuang0604/SelfExSR)
- AVIP (in-house curated dataset)

## Code description
### Models
The GainNet configuration model consists of `UNet_backbone.py` and `DE_block.py`.
- `UNet_backbone.py` includes Noise Estimatior block and Image-to-image translator block.
- `DE_block.py` includes U-Net and Swin transformer based Depth-fusion enhancer block.
### Util for training
- `utils.py` contains basic contents required for training and evaluation, such as PSNR and SSIM calculation, and weight initialization.
- `dataset.py` connects training images to Dataloader and changes them so that the model can train.
### Training and testing
- `train_GainNet.py` and `test_GainNet.py` are responsible for training GainNet and evaluating the trained model, respectively.

## Saved model
The `/trained model/` folder contains the trained models that constitute the GainNet. The trained models are saved as `.pth` file.

## Evaluation

![image](https://github.com/user-attachments/assets/c8018ec0-7980-409d-909c-72d3fad8a4e0)
**Fig. 1.**Visual comparison of denoising results with Kodak24 dataset under extreme noise conditions (𝜎 ≥ 50). (a) Input noisy images with varying noise level: 𝜎 = 50, 75, 90, 110 (PSNR = 14.59, 11.73, 10.88, 9.65 dB). (b) Denoising results of DnCNN (PSNR = 26.95, 24.57, 22.83, 21.83 dB), (c) FFDNet (PSNR = 27.41, 24.51, 22.69, 21.28 dB), (d) DudeNet (PSNR = 27.62, 25.12, 23.19, 22.30 dB), (e) NIFBGDNet (PSNR = 27.34, 24.87, 23.07, 22.05 dB), (f) DRDNet (PSNR = 27.43, 24.99, 23.68, 22.24 dB), and (g) the proposed GainNet (PSNR = 28.20, 26.45, 26.98, 24.68 dB).

![image](https://github.com/user-attachments/assets/2bf457e5-4d67-470a-b0c2-2467d7f00331)
**Fig. 2.** Visual comparison of denoising results with Set5 dataset under extreme noise conditions (𝜎 ≥ 50). (a) Input noisy images with varying noise level: 𝜎 = 50, 75, 90, 110 (PSNR = 15.48, 12.47, 11.27, 10.04 dB). (b) Denoising results of DnCNN (PSNR = 25.05, 21.55, 19.84, 18.13 dB), (c) FFDNet (PSNR = 25.43, 21.62, 19.90, 17.98 dB), (d) DudeNet (PSNR = 25.04, 21.62, 20.03, 18.30 dB), (e) NIFBGDNet (PSNR = 25.42, 21.82, 20.29, 18.50 dB), (f) DRDNet (PSNR = 25.13, 21.72, 20.01, 18.37 dB), and (g) the proposed GainNet (PSNR = 29.05, 27.16, 26.27, 25.18 dB).

![image](https://github.com/user-attachments/assets/0af9602a-16fb-4b03-82d8-45222994ec97)
**Fig. 2.** Visual comparison of denoising results with AVIP dataset under extreme noise conditions (𝜎 ≥ 50). (a) Input noisy images with varying noise level: 𝜎 = 50, 75, 90, 110 (PSNR = 14.82, 11.94, 10.84, 9.77 dB). (b) Denoising results of DnCNN (PSNR = 24.79, 22.25, 21.05, 19.71 dB), (c) FFDNet (PSNR = 25.11, 22.12, 20.66, 19.01 dB), (d) DudeNet (PSNR = 25.32, 22.70, 21.43, 20.02 dB), (e) NIFBGDNet (PSNR = 26.94, 22.43, 21.28, 19.88 dB), (f) DRDNet (PSNR = 25.27, 22.74, 21.48, 20.07 dB), and (g) the proposed GainNet (PSNR = 25.80, 23.97, 23.22, 22.56 dB).
