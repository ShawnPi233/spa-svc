Language: **English** 
[Change to Chinese Version](./cn_README.md) 

# SPA-SVC: Self-supervised Pitch Augmentation for Singing Voice Conversion

This is an official repository of our work **SPA-SVC**: **S**elf-supervised **P**itch **A**ugmentation for **S**inging **V**oice **C**onversion (Accepted by Interspeech2024).

Audio samples are available on the [page](https://shawnpi233.github.io/publication/paper/spasvc/).
Arxiv paper can be found here [https://arxiv.org/abs/2406.05692](https://arxiv.org/abs/2406.05692).

## SPA-SVC Architecture
![SPA-SVC Architecture](figs/architecture.png)

## (0) Environment Setups

```bash
# Creater conda environment, Python version 3.8.18
conda create -n spa-svc python=3.8.18
# Install requirements, torch version 1.31.1+cu116
pip install -r requirements.txt
```

```bash
# Activate conda environment
conda activate spa-svc
```

## (1) Data Preprocessing
```bash
nohup python preprocess.py -c configs/spa-svc.yaml >../preprocess_all.log 2>&1 &         
```

## (2) Model Training
```bash
nohup python train_diff_singing_enhance.py -c configs/spa-svc-m.yaml >../spa_svc_m.log 2>&1 & # use MSE cycle loss

nohup python train_diff_singing_enhance.py -c configs/spa-svc.yaml >../spa_svc.log 2>&1 & # use SSIM cycle loss
```

## (3) Model Inference
```bash
nohup python main_diff.py \
    -i '/path/to/your/audio/directory/' \
    -diff '/path/to/your/model/directory/model.pt' \
    -o '/path/to/your/output/directory/' \
    -k 12 -id 1 -speedup 'auto' -method 'auto' \
    -kstep 100 --gpu_ids 1 \
    > '/path/to/your/log/directory/diffusion-test.log' 2>&1 &
```
