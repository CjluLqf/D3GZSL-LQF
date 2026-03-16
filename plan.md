# Plan

## Task
新增仓库忽略规则，避免训练运行产生的无关文件被提交。

## 将要修改的文件
- /home/st/pytorch/lqf/D3GZSL-LQF/plan.md
- /home/st/pytorch/lqf/D3GZSL-LQF/.gitignore

## Steps
1. 在仓库根目录创建 .gitignore。
2. 写入 Python 缓存、训练产物、日志、IDE 配置、数据目录等忽略规则。
3. 用 git status 验证规则生效。
4. 若已有历史追踪噪音文件，后续按需执行 git rm --cached 清理索引。

## 本次执行说明
- 忽略 data/。
- 忽略 .vscode/ 与 .idea/。
- 不修改训练代码。

## 执行状态
- 已完成：创建 /home/st/pytorch/lqf/D3GZSL-LQF/.gitignore。
- 已验证：git check-ignore 命中 models/、wandb/、data/、.vscode/、img/ 规则。
