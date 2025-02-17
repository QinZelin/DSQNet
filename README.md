### Installation
# DSQNet: Enhancing Change Detection Network via Deep Semantics Query for Remote Sensing Images
### Zilin Qin and Lefei Zhang

<p align="center">
  <a href="#introduction">Introduction</a> |
  <a href="#Results">Results</a> |
  <a href="#usage">Usage</a> |
</p >
## Introduction

Abstract— Change detection from remote sensing (RS) images has made significant progress in many applications including environmental
protection and agricultural monitoring. Recently, RS change detection
algorithms mainly focus on feature interaction between the bitemporal
images. However, there is a challenge in existing methods regarding
how to focus more attention on local prominent features and specifically
enhance their salience during the interaction of representations. For this
issue, this letter presents a change detection network DSQNet that marks
multiple regions of interest using query vectors with deep semantics and
explicitly searches the heterogeneous features for focused interaction.
Specifically, DSQNet uses bidirectional matching query (BMQ) module
to effectively perceive local relevant features by feature space query
for cross matching and adequately enhance the context relationship
within specific regions during the interaction, which helps the model
better learn the idea of potential change. Moreover, to make the query
vectors and the feature representation aligned in the semantic space,
we further propose the deep semantic adjustment feature pyramid (DSP)
module. It realizes interlayer feature adjustment from the inside out
in the pyramid and enables query vectors to represent extremely rich
semantics, improving query efficiency. Experimental results on four
benchmark datasets show that DSQNet achieves better performance than
other advanced change detection networks.

<figure>
<img src=DSQNet_framework.png>
<figcaption align = "center"><b>Fig.1 - The overall framework of DSQNet </b></figcaption>
</figure>
<figure>
<div align="center">
<img src=myvisualization.png>
</div>
<figcaption align = "center"><b>Fig.2 - Comparison of result mask maps by various methods on different
datasets. </b></figcaption>
</figure>

#Results
|Dataset|Backbone | Input size | Params (M) | Fscore| IoU|
|-------|-------- | ----------  | ----- | ----- | ----- |
| LEVIR-CD |Swin-T | 512 × 512 | 29.5M| 92.03 | 85.24 |
| SVCD |Swin-T |  512 × 512 | 29.5M |97.20 | 94.55|
| S2Looking | Swin-T |256 × 256 | 29.5M| 66.85 | 50.21|
| DSIFN | Swin-T | 256 × 256 | 29.5M | 69.77| 53.89 |
| LEVIR-CD |ViTAE-S | 512 × 512 | 19.8M| 92.44 | 85.94 |
| SVCD |ViTAE-S |  512 × 512 | 19.8M |97.66 | 95.43|
| S2Looking | ViTAE-S |256 × 256 | 19.8M| 67.08 | 50.47|
| DSIFN | ViTAE-S | 256 × 256 | 19.8M | 70.01| 54.32 |

#Usage
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

