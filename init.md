# D3GZSL CUB 初始化与运行指南

## 1. 创建并激活环境（d3gzsl）

```bash
conda create -n d3gzsl python=3.10 -y
conda activate d3gzsl
```

## 2. 安装 PyTorch（CUDA 12.1）

```bash
conda install -y pytorch torchvision pytorch-cuda=12.1 -c pytorch -c nvidia
```

如果不使用 CUDA，可改为 CPU 版本（可选）：

```bash
conda install -y pytorch torchvision cpuonly -c pytorch
```

## 3. 安装其余依赖

```bash
pip install numpy scipy scikit-learn matplotlib seaborn wandb
```

## 4. 准备 CUB 数据文件

请确保以下文件存在：

- gzsl/data/cub/res101.mat
- gzsl/data/cub/att_splits.mat

检查命令：

```bash
cd /home/st/pytorch/lqf/D3GZSL-LQF
ls -lh gzsl/data/cub/res101.mat gzsl/data/cub/att_splits.mat
```

## 5. 运行训练脚本

```bash
conda activate d3gzsl
cd /home/st/pytorch/lqf/D3GZSL-LQF/gzsl
wandb offline
python main.py
```

## 6. 说明与常见坑

1. 运行目录必须在 gzsl 下。
   main.py 使用相对路径 ./data/cub/...，所以要在 gzsl 目录执行。
2. 脚本会初始化 wandb。
   不想联网记录时可先执行 wandb offline。
3. 默认使用 0 号 GPU。
   main.py 中硬编码 CUDA_VISIBLE_DEVICES='0'。

## 7. 快速自检（可选）

```bash
python -c "import torch, scipy, sklearn, wandb; print('ok', torch.__version__)"
python -c "import torch; print('cuda:', torch.cuda.is_available())"
```
