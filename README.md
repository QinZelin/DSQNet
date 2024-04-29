<h1 align="center"> Enhancing Change Detection Network via Bidirectional Matching Query for Remote Sensing Images </h1> 

<p align="center">
  <a href="#introduction">Introduction</a> |
  <a href="#statement">Statement</a> |
  <a href="#results-and-models">Results & Models</a> |
  <a href="#usage">Usage</a> |
</p >

## Introduction

This repository contains codes, models and test results for the paper "Enhancing Change Detection Network via Bidirectional Matching Query for Remote Sensing Images". 

Remote-sensing image change detection (CD) task plays an important role in disaster assessment, earth observation and other missions. Now, more studies focus on feature interaction between the bitemporal images. However, existing models solely concentrate on global alignment the entire image, neglecting the highlighting of local heterogeneous characteristics. This deficiency leads to negative understanding of change region during feature interaction. To solve this issue, we propose Bidirectional Matching Query (BMQ) module, which improves the saliency of change regions and makes the model grasp the concept of “change region of interest” by querying potential change regions for matching in the feature interaction. Additionally, to enhance the ability of feature representation and spatial relationship, we also propose Deep Semantic Regulation Feature Pyramid Network (DSR-FPN). It makes better use of deep semantic feature and realizes central regulation from top to bottom. With mentioned above, we design the network BMQNet and conduct experiments on two benchmark datasets. The experimental results show that BMQNet achieves better performance than other advanced foundation models in change detection task.


<figure>
<div align="center">
<img src=BMQNet.png width="80%">
</div>
<figcaption align = "center"><b>(a) is the overall framework of BMQNet. (b) is a visual illustration of the BMQ module. The query key and extracted features are all from DSR-FPN in figture (b). </b></figcaption>
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

### LEBIR-CD

| Method | Backbone |Input size  | F1  | Model |
| ------ | -------- |---------- | ------- | --- |
| BMQNet| Swin-T |512 × 512 | 92.01 |  [baidu](https://pan.baidu.com/s/1-2IuJaOjhEi5luGk3sO2tw?pwd=rbsv) |
| BMQNet| ViTAEv2-S |512 × 512 | 92.37 |  [baidu](https://pan.baidu.com/s/1nEQ_o63hzl4Y8goqBHcVMg?pwd=inzx) |
### S2Looking

| Method | Backbone |Input size | F1 | Model |
| ------ | -------- |---------- | ------- | --- |
| BMQNet| Swin-T |512 × 512 | 66.69 |  [baidu](https://pan.baidu.com/s/1x4EynqGiKNOdrT4nfWom3g?pwd=ztga ) |
| BMQNet| ViTAEv2-S |512 × 512 | 67.08 |  [baidu](https://pan.baidu.com/s/1ee88ZbYrYKm0NhpCU1gl2g?pwd=4ky8 ) |

## Usage

### Installation

The code framework is mainly borrowed from open-cd. Thus,

please refer to [opencd-README.md](https://github.com/likyoo/open-cd/blob/main/README.md) for installing main packeges such as python, pytorch, etc.

If there is some problem running the BMQNet, please try the following environment:
- Python 3.8.18
- Pytorch 1.9.0+cu111
- torchvision 0.10.0+cu111
- timm 0.9.12
- mmcv 2.1.0
- mmengine 0.10.2
  
### Training

Training the BMQNet with Swin-T backbone on LEVIR-CD dataset: 

```
python tools/train.py configs/BMQNet/BMQNet_swin_imp_512x512_80k_levircd_lr1e-4_bs8_wd0.01.py --work-dir ./BMQNet_swin_imp_512x512_80k_levircd_lr1e-4_bs8_wd0.01
```

Training the BMQNet with ViTAEv2-S backbone on S2Looking dataset: 

```
python tools/train.py BMQNet_vitae_imp_512x512_80k_s2looking_lr1e-4_bs8_wd0.01.py --work-dir ./BMQNet_vitae_imp_512x512_80k_s2looking_lr1e-4_bs8_wd0.01.py
```

### Inference

Evaluation using Swin-T backbone on LEVIR-CD dataset

```
python tools/test.py configs/BMQNet/BMQNet_swin_imp_512x512_80k_levircd_lr1e-4_bs8_wd0.01.py [model pth] --show-dir visualization/LEVIR
```

Evaluation using ViTAEv2-S backbone on S2Looking dataset

```
python tools/test.py configs/BMQNet/BMQNet_vitae_imp_512x512_80k_s2looking_lr1e-4_bs8_wd0.01.py [model pth] --show-dir visualization/S2Looking
```

