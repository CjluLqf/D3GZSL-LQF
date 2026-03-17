# D3GZSL CUB 初始化与运行指南（RTX 5090）

## 0. 服务器信息

- GPU: RTX 5090
- Driver: 580.126.09
- System CUDA: 13.0

说明：推荐对齐到已验证可用组合：PyTorch 2.9.1+cu130。

## 1. 创建并激活环境（d3gzsl）

```bash
conda create -n d3gzsl python=3.11 -y
conda activate d3gzsl
```

## 2. 安装 PyTorch（固定 2.9.1+cu130，适配 5090）

```bash
# 可选：先升级打包工具
python -m pip install -U pip setuptools wheel

# 建议：先移除旧版本，避免残留冲突
pip uninstall -y torch torchvision torchaudio

# 安装与已验证环境一致的版本
pip install torch==2.9.1 torchvision==0.24.1 torchaudio==2.9.1 --index-url https://download.pytorch.org/whl/cu130
```

如果不使用 CUDA，可改为 CPU 版本（可选）：

```bash
pip install torch torchvision torchaudio
```

## 3. 安装其余依赖

```bash
pip install numpy scipy scikit-learn matplotlib seaborn wandb
```

## 4. 准备 CUB 数据文件

先创建代码要求的数据目录：

```bash
cd /home/st/pytorch/lqf/D3GZSL-LQF
mkdir -p gzsl/data/cub
```

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
python -c "import torch; print('cuda:', torch.cuda.is_available()); print('gpu:', torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'none')"
python -c "import torch; print('torch:', torch.__version__); print('compiled_cuda:', torch.version.cuda); print('cudnn:', torch.backends.cudnn.version())"
```
