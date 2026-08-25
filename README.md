# AD-Research

深度学习/自动驾驶领域经典论文的中文翻译，基于 arxiv-paper-translator-v2 翻译流水线。

每篇论文一个文件夹，只保留成品：
- `<论文名>_中文.pdf` — 编译好的中文翻译 PDF（XeLaTeX 排版）

## 已翻译论文

| 论文 | 领域 | 会议/来源 | 页数 |
|------|------|-----------|------|
| [VAD](VAD/) | 端到端自动驾驶 | CVPR 2023 | 10 |
| [UniAD](UniAD/) | 端到端自动驾驶 | CVPR 2023 | 22 |
| [DETR3D](DETR3D/) | 3D目标检测 | CoRL 2021 | 12 |
| [PETR](PETR/) | 3D目标检测 | ECCV 2022 | 16 |
| [MapTR](MapTR/) | 在线建图 | ICLR 2023 | 17 |
| [MOTR](MOTR/) | 多目标跟踪 | ECCV 2022 | 14 |
| [MTR](MTR/) | 运动预测 | NeurIPS 2022 | 17 |
| [ANYmal](ANYmal/) | 四足机器人 | Science Robotics 2020 | 20 |
| [BEVFormer](BEVFormer/) | BEV感知 | ECCV 2022 | 18 |
| [BEVFormerV2](BEVFormerV2/) | BEV感知 | CVPR 2023 | 12 |
| [ST-P3](ST-P3/) | 端到端自动驾驶 | ECCV 2022 | 21 |
| [SparseAD](SparseAD/) | 端到端自动驾驶 | ECCV 2024 | 34 |
| [VADv2](VADv2/) | 端到端自动驾驶 | ICLR 2026 | 14 |
| [BridgeSim](BridgeSim/) | 端到端自动驾驶 | arXiv 2604.10856 | 23 |
| [DiT](DiT/) | 扩散模型 (Diffusion Transformer) | ICCV 2023 | 25 |
| [去噪扩散概率模型](去噪扩散概率模型/) | 扩散模型 (DDPM) | NeurIPS 2020 | 25 |
| [基于潜扩散模型的高分辨率图像合成](基于潜扩散模型的高分辨率图像合成/) | 扩散模型 (潜扩散/LDM) | CVPR 2022 | 44 |
| [Diffusion Planner](Diffusion%20Planner/) | 自动驾驶规划 (扩散模型) | ICLR 2025 | 20 |
| [DiffusionDrive](DiffusionDrive/) | 端到端自动驾驶 (扩散模型) | CVPR 2025 | 14 |
| [Depth Anything 3](Depth%20Anything%203/) | 单目深度估计 | arXiv 2511.10647 | 31 |
| [Transformer 是贝叶斯网络](Transformer%20是贝叶斯网络/) | 理论 | arXiv 2603.17063 | 28 |
| [Transformer 注意力的贝叶斯几何](Transformer%20注意力的贝叶斯几何/) | 理论 | arXiv 2512.22471 | 27 |
| [强化学习中的延迟](强化学习中的延迟/) | 强化学习 | arXiv 2309.11096 | 158 |
| [重新审视基于模仿的自动驾驶规划器](重新审视基于模仿的自动驾驶规划器/) | 自动驾驶规划 | arXiv 2309.10443 | 7 |
| [端到端自动驾驶中的后训练：统一视角](端到端自动驾驶中的后训练：统一视角/) | 端到端自动驾驶 | arXiv 2607.08072 | 20 |
| [DriveLM](DriveLM/) | 驾驶语言导航 (图VQA) | arXiv 2312.14150 | 45 |
| [告别基于学习的车辆运动规划的误区](告别基于学习的车辆运动规划的误区/) | 自动驾驶规划 | arXiv 2306.07962 | 13 |
| [量化布尔贝叶斯网络](量化布尔贝叶斯网络/) | 概率图模型 | arXiv 2402.06557 | 32 |
| [离线强化学习中用于精确能量引导扩散采样的对比能量预测](离线强化学习中用于精确能量引导扩散采样的对比能量预测/) | 强化学习 (扩散模型/能量引导) | NeurIPS 2023 | 34 |

## 翻译方法

使用 [arxiv-paper-translator-v2](https://github.com/arxiv-paper-translator-v2) 工作流：
- 基于 LaTeX 源码翻译，保留原始排版
- 独立审查 subagent 做准确性校对
- XeLaTeX 编译生成中文 PDF

## 仓库规范

- 每个论文文件夹只保留编译好的成品 PDF，不保留中间文件（LaTeX 源码、图片、日志等）
- 经典论文用其代号命名文件夹（如 BEVFormer、VAD、DiT、BridgeSim、Diffusion Planner），无代号的用论文名
- 新增翻译请遵守 [CONTRIBUTING.md](CONTRIBUTING.md) 归档规范
