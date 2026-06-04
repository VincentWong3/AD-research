# 论文技术报告：VADv2 — 基于概率规划的端到端矢量化自动驾驶

> **arXiv ID**: 2402.13243
> **原文标题**: VADv2: End-to-End Vectorized Autonomous Driving via Probabilistic Planning
> **翻译日期**: 2026-06-04

---

## 📋 论文概览

### 基本信息
- **作者**: Bo Jiang, Shaoyu Chen, Hao Gao, Bencheng Liao, Qian Zhang, Wenyu Liu, Xinggang Wang
- **机构**: 华中科技大学, 地平线机器人 (Horizon Robotics)
- **发表**: ICLR 2026
- **领域**: 端到端自动驾驶、概率规划

### 核心贡献
1. 提出概率规划（Probabilistic Planning）来应对规划的不确定性和非确定性本质
2. 设计概率场（Probabilistic Field）建模从动作空间到概率分布的映射
3. 提出规划词表（Planning Vocabulary）离散化连续动作空间，使用最远轨迹采样（FTS）构建
4. VADv2 在 CARLA Town05、Bench2Drive、NAVSIM、3DGS 等多个基准上达到 SOTA

---

## 🎯 研究背景与动机

### 问题定义
端到端自动驾驶从大规模人类驾驶演示中学习驾驶策略，但规划具有**不确定性和非确定性**——同一场景下存在多种合理驾驶行为（如变道超车 vs 保持跟随）。

### 现有方法的局限性
现有方法（VAD、UniAD、Transfuser、MILE 等）遵循**确定性范式**，直接回归未来轨迹或控制信号。当可行解空间非凸时，确定性建模会输出"中间值"，导致安全风险。

### 本文的创新点
- 将规划策略建模为**场景条件下的非平稳随机过程** $p(\boldsymbol{a} | \boldsymbol{o})$
- **离散化动作空间**为 4096 大小的规划词表（每个动作是从真实驾驶中采样的完整轨迹）
- 受 NeRF 连续场和 LLM 语言建模启发，用**概率场 + Transformer** 学习动作分布

---

## 🔬 方法论

### 整体架构
```
多视角图像序列 → 场景编码器（BEV + Map/Agent/Traffic/Image Tokens）
                              ↓
                    规划令牌（位置编码）→ Transformer解码器 ← 场景令牌
                              ↓
                         概率场 → p(a) → 采样动作 → PID控制器
```

### 关键技术

1. **场景编码器**: 包含四类令牌——
   - 地图令牌（MapTRv2 风格，矢量化地图元素）
   - 智能体令牌（位置、朝向、速度、未来轨迹）
   - 交通元素令牌（交通灯、停止标志状态）
   - 图像令牌（前视图稠密特征）

2. **规划词表构建**: 最远轨迹采样（FTS）从驾驶演示动作集中选出 N=4096 个代表性轨迹，每个轨迹是自然满足运动学约束的完整 6-路径点序列

3. **概率场**: 用正弦位置编码将轨迹坐标映射到高维空间 $\mathbb{R}^{2L}$，级联 Transformer 解码器与场景令牌交互，MLP + Sigmoid 输出概率

4. **训练损失**:
   - **分布损失**: KL散度 → 交叉熵（$p_{\text{data}}$ 通过出现频率估计）
   - **冲突损失**: 与真实运动/道路边界冲突的动作降低概率
   - **场景令牌损失**: 地图/智能体/交通元素的监督信号

5. **推理**: 采样最高概率动作，Top-K + 规则包装器用于实际部署

---

## 📊 实验与结果

### 实验设置
- **数据集**: CARLA（约300万片段，Towns 3/4/6/7/10训练，Town05评估）、真实世界2000小时数据
- **评估指标**: DS（驾驶分数）、RC（路线完成率）、IS（违规分数）、碰撞率、PDMS 等
- **对比方法**: Transfuser, ThinkTwice, DriveMLM, VAD, UniAD, DiffusionDrive, GoalFlow 等

### 主要结果

| 基准 | VADv2 | 此前最佳 | 提升 |
|------|-------|----------|------|
| Town05 Long (DS) | **85.1** | 76.1 (DriveMLM) | +9.0 |
| Bench2Drive (DS) | **76.15** | 74.33 (ETA) | +1.82 |
| NAVSIM (PDMS) | **89.3** | 88.6 (Hydra-NeXt) | +0.7 |
| NAVSIMv2 (EPDMS) | **85.8** | 84.2 (PRIX) | +1.6 |
| 3DGS (碰撞率↓) | **0.270** | 0.320 (TransFuser) | -15.6% |

### 消融实验
- **概率 vs 确定性**: 概率规划在高交通密度下鲁棒性显著更好
- **冲突损失**: 移除后规划准确率下降
- **词表大小**: 256→4096 持续改善（离散化误差减小）
- **FTS vs k-means**: FTS 动作空间覆盖最优

---

## 💡 关键见解

### 概率规划的优越性
- 确定性规划在高交通密度下性能明显退化，概率规划保持稳定
- 开环指标上两者接近，闭环中概率规划显著胜出（说明开环评估的局限）

### 与 LLM 的类比
- LLM：给定上下文 → 下一个词的条件概率分布 → 采样
- VADv2：给定场景 → 动作的条件概率分布 → 采样
- 两者都在大规模数据上学习经验分布，用交叉熵最小化预测分布与经验分布的差异

---

## 🔍 局限性与未来工作

### 当前局限
- 仿真器和 3DGS 环境仍存在智能体行为简单、场景真实感不足的问题
- 规划词表增加少量推理开销（125ms vs 118ms 基线）

### 未来方向
- 利用更大规模专家驾驶数据提升规划性能
- 缩小仿真与真实部署之间的差距

---

## 📚 相关工作对比

| 方法 | 核心思想 | 优势 | 劣势 |
|------|---------|------|------|
| VAD | 矢量化场景表示 | 去稠密地图，高效 | 确定性回归，无法处理多模态 |
| UniAD | 多任务感知+预测+规划 | 联合优化 | 复杂流程，计算量大 |
| DiffusionDrive | 扩散模型生成轨迹 | 高质量多模态 | 预定义锚点限制多样性 |
| GoalFlow | 目标点+流匹配 | 分解简化 | 单目标点限制多样性 |
| **VADv2** | **概率场+规划词表** | **完整分布建模，多模态鲁棒** | 词表构建需离线处理 |

---

## 🎓 个人评价

### 优点
- 概率规划是解决不确定性的优雅方案，与 LLM 的类比清晰
- 规划词表+离散化巧妙将连续空间问题转化为可处理的形式
- 跨多个基准的闭环验证充分，实验扎实
- 纯视觉方案（仅相机），实用性高

### 可改进之处
- 词汇表固定大小 4096 可能在大规模部署时有覆盖不足的风险
- 对"中间动作"导致安全问题的解释可以更量化

### 推荐阅读对象
- 自动驾驶规划研究者
- 对概率建模、离散化技术感兴趣的研究人员
- 正在从确定性方法转向概率方法的工程师

---

## 📎 附录

### 关键公式
- 概率规划模型: $p(\boldsymbol{a} | \boldsymbol{o}) = \sigma(\text{MLP}(\phi(E(\boldsymbol{a}), E_{\text{scene}}) + E_{\text{navi}} + E_{\text{state}}))$
- 分布损失: $\mathcal{L}_{\text{distribution}} = -\sum p_{\text{data}}(\boldsymbol{a}) \cdot \log p_{\text{pred}}(\boldsymbol{a})$
- 冲突损失: $\mathcal{L}_{\text{conflict}} = \sum \mathbb{1}_{\text{conflict}}(\boldsymbol{a}) \cdot \log p_{\text{pred}}(\boldsymbol{a})$

### 术语表
| 英文 | 中文 |
|------|------|
| Probabilistic Planning | 概率规划 |
| Planning Vocabulary | 规划词表 |
| Planning Token | 规划令牌 |
| Scene Token | 场景令牌 |
| Probabilistic Field | 概率场 |
| Distribution Loss | 分布损失 |
| Conflict Loss | 冲突损失 |
| Driving Demonstrations | 驾驶演示 |

### 参考资源
- **论文原文**: [arXiv 2402.13243](https://arxiv.org/abs/2402.13243)
- **代码实现**: [github.com/hustvl/VAD](https://github.com/hustvl/VAD)
- **翻译 PDF**: `AD-research/VADv2/VADv2_zh.pdf`

---

**报告生成说明**: 本报告基于对 LaTeX 源码的深度理解和翻译后的 PDF 文件整理而成，旨在提供论文的结构化总结和技术洞察。
