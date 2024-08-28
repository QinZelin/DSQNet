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

