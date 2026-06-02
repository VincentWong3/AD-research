# Paper Context for Translation

## Title
ST-P3: End-to-end Vision-based Autonomous Driving via Spatial-Temporal Feature Learning
→ ST-P3：基于时空特征学习的端到端视觉自动驾驶

## Abstract
Many existing autonomous driving paradigms involve a multi-stage discrete pipeline of tasks. To better predict the control signals and enhance user safety, an end-to-end approach that benefits from joint spatial-temporal feature learning is desirable...
→ 许多现有的自动驾驶范式采用多阶段离散任务流程。为了更好地预测控制信号并提升用户安全性，需要一种能够从联合时空特征学习中受益的端到端方法。

## Paper Structure
1. Introduction (sec:intro)
2. Related Work (sec:related work) - Interpretable E2E Framework, BEV Representation, Future Prediction, Motion Planning
3. Methodology (sec:method)
   - 3.1 Perception: Egocentric Aligned Accumulation (sec:method-perception)
   - 3.2 Prediction: Dual Pathway Probabilistic Future Modelling (sec:method-prediction)
   - 3.3 Planning: Prior Knowledge Incorporation and Refinement (sec:method-plan)
   - 3.4 Overall Loss for End-to-End Learning (sec:method-e2e learning)
4. Experiments (sec:experiments)
   - 4.1 Open-loop Results on nuScenes (sec:res-nuscenes)
   - 4.2 Closed-loop Results on CARLA (sec:res-carla)
   - 4.3 Ablation Study (sec:exp-ablation)
5. Conclusions
6. Appendix (sup_main_chapter.tex)
   - Implementation Details
   - Depth Supervision
   - Additional Experiment Results

## Key Terminologies (术语表)

| English | 中文 | Notes |
|---------|------|-------|
| ST-P3 | ST-P3 | (保留) |
| Egocentric Aligned Accumulation (EAA) | 自我中心对齐累积 | |
| Dual Pathway Modelling | 双路径建模 | |
| Prior Knowledge Incorporation and Refinement | 先验知识融合与优化 | |
| Spatial-temporal | 时空 | 注意空格 |
| End-to-end | 端到端 | 注意连字符 |
| Bird's eye view (BEV) | 鸟瞰图 (BEV) | 首次出现写全，后续用BEV |
| Perception | 感知 | |
| Prediction | 预测 | |
| Planning | 规划 | / 规划模块 |
| Self-driving vehicle (SDV) | 自动驾驶车辆 (SDV) | |
| High-definition (HD) map | 高清地图 (HD map) | |
| LiDAR | LiDAR | (保留) |
| Deep learning | 深度学习 | |
| Backbone | 主干网络 | |
| Depth estimation | 深度估计 | |
| BEV transformation | BEV变换 | |
| GRU (Gated Recurrent Unit) | GRU（门控循环单元） | |
| Cost volume | 代价体 | |
| Cost map | 代价图 | |
| Trajectory sampler / Sampler | 轨迹采样器 / 采样器 | |
| Trajectory | 轨迹 | |
| Waypoint | 路径点 | |
| Semantic segmentation | 语义分割 | |
| Instance segmentation | 实例分割 | |
| Intersection-over-Union (IoU) | 交并比 (IoU) | |
| Collision rate | 碰撞率 | |
| Open-loop | 开环 | |
| Closed-loop | 闭环 | |
| nuScenes | nuScenes | (保留, 数据集名) |
| CARLA | CARLA | (保留, 模拟器名) |
| Ego-motion | 自车运动 | |
| Ego-centric / Egocentric | 自我中心 | |
| Front-view features | 前视图特征 | |
| Temporal model / Temporal fusion | 时序模型 / 时序融合 | |
| Uncertainty distribution | 不确定性分布 | |
| Gaussian distribution | 高斯分布 | |
| Bernoulli distribution | Bernoulli分布 | |
| L2 error / L2 distance | L2误差 / L2距离 | |
| Route Completion (RC) | 路线完成率 (RC) | |
| Driving Score (DS) | 驾驶得分 (DS) | |
| Ablation study | 消融实验 | |
| State-of-the-art (SOTA) | 最先进方法 (SOTA) | |
| Margin loss / Max-margin loss | 间隔损失 / 最大间隔损失 | |
| Panoptic Quality (PQ) | 全景质量 (PQ) | |
| Recognition Quality (RQ) | 识别质量 (RQ) | |
| Segmentation Quality (SQ) | 分割质量 (SQ) | |
| EfficientNet-B4 | EfficientNet-B4 | (保留) |
| ResNet-18 | ResNet-18 | (保留) |
| Convolutional Neural Network (CNN) | 卷积神经网络 (CNN) | |
| 3D convolution | 3D卷积 | |
| Reinforcement Learning (RL) | 强化学习 (RL) | |
| Imitation Learning (IL) | 模仿学习 (IL) | |
| Perspective view | 透视图 / 视角视图 | |
| Occupancy map / Occupancy grid | 占用图 / 占用网格 | |
| Decoder | 解码器 | |
| Hidden state | 隐状态 | |
| BEV feature | BEV特征 | |
| Spatial fusion | 空间融合 | |
| Temporal fusion | 时序融合 | |
| Ego-vehicle | 自车 | |
| High-level command | 高层指令 / 高级指令 | left/right/forward |
| Prior knowledge | 先验知识 | |
| Refinement | 优化 / 精化 | |
| Agent | 智能体 | |
| Frontier-view | 前视图 | |
| Safety cost | 安全代价 | |
| Comfort / Smoothness | 舒适性 / 平滑性 | |
| Progress cost | 进度代价 | |
| Bicycle model | 自行车模型 | |
| Frenet frame | Frenet坐标系 | |
| Top-k cross-entropy loss | top-k交叉熵损失 | |
| Mixture Gaussian | 混合高斯 | |
| Residual block | 残差块 | |
| Average pooling | 平均池化 | |
| Skip connection | 跳跃连接 | |
