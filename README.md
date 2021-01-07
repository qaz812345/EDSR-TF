# EDSR-TF
This is a task of image super resolution. We use 291 dataset which contains 291 high-resolution images as the training set. We train an EDSR network from [GitHub](https://github.com/Saafke/EDSR_Tensorflow). EDSR is an enhanced version of the residual network architecture which handles a specific super-resolution scale, and it use the residual block without the batch normalization.

We test on Set14 dataset which contains 14 low-resolution images on a scale of 3, and the highest testing PSNR can reach 25.680 dB.

# Reproducing Submission
1. [Requirement](#Requirement)
2. [Installation](#Installation)
3. [Dataset Configuration](#Dataset-Configuration)
4. [Training](#Training)
5. [Inference](#Inference)

# Requirement
* tensorflow 1.15.0
* opencv-python

# Installation
1. Clone this repository. 
```
git clone https://github.com/qaz812345/EDSR-TF.git
```
2. cd to this repository and clone [EDSR](https://github.com/Saafke/EDSR_Tensorflow) repository.
```
git clone https://github.com/Saafke/EDSR_Tensorflow.git
```
3. Replace ```main.py``` and ```run.py```.

# Dataset Configuration
1. Download training and test dataset from [here](https://drive.google.com/drive/u/0/folders/1H-sIY7zj42Fex1ZjxxSC3PV1pK4Mij6x)
2. Unzip the dataset files and Set the data directory structure as:
```
EDSR-TF
|__EDSR_Tensorflow
|   |__data
|   |   |__train
|   |   |   |__<train_image>
|   |   |   |__ ...
|   |   |
|   |   |__val
|   |   |   |__<val_image>
|   |   |   |__ ...
|   |   |
|   |   |__test
|   |       |__<test_image>
|   |        |__ ...
|   |  
|   |__ ...
|   |__ ...
```
3. The ```val``` directory is optional, you can pass the same path with training dataset if you want. Here I pick 51 images to the val directory.

# Training
### Data Pre-process and Augmentation
* Creates 48*48 LR patches with corresponding HR patches
* Normalize with pre-computed mean of training set
* Random flip

### Training Command:
```python main.py --train --fromscratch --scale 3 --traindar data/train --validdir data/val --epochs 100 --batch 32```

# Inference
To test on test dataset with a scale of 3.
### Inference command:
```python main.py --upscale --scale 3 --traindar data/train --testdir data/test --savedir <results_dir>```

# Reference
* Saafke, EDSR_Tensorflow, viewed 7 Jan 2021, [https://github.com/Saafke/EDSR_Tensorflow](https://github.com/Saafke/EDSR_Tensorflow)