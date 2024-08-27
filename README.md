<h1 align="center"> DSQNet: Enhancing Change Detection Network via Deep Semantics Query for Remote Sensing Images </h1> 

<p align="center">
  <a href="#introduction">Introduction</a> |
  <a href="#statement">Statement</a> |
  <a href="#results-and-models">Results & Models</a> |
  <a href="#usage">Usage</a> |
</p >

## Introduction

This repository contains codes for "DSQNet: Enhancing Change Detection Network via Deep Semantics Query for Remote Sensing Images". 

Change detection from remote sensing (RS) images has made significant progress in many applications including environmental protection and agricultural monitoring. Recently, RS change detection algorithms mainly focus on feature interaction between the bitemporal images. However, there is a challenge in existing methods regarding how to focus more attention on local prominent features and effectively enhance their salience during the interaction of representations. For this issue, this letter presents a change detection network DSQNet that marks multiple regions of interest using query vectors with deep semantics and explicitly searches the heterogeneous features for focused interaction. Specifically, DSQNet employs bidirectional matching query (BMQ) module to effectively perceive local relevant features by feature space query for cross matching and adequately enhance the context relationship within specific regions during the interaction, which helps the model better learn the idea of potential change. Moreover, in order to make the query vectors and the feature representation aligned in the semantic space, we further propose the deep semantic adjustment feature pyramid (DSP) module. It realizes interlayer feature adjustment from the inside out in the pyramid and enables query vectors to represent extremely rich semantics, improving query efficiency. Experimental results on four benchmark datasets show that DSQNet achieves better performance than other advanced change detection networks.

<figure>
<div align="center">
<img src=DSQ.png width="80%">
</div>
<figcaption align = "center"><b>(a) is the overall framework of DSQNet. (b) is a visual illustration of the BMQ module.</b></figcaption>
</figure>

## Statement
We adopt a change detection toolbox, open-cd, based on PyTorch and OpenMMLab related tools. Most of the basic codes are mainly from open-cd ( https://github.com/likyoo/open-cd ), please go to the sourced code if there are some problems. 


## Results and Models

We visualize the experimental results and it is shown that the four comparison models tend to produce results with incomplete regions. Instead, our proposed model can overcome this issue and produce semantically consistent regions in most cases, which further certifies its effectiveness.

<figure>
<div align="center">
<img src=result.png width="60%">
</div>
<figcaption align = "center"><b>Comparison of change maps of different methods on LEVIR-CD and S2Looking dataset. The red and green colors represent FP and FN results, respectively. (a) T1. (b) T2. (c) Ground Truth. (d) BiT. (e) AANet. (f) ChangerAD. (g) TransYNet. (h) Ours. </b></figcaption>
</figure>

### LEVIR-CD

| Method | Backbone |Input size  | F1  | Model |
| ------ | -------- |---------- | ------- | --- |
| DSQNet| Swin-T |512 × 512 | 92.03 |  [baidu](https://pan.baidu.com/s/1-2IuJaOjhEi5luGk3sO2tw) |
| DSQNet| ViTAEv2-S |512 × 512 | 92.44 |  [baidu](https://pan.baidu.com/s/1nEQ_o63hzl4Y8goqBHcVMg) |
### S2Looking

| Method | Backbone |Input size | F1 | Model |
| ------ | -------- |---------- | ------- | --- |
| DSQNet| Swin-T |512 × 512 | 66.85 |  [baidu](https://pan.baidu.com/s/1x4EynqGiKNOdrT4nfWom3g) |
| DSQNet| ViTAEv2-S |512 × 512 | 67.08 |  [baidu](https://pan.baidu.com/s/1ee88ZbYrYKm0NhpCU1gl2g) |

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

