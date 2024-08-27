<h1 align="center"> DSQNet: Enhancing Change Detection Network via Deep Semantics Query for Remote Sensing Images </h1> 

<p align="center">
  <a href="#introduction">Introduction</a> |
  <a href="#statement">Statement</a> |
  <a href="#results-and-models">Results & Models</a> |
  <a href="#usage">Usage</a> |
</p >

## Introduction

This repository contains codes, models and test results for the paper "DSQNet: Enhancing Change Detection Network via Deep Semantics Query for Remote Sensing Images". 

Change detection from remote sensing (RS) images has made significant progress in many applications including environmental protection and agricultural monitoring. Recently, RS change detection algorithms mainly focus on feature interaction between the bitemporal images. However, since these existing models concentrate on global alignment of the whole image, they have payed less attention on local divergent characteristics, which leads to negative understanding of change region during feature interaction. It has become one of major hindrance to improving detection performance. To relieve this issue, this letter presents a change detection network DSQNet that queries potential change regions using keys with deep semantics to boost the prominence of these heterogeneous features. Specifically, DSQNet employs bidirectional matching query (BMQ) module to promote the model better learn the idea of “region of potential change” by utilizing query keys to adequately perceive local relevant features for cross matching in the stage of interaction. Moreover, in order to make the query key and the feature representation aligned in the semantic space, we further propose the deep semantic adjustment feature pyramid (DSP) module. It realizes interlayer feature adjustment from the inside out in pyramid and enables query keys represent extremely rich semantics, improving query efficiency. Experimental results on two benchmark datasets show that DSQNet achieves better performance than other advanced change detection networks.


<figure>
<div align="center">
<img src=DSQ.png width="80%">
</div>
<figcaption align = "center"><b>(a) is the overall framework of DSQNet. (b) is a visual illustration of the BMQ module. The query key and extracted features are all from DSP in figture (b). </b></figcaption>
</figure>

## Statement
We adopt a change detection toolbox, open-cd, based on PyTorch and OpenMMLab related tools. Most of the basic codes are mainly from open-cd ( https://github.com/likyoo/open-cd ), please go to the sourced code if there are some problems. 


## Results and Models

We visualize the experimental results and it is shown that the four comparison models tend to produce results with incomplete regions. Instead, our proposed model can overcome this issue and produce semantically consistent regions in most cases, which further certifies its effectiveness.

<figure>
<div align="center">
<img src=result.png width="60%">
</div>
<figcaption align = "center"><b>Comparison of change maps of different methods on LEVIR-CD and S2Looking dataset. The red and green colors represent FP and FN results, respectively. (a) T1. (b) T2. (c) Ground Truth. (d) STANet. (e) BiT. (f) AANet. (g) ChangerAD. (h) Ours. </b></figcaption>
</figure>

### LEVIR-CD

| Method | Backbone |Input size  | F1  | Model |
| ------ | -------- |---------- | ------- | --- |
| DSQNet| Swin-T |512 × 512 | 92.01 |  [baidu](https://pan.baidu.com/s/1-2IuJaOjhEi5luGk3sO2tw?pwd=rbsv) |
| DSQNet| ViTAEv2-S |512 × 512 | 92.37 |  [baidu](https://pan.baidu.com/s/1nEQ_o63hzl4Y8goqBHcVMg?pwd=inzx) |
### S2Looking

| Method | Backbone |Input size | F1 | Model |
| ------ | -------- |---------- | ------- | --- |
| DSQNet| Swin-T |512 × 512 | 66.69 |  [baidu](https://pan.baidu.com/s/1x4EynqGiKNOdrT4nfWom3g?pwd=ztga ) |
| DSQNet| ViTAEv2-S |512 × 512 | 67.08 |  [baidu](https://pan.baidu.com/s/1ee88ZbYrYKm0NhpCU1gl2g?pwd=4ky8 ) |

## Usage

### Installation

The code framework is mainly borrowed from open-cd. Thus,

please refer to [opencd-README.md](https://github.com/likyoo/open-cd/blob/main/README.md) for installing main packeges such as python, pytorch, etc.

If there is some problem running the DSQNet, please try the following environment:
- Python 3.8.18
- Pytorch 1.9.0+cu111
- torchvision 0.10.0+cu111
- timm 0.9.12
- mmcv 2.1.0
- mmengine 0.10.2
  
### Training

Training the DSQNet with Swin-T backbone on LEVIR-CD dataset: 

```
python tools/train.py configs/DSQNet/DSQNet_swin_imp_512x512_80k_levircd_lr1e-4_bs8_wd0.01.py --work-dir ./DSQNet_swin_imp_512x512_80k_levircd_lr1e-4_bs8_wd0.01
```

Training the DSQNet with ViTAEv2-S backbone on S2Looking dataset: 

```
python tools/train.py configs/DSQNet/DSQNet_vitae_imp_512x512_80k_s2looking_lr1e-4_bs8_wd0.01.py --work-dir ./DSQNet_vitae_imp_512x512_80k_s2looking_lr1e-4_bs8_wd0.01.py
```

### Inference

Evaluation using Swin-T backbone on LEVIR-CD dataset

```
python tools/test.py configs/DSQNet/DSQNet_swin_imp_512x512_80k_levircd_lr1e-4_bs8_wd0.01.py [model pth] --show-dir visualization/LEVIR
```

Evaluation using ViTAEv2-S backbone on S2Looking dataset

```
python tools/test.py configs/DSQNet/DSQNet_vitae_imp_512x512_80k_s2looking_lr1e-4_bs8_wd0.01.py [model pth] --show-dir visualization/S2Looking
```

