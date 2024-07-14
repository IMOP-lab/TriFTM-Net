# TriFTM-Net: Tri-Path Fourier-Temporal Modulation Network for macular edema Pathology Segmentation and Reconstruction in High-Precision Intraoperative Navigation

TriFTM-Net:TriFTM-Net: Tri-Path Fourier-Temporal Modulation Network for macular edema Pathology Segmentation and Reconstruction in High-Precision Intraoperative Navigation

Xingru Huang, Shuaibin Chen, Huawei Wang, Yaoqi Sun, Tangsen Huang, Jian Huang,  Yihao Guo, Hong He, Minhong Sun, Jin Liu, Zhiwen Zheng, Xiaoshuai Zhang and Shaowei Jiang

Hangzhou Dianzi University IMOP-lab

<div align=center>
  <img src="https://github.com/IMOP-lab/TriFTM-Net/blob/main/figure/triftm-net.png">
</div>
<p align=center>
  Figure 1: Detailed network structure of the TriFTM-Net.
</p>

We propose TriFTM-Net, a 2D medical image segmentation network for high-precision intraoperative navigation that integrates spatial, frequency, and spatiotemporal domain information. TriFTM-Net achieves the best performance on key metrics compared to 13 previous methods on the OIMHS dataset. 

We will first introduce our methods and principles, then describe the experimental environment, and finally present the experimental results.

## Methods
### TPSHE

<div align=center>
  <img src="https://github.com/IMOP-lab/TriFTM-Net/blob/main/figure/tpshe.png"width=80% height=80%>
</div>
<p align=center>
  Figure 3: Structure of the TPSHE.
</p>

TPSHE, as an innovative encoder integrating spatial, spectral, and time-frequency domains, is capable of capturing both global structural information, such as the choroid and retina, and localized features, including macular edema.

### FRM

<div align=center>
  <img src="https://github.com/IMOP-lab/TriFTM-Net/blob/main/figure/frm.png"width=80% height=80%>
</div>
<p align=center>
  Figure 3: Structure of the FRM.
</p>

FRM is integrated between the encoder and decoder to optimize the capture and utilization of fine-grained information within deep feature maps. This approach suppresses irrelevant factors, mitigates noise interference, and enhances the network's capacity to represent detailed features, such as those associated with macular edema.

### HFRM

<div align=center>
  <img src="https://github.com/IMOP-lab/TriFTM-Net/blob/main/figure/hfrm.png"width=80% height=80%>
</div>
<p align=center>
  Figure 3: Structure of the HFRM.
</p>

HFRM enables the model to accurately reconstruct the high-level features required for detail enhancement from the sampled features, avoiding the loss of detail information. By utilizing multi-scale convolution operations and integrating features of different levels, it significantly improves the model's performance. The DCB ensures the accuracy of the enhanced features.

## Installation
Experiments were conducted under identical hardware and software environments: four servers, each equipped with two NVIDIA Geforce RTX 3080 10GB GPUs and 128GB of memory. The project was implemented using Python 3.9.0, PyTorch 1.13.1, and CUDA 11.7.64, with Distributed Data Parallel (DDP) training and evaluation. The optimizer used was AdamW with an initial learning rate set at 0.0001. Model weights were randomly initialized, the batch size was set to 4, and the training spanned 100 epochs.

## Experiment

### Compare with others on the OIMHS dataset

<div align=center>
  <img src="https://github.com/IMOP-lab/TriFTM-Net/blob/main/figure/baselines.png">
</div>
<p align=center>
  Figure 6: Comparison experiments between our method and 13 previous segmentation methods on the OIMHS dataset.
</p>

<div align=center>
  <img src="https://github.com/IMOP-lab/TriFTM-Net/blob/main/figure/.png">
</div>
<p align=center>
  Figure 7: The visual results of our method compared to the existing 13 segmentation methods on the OIMHS dataset.
</p>

#### Cross Validation Results

<div align=center>
  <img src="https://github.com/IMOP-lab/SASAN-Pytorch/blob/main/figures/five-fold-cross.png">
</div>
<p align=center>
  Figure 8: Our method's 5-fold cross-validation results compared to the 13 segmentation methods on the OIMHS dataset.
</p>

Comparative experiments on the public OIMHS dataset and five-fold cross-validation further demonstrate the efficacy and reliability of our method against previous approaches.

### Ablation study

#### Key components of SASAN
<div align=center>
  <img src="https://github.com/IMOP-lab/SASAN-Pytorch/blob/main/tables/Ablation1.png">
</div>
<p align=center>
  Figure 9: Ablation experiments on key components of SASAN on the CMED dataset.
</p>

FINE introduces a wide range of low-frequency features, which has a good effect in reducing high-frequency noise and enhancing detail extraction. ASEM has a strong ability to enhance the network for the analysis of features that are difficult to distinguish objects.

#### Loss function strategy

<div align=center>
  <img src="https://github.com/IMOP-lab/SASAN-Pytorch/blob/main/tables/Ablation2.png">
</div>
<p align=center>
  Figure 10: Ablation experiments on Loss function strategy on the CMED dataset.
</p>

The self-updating mechanism and BoundaryRea Loss enhance the network's boundary segmentation ability. To a certain extent, it also improves the overall segmentation ability of the network.

### Model Complexity

<div align=center>
  <img src="https://github.com/IMOP-lab/SASAN-Pytorch/blob/main/figures/Parameters.png">
