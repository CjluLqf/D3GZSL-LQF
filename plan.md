# Plan

## Task
将 d3gzsl 环境对齐到已验证可用的 PyTorch 2.9.1+cu130（RTX 5090），并同步更新初始化文档。

## 将要修改的文件
- /home/st/pytorch/lqf/D3GZSL-LQF/plan.md
- /home/st/pytorch/lqf/D3GZSL-LQF/init.md

## Steps
1. 检查 d3gzsl 环境当前 torch 版本与 CUDA 运行时版本。
2. 升级 pip/setuptools/wheel，清理旧 torch 包并安装 2.9.1+cu130。
3. 验证 torch 版本、CUDA 可用性与 GPU 识别。
4. 更新 init.md 的 PyTorch 安装章节，明确 cu130 与版本锁定。

## 本次执行说明
- 仅升级环境与文档，不改动训练逻辑。

## 执行状态
- 已完成：d3gzsl 已安装 PyTorch 2.9.1+cu130，并同步更新 init.md。
