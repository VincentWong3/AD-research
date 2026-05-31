# AD-Research

自动驾驶领域经典论文的中文翻译，基于 Claude Code + arxiv-paper-translator-v2 翻译流水线。

每篇论文包含：
- `*_中文.pdf` — 编译好的中文翻译 PDF
- `latex_source/` — 翻译后的 LaTeX 源码，可重新编译

## 已翻译论文

| 论文 | 领域 | 会议 | 页数 |
|------|------|------|------|
| [VAD](VAD/) | 端到端自动驾驶 | CVPR 2023 | 10 |
| [UniAD](UniAD/) | 端到端自动驾驶 | CVPR 2023 | 22 |
| [DETR3D](DETR3D/) | 3D目标检测 | CoRL 2021 | 12 |
| [PETR](PETR/) | 3D目标检测 | ECCV 2022 | 16 |
| [MapTR](MapTR/) | 在线建图 | ICLR 2023 | 17 |
| [MOTR](MOTR/) | 多目标跟踪 | ECCV 2022 | 14 |
| [MTR](MTR/) | 运动预测 | NeurIPS 2022 | 17 |
| [ANYmal](ANYmal/) | 四足机器人 | Science Robotics 2020 | 20 |

## 翻译方法

使用 [arxiv-paper-translator-v2](https://github.com/arxiv-paper-translator-v2) 工作流：
- 基于 LaTeX 源码翻译，保留原始排版
- 独立审查 subagent 做准确性校对
- XeLaTeX 编译生成中文 PDF

🤖 Generated with [Claude Code](https://claude.com/claude-code)
