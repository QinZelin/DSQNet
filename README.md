<h1 align="center"> PPNet: Enhancing Remote Sensing Image Change Detection Network via Potential Perception </h1> 

<p align="center">
  <a href="#introduction">Introduction</a> |
  <a href="#statement">Statement</a> |
  <a href="#results-and-models">Results & Models</a> |
  <a href="#usage">Usage</a> |
</p >

## Introduction

This repository contains codes, models and test results for the paper "PPNet: Enhancing Remote Sensing Image Change Detection Network via Potential Perception". 

Change detection from remote sensing (RS) images has made significant progress in many applications including environmental protection and agricultural monitoring. Recently, RS change detection algorithms mainly focus on feature interaction between the bitemporal images. However, since these existing models concentrate on global alignment of the whole image, they have payed less attention on local divergent characteristics, which leads to negative understanding of change region during feature interaction. It has become one of major hindrance to improving detection performance. To relieve this issue, this letter presents a change detection network PPNet that can effectively perceive potential change regions and boost the prominence of these heterogeneous features. Specifically, PPNet employs bidirectional matching query (BMQ) module to promote the model better learn the idea of “region of potential change” by querying relevant local regions for cross matching and feature alignment in the stage of interaction. Moreover, to enhance the ability of feature extraction and spatial representation, we further propose the deep semantic adjustment feature pyramid (DSP) module to better use the deep semantic feature and realize interlayer feature adjustment from the inside out. Experimental results on two benchmark datasets show that PPNet achieves better performance than other advanced change detection networks.


<figure>
<div align="center">
<img src=BMQModel.png width="80%">
</div>
<figcaption align = "center"><b>(a) is the overall framework of PPNet. (b) is a visual illustration of the BMQ module. The query key and extracted features are all from DSP in figture (b). </b></figcaption>
</figure>

## Statement
We adopt a change detection toolbox, open-cd, based on PyTorch and OpenMMLab related tools. Most of the basic codes are mainly from open-cd ( https://github.com/likyoo/open-cd ), please go to the sourced code if there are some problems. 


## Results and Models

We visualize the experimental results and it is shown that the four comparison models tend to produce results with incomplete regions. Instead, our proposed model can overcome this issue and produce semantically consistent regions in most cases, which further certifies its effectiveness.

<figure>
<div align="center">
<img src=results.png width="60%">
</div>
<figcaption align = "center"><b>Comparison of change maps of different methods on LEVIR-CD and S2Looking dataset. The red and green colors represent FP and FN results, respectively. (a) T1. (b) T2. (c) Ground Truth. (d) STANet. (e) BiT. (f) AANet. (g) ChangerAD. (h) Ours. </b></figcaption>
</figure>

### LEVIR-CD

| Method | Backbone |Input size  | F1  | Model |
| ------ | -------- |---------- | ------- | --- |
| PPNet| Swin-T |512 × 512 | 92.01 |  [baidu](https://pan.baidu.com/s/1-2IuJaOjhEi5luGk3sO2tw?pwd=rbsv) |
| PPNet| ViTAEv2-S |512 × 512 | 92.37 |  [baidu](https://pan.baidu.com/s/1nEQ_o63hzl4Y8goqBHcVMg?pwd=inzx) |
### S2Looking

| Method | Backbone |Input size | F1 | Model |
| ------ | -------- |---------- | ------- | --- |
| PPNet| Swin-T |512 × 512 | 66.69 |  [baidu](https://pan.baidu.com/s/1x4EynqGiKNOdrT4nfWom3g?pwd=ztga ) |
| PPNet| ViTAEv2-S |512 × 512 | 67.08 |  [baidu](https://pan.baidu.com/s/1ee88ZbYrYKm0NhpCU1gl2g?pwd=4ky8 ) |

## Usage

### Installation

The code framework is mainly borrowed from open-cd. Thus,

please refer to [opencd-README.md](https://github.com/likyoo/open-cd/blob/main/README.md) for installing main packeges such as python, pytorch, etc.

If there is some problem running the PPNet, please try the following environment:
- Python 3.8.18
- Pytorch 1.9.0+cu111
- torchvision 0.10.0+cu111
- timm 0.9.12
- mmcv 2.1.0
- mmengine 0.10.2
  
### Training

Training the PPNet with Swin-T backbone on LEVIR-CD dataset: 

```
python tools/train.py configs/PPNet/PPNet_swin_imp_512x512_80k_levircd_lr1e-4_bs8_wd0.01.py --work-dir ./PPNet_swin_imp_512x512_80k_levircd_lr1e-4_bs8_wd0.01
```

Training the PPNet with ViTAEv2-S backbone on S2Looking dataset: 

```
python tools/train.py PPNet_vitae_imp_512x512_80k_s2looking_lr1e-4_bs8_wd0.01.py --work-dir ./PPNet_vitae_imp_512x512_80k_s2looking_lr1e-4_bs8_wd0.01.py
```

### Inference

Evaluation using Swin-T backbone on LEVIR-CD dataset

```
python tools/test.py configs/PPNet/PPNet_swin_imp_512x512_80k_levircd_lr1e-4_bs8_wd0.01.py [model pth] --show-dir visualization/LEVIR
```

Evaluation using ViTAEv2-S backbone on S2Looking dataset

```
python tools/test.py configs/PPNet/PPNet_vitae_imp_512x512_80k_s2looking_lr1e-4_bs8_wd0.01.py [model pth] --show-dir visualization/S2Looking
```

