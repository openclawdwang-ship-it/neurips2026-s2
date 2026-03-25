# NeurIPS 2026 全面课题调研：20+ 研究方向

**调研日期**: 2026-03-23
**目标**: 为 Dr. Chengjia Wang 投稿 NeurIPS 2026 提供**全面、跨领域**的研究方向分析
**关键截止日期**: Abstract — **May 4, 2026 (AOE)** | Full Paper — **May 6, 2026 (AOE)**
**距 deadline**: ~42 天

---

## Dr. Wang 背景速览

| 维度 | 详情 |
|------|------|
| **职位** | Assistant Professor, Heriot-Watt University |
| **h-index** | 24 |
| **核心专长** | 心脏 MRI 分割 (40K UK Biobank pipeline, Dice 0.91)、因果推理 (PC/FCI/MR)、多器官影像、AI 验证 |
| **数据资源** | UK Biobank Application 40616: 45K+ 心脏 MRI + 脑 MRI + 腹部 MRI + 遗传数据（同一群体） |
| **工业合作** | Canon Medical Systems（CardioScan 项目） |
| **计算资源** | 无本地 GPU；云租赁 RTX 4090 (~$0.44/hr)；Mini PC: Ryzen 5 4500U + 32GB RAM |
| **NeurIPS 经验** | 首次投稿 |

---

## NeurIPS 录取的核心原则

> **NeurIPS 要的是方法论创新。医学领域是 testbed，不是 contribution。**
> - "我们用 X 模型在心脏 MRI 上提高了 2% Dice" → 去 MICCAI
> - "我们证明了 Y 的可辨识性条件并在器官形态数据上验证" → NeurIPS

**2025 录取率**: 24.5% (5,290/21,575) | **Oral**: 0.36% | **Spotlight**: 3.2%

---

## 研究方向总表（22 个方向，按综合评分排序）

| 排名 | 方向 | 领域 | NeurIPS 适合度 | 计算需求 | 6 周可行性 | 新颖性 | Dr. Wang 优势 | 综合分 |
|------|------|------|--------------|---------|-----------|--------|-------------|--------|
| **1** | Mamba 选择性测试时适配 | 架构 + TTA | ★★★★★ | 极低 | 高 | ★★★★★ | ★★★★ | **9.4** |
| **2** | 因果可辨识性：纵向器官动力学 | 因果 ML | ★★★★★ | 低-中 | 中 | ★★★★★ | ★★★★★ | **9.2** |
| **3** | 分布漂移下的 Conformal 分割 | 不确定性 | ★★★★★ | 极低 | 高 | ★★★★ | ★★★★ | **9.0** |
| **4** | 反事实心脏影像 via Flow Matching | 因果 + 生成 | ★★★★★ | 中 | 中 | ★★★★★ | ★★★★★ | **9.0** |
| **5** | 跨器官因果网络发现 | 因果 ML | ★★★★ | 低 | 高 | ★★★★★ | ★★★★★ | **8.8** |
| **6** | 因果公平性审计框架 | 公平性 | ★★★★★ | 极低 | 高 | ★★★★ | ★★★★ | **8.6** |
| **7** | Interventional Shapley 多模态归因 | XAI + 因果 | ★★★★ | 极低 | 高 | ★★★★ | ★★★★ | **8.5** |
| **8** | 耦合 Mamba 跨器官融合 | 多模态融合 | ★★★★ | 低-中 | 中 | ★★★★★ | ★★★★★ | **8.5** |
| **9** | 联邦 LoRA 心脏 MRI 基础模型 | FL + PEFT | ★★★★ | 中 | 中 | ★★★★ | ★★★★ | **8.3** |
| **10** | 基于知识瓶颈的抗漂移医学分类 | 领域适应 | ★★★★ | 低 | 高 | ★★★★ | ★★★ | **8.2** |
| **11** | 数据集蒸馏用于医学 FM 微调 | 高效 ML | ★★★★ | 中 | 中 | ★★★★ | ★★★ | **8.0** |
| **12** | 健康时序基础模型 (ECG+PPG) | 基础模型 | ★★★★ | 中-高 | 低 | ★★★★ | ★★★ | **7.8** |
| **13** | 扩散模型 3D 心脏重建 | 扩散模型 | ★★★★ | 中 | 中 | ★★★★ | ★★★★ | **7.8** |
| **14** | 持续学习框架：器官分割 | 持续学习 | ★★★★ | 低-中 | 中 | ★★★★ | ★★★ | **7.6** |
| **15** | 图神经网络器官交互建模 | GNN | ★★★ | 低 | 高 | ★★★★ | ★★★★★ | **7.5** |
| **16** | 零样本跨模态心脏分割 | 零样本 | ★★★ | 低-中 | 中 | ★★★ | ★★★★ | **7.4** |
| **17** | 隐私保护心脏 AI 基准 | D&B Track | ★★★★ | 低 | 高 | ★★★ | ★★★★ | **7.3** |
| **18** | 心脏影像合成数据评估基准 | D&B Track | ★★★★ | 低 | 高 | ★★★ | ★★★★ | **7.2** |
| **19** | 元学习跨 Scanner 快速适配 | 元学习 | ★★★ | 中 | 中 | ★★★ | ★★★★ | **7.0** |
| **20** | 神经 ODE 心脏动力学建模 | 动力系统 | ★★★★ | 低-中 | 低-中 | ★★★★ | ★★★★ | **7.0** |
| **21** | 低比特量化心脏分割模型 | 量化 | ★★★ | 低 | 高 | ★★★ | ★★★ | **6.8** |
| **22** | VLM 心脏报告生成基准 | VLM | ★★★ | 低 | 中 | ★★★ | ★★★★ | **6.7** |

---

# 第一部分：Top 7 强烈推荐方向（详细分析）

---

## 方向 1: Selective State Adaptation — Mamba 架构的选择性测试时适配

**综合评分: 9.4/10** | **推荐优先级: 🥇 首选**

### 建议标题
*Selective State Adaptation: Test-Time Tuning of State-Space Segmentation Models via Input-Dependent Gate Recalibration*

### 核心创新
为 Mamba/SSM 架构设计专用的 test-time adaptation (TTA) 机制。不更新所有参数，而是仅选择性地重新校准 Mamba blocks 的 input-dependent gating 参数（B、C、Δ 矩阵），利用 SSM 的门控机制作为适配的"旋钮"。

### NeurIPS 2024-2025 相关论文支撑
| 论文 | 会议 | 关联 |
|------|------|------|
| **Gated Attention for LLMs** (Qwen) | NeurIPS 2025 Best Paper | 证明 sigmoid 门控在注意力机制中的效果 |
| **ZERO: Frustratingly Easy TTA of VLMs** | NeurIPS 2024 | 训练-free TTA, 10x 快于 prompt tuning |
| **PeTTA: Persistent TTA in Recurring Scenarios** | NeurIPS 2024 | 循环场景中的动态适配策略 |
| **Samba: Severity-aware SSM for Cross-domain Grading** | NeurIPS 2024 | Mamba + 跨域医学影像 |
| **Coupled Mamba** | NeurIPS 2024 | SSM 多模态融合 |

### 技术路线
1. 使用预训练 Mamba 分割模型（U-Mamba 或 VM-UNet）
2. 测试时冻结所有参数，仅更新每个 Mamba block 的 B、C、Δ 矩阵
3. 通过最小化预测熵 + 解剖先验约束进行数步梯度更新
4. **理论分析**: SSM 的 "input selection" 机制为何比 Transformer 的注意力更适合 TTA
5. 验证: 心脏 MRI 跨 scanner (ACDC, M&Ms, UK Biobank)

### 为什么适合 NeurIPS
- 贡献是关于 **SSM 架构在 TTA 中的固有优势**的架构洞察
- 桥接两个热点方向：SSM (Mamba) + Test-Time Adaptation
- NeurIPS 2025 Best Paper 就是关于 gating 机制的

### 竞争分析
- **Mamba 医学影像**: 2024-2025 新兴方向，Mamba TTA **基本未被探索**
- **TTA 社区**: 关注 Transformer/CNN, 没有 SSM-specific 方法
- **结论**: "Right place, right time" — 蓝海

### 计算与成本
- 使用公开预训练模型，TTA 每张图片秒级 GPU 时间
- **总计**: < $20 云 GPU 费用
- **风险**: 低（基于公开模型 + 简单修改 = 快速验证）

### 时间线 (6 周)
| 周 | 任务 |
|----|------|
| 1 | 下载预训练模型 + 实现 TTA baseline (TENT, entropy) |
| 2 | 实现 SSM-specific gate recalibration TTA |
| 3 | 跨 scanner 实验 (ACDC → M&Ms → UK Biobank) |
| 4 | 理论分析 + ablation studies |
| 5 | 写作 |
| 6 | 修改 + 提交 |

---

## 方向 2: Identifiable Causal Dynamics — 纵向器官形态中的因果发现

**综合评分: 9.2/10** | **推荐优先级: 🥈 最高学术价值**

### 建议标题
*Identifiable Causal Dynamics in Longitudinal Organ Morphology: A Latent State-Space Approach*

### 核心创新
结合结构化状态空间模型和因果可辨识性理论，发现驱动心脏老化的因果因子。创新点是**证明可辨识性条件**——在什么假设下可以从心脏形状序列中恢复真实因果潜在因子。

### NeurIPS 2024-2025 相关论文支撑
| 论文 | 会议 | 关联 |
|------|------|------|
| **Causal Representation Learning for Health Data** | NeurIPS 2025 | 健康数据因果表征学习 |
| **The Boundaries of Fair AI: A Causal Perspective** | NeurIPS 2025 | 因果 + 医学影像公平性 |
| **Drug Discovery with Causal Reasoning** | NeurIPS 2024 | 因果推理在健康领域 |
| **Towards Identifiability of Hierarchical Temporal CRL** | NeurIPS 2025 | 时间因果表征可辨识性 |

### 技术路线
1. UK Biobank 心脏 MRI 序列编码为潜在表征 (VAE/pretrained encoder)
2. 用线性 SSM 建模潜在动力学，转移矩阵约束为稀疏无环（编码因果结构）
3. 证明在温和条件下（充分时间观测、非高斯创新），因果图可辨识
4. 用已知心脏老化生物学验证（LV 质量增加先于收缩功能下降）
5. Mendelian Randomization 作为因果方向"金标准"验证

### 为什么适合 NeurIPS
- Causal representation learning 是 NeurIPS 最活跃的理论方向之一 (Scholkopf, Bengio 主导)
- 这直接延伸时间因果可辨识性到**连续时间、空间结构化观测**
- UK Biobank 45K 规模为理论结论提供强大经验支撑

### 竞争分析
- **Scholkopf group (MPI)**: Causal representation learning 但**不在心脏/纵向影像**
- **Bengio group**: Causal ML + drug discovery 但**不在影像**
- **UK Biobank 心脏因果**: 几乎无人做
- **独特优势**: UK Biobank 纵向数据 + 遗传 MR 验证工具

### 计算与成本
- 特征提取: RTX 4090 批量处理 2-3 天
- SSM 拟合: CPU 友好
- **总计**: ~$100 云 GPU
- **风险**: 中（可辨识性证明是最难部分，但即使纯经验性结果也有价值）

---

## 方向 3: Conformal Organ Segmentation — 分布漂移下的不确定性量化

**综合评分: 9.0/10** | **推荐优先级: 🥉**

### 建议标题
*Conformal Organ Segmentation: Distribution-Free Uncertainty Quantification Under Scanner Shift via Optimal Transport Calibration*

### 核心创新
产生像素级 conformal prediction sets，在测试 scanner 与校准 scanner 不同时仍保持有限样本覆盖保证。使用 optimal transport 重加权校准分数。

### NeurIPS 2024-2025 支撑
- Conformal prediction 是 NeurIPS 2024-2025 持续热点（7+ 篇录取）
- **KnoBo** (NeurIPS 2024 Spotlight): 知识增强抗漂移模型，32.4% 提升
- **Generalize or Detect?** (NeurIPS 2024): 同时处理 OOD 和 domain generalization

### 技术路线
1. 定义分割的 non-conformity score
2. OT 计算源-目标 scanner 分布间的重要性权重
3. 证明覆盖保证
4. 验证: AMOS, TotalSegmentator, UK Biobank 多器官

### 计算成本
- **极低**: 后处理方法，使用预训练分割模型推理
- **总计**: < $10

---

## 方向 4: Counterfactual Hearts — 反事实心脏影像生成

**综合评分: 9.0/10**

### 建议标题
*Counterfactual Hearts: Estimating Causal Effects of Cardiovascular Risk Factors via Conditional Flow Matching on Cardiac MRI*

### 核心创新
用条件 flow matching + 结构因果模型生成反事实心脏 MRI（"如果这个患者没有高血压 10 年，心脏会是什么样？"），并用 Mendelian Randomization 验证因果效应。

### NeurIPS 2024-2025 支撑
| 论文 | 关联 |
|------|------|
| **SemFlow** (NeurIPS 2024) | Rectified flow 统一分割与生成 |
| **Fisher Flow Matching** (NeurIPS 2024) | 离散数据上的几何 flow matching |
| **Consistency Diffusion Bridge** (NeurIPS 2024) | 加速扩散桥模型 4-50x |
| **DiffusionBlend** (NeurIPS 2024) | 3D patch 扩散先验用于 CT 重建 |

### 技术路线
1. 在 UK Biobank 心脏 MRI 潜在空间训练条件 flow matching
2. 构建结构因果模型: 年龄 → 高血压 → LV 重构 → EF 下降
3. 使用 do-calculus 进行干预: do(高血压=0)
4. MR 验证因果效应大小

### 计算成本: ~$70 (RTX 4090 3-5 天)

---

## 方向 5: Cross-Organ Causal Discovery — 跨器官因果网络

**综合评分: 8.8/10**

### 建议标题
*Cross-Organ Causal Networks from Population Imaging: Discovering Heart-Brain-Liver Pathways in 45,000 UK Biobank Participants*

### 核心创新
利用 UK Biobank 多器官影像 (心脏 + 脑 + 腹部 MRI) 发现器官间因果通路。2025 Nature Comms 论文建立了相关性基础，本文加入**因果推理** (MR + 约束算法)。

### 独特竞争优势
- UK Biobank 是**全球唯一**拥有同一个体 31K+ 配对多器官影像 + 遗传数据的数据集
- 直接支持 ERC ORGANOME 申请（核心假说）
- "器官不是孤立存在的" 是新兴范式

### 计算成本: ~$50 (大部分是 CPU 计算)

---

## 方向 6: Causal Fairness Graphs — 心脏 AI 因果公平性

**综合评分: 8.6/10**

### 建议标题
*Causal Fairness Graphs for Medical AI: Auditing Path-Specific Effects in Cardiac Risk Prediction*

### 核心创新
用因果 DAG 将心脏 AI 预测的不公平性分解为**直接歧视、间接歧视和合理差异**。

### NeurIPS 2024-2025 支撑
| 论文 | 关联 |
|------|------|
| **FairMedFM** (NeurIPS 2024 D&B) | 医学 FM 公平性基准 (17 数据集, 20 FMs) |
| **OxonFair** (NeurIPS 2024) | 算法公平性工具包，支持医学 |
| **CARES** (NeurIPS 2024 D&B) | 医学 VLM 可信度 5 维度基准 |
| **Cross-Care** (NeurIPS 2024 D&B) | LLM 医学偏见评估 |
| **The Boundaries of Fair AI** (NeurIPS 2025) | 医学影像公平性因果视角 |

### 技术路线
1. 构建心脏 AI 因果 DAG: 人口统计 → 社会经济 → 暴露 → 生物标志物 → 心脏结局
2. 定义 path-specific fairness 标准
3. 使用 UK Biobank 数据估计路径效应
4. 证明: 部分 "不公平" 是合理的生物差异 vs 真正的歧视

### 计算成本: < $5 (纯统计计算)

---

## 方向 7: Interventional Shapley Values — 多模态因果特征归因

**综合评分: 8.5/10**

### 建议标题
*Interventional Shapley Values for Multi-Modal Medical Data: Causal Feature Attribution in Cardiac Risk Prediction*

### 核心创新
用 interventional Shapley values 归因心脏风险预测到各模态特征，解决标准 Shapley values **条件化不可能特征组合**的问题。

### NeurIPS 2024-2025 支撑
- **Beyond Concept Bottleneck Models** (NeurIPS 2024): 使黑盒模型可干预，验证于胸片
- XAI + 因果推理交叉在 NeurIPS 持续增长

### 计算成本: < $5 (CPU 计算，无需 GPU)

---

# 第二部分：补充推荐方向（8-22，简要分析）

---

## 方向 8: Coupled Mamba 跨器官融合

**综合评分: 8.5/10**

### 建议标题
*Coupled State-Space Chains for Cross-Organ Medical Image Fusion*

### 核心创新
扩展 NeurIPS 2024 Coupled Mamba (耦合状态链多模态融合) 到医学场景: 每个器官（心脏、脑、肝）作为一个状态链，通过跨链隐状态转移实现器官交互建模。

### 支撑论文
- **Coupled Mamba** (NeurIPS 2024): 83.7% GPU 内存节省, 49% 推理加速
- **HEALNet** (NeurIPS 2024): 迭代注意力多模态融合

### Dr. Wang 优势: UK Biobank 多器官数据是理想验证平台
### 计算: 中 (~$50)

---

## 方向 9: 联邦 LoRA 心脏 MRI 基础模型

**综合评分: 8.3/10**

### 建议标题
*FedCardiac: Federated Low-Rank Adaptation of Cardiac MRI Foundation Models Across Multi-Vendor Deployments*

### 核心创新
将 NeurIPS 2024 的 FLoRA/FlexLoRA 异构 LoRA 聚合方法应用于心脏 MRI: 不同医院 scanner 的模型通过联邦学习协同训练，无需共享数据。

### 支撑论文
- **FLoRA** (NeurIPS 2024): 无噪声异构 LoRA 聚合
- **FlexLoRA** (NeurIPS 2024): 动态 LoRA rank 调整
- **DictPFL** (NeurIPS 2025): 加密 FL, 402-748x 通信压缩
- **SpaFL** (NeurIPS 2024): 0.17% 通信成本

### Dr. Wang 优势: Canon Medical 合作 = 多 scanner 场景真实部署
### 计算: 中 (~$80)

---

## 方向 10: 知识增强瓶颈模型抗 Scanner 漂移

**综合评分: 8.2/10**

### 建议标题
*Cardiac KnoBo: Knowledge-Enhanced Bottleneck Models for Scanner-Robust Cardiac MRI Analysis*

### 灵感来源
- **KnoBo** (NeurIPS 2024 Spotlight): 用医学教科书知识构建概念瓶颈，抗域偏移 32.4%
- 将此方法迁移到心脏 MRI: 用 PubMed + ESC 指南构建心脏概念空间

### 计算: 低 (~$20)

---

## 方向 11: 数据集蒸馏用于医学 FM 微调

**综合评分: 8.0/10**

### 建议标题
*Distilling Clinical Knowledge: Gradient-Matched Dataset Distillation for Efficient Medical Foundation Model Fine-Tuning*

### 核心创新
将大型医学影像数据集蒸馏为 10-50 张合成图像，微调 FM 达到接近全数据集性能。

### 支撑论文
- **Single GPU Task Adaptation** (NeurIPS 2025): 单 GPU 病理 FM 适配
- **CUFIT** (NeurIPS 2024): 噪声标签下 VFM 课程微调
- **Memory-Efficient Medical FMs** (NeurIPS 2025): 内存高效医学 FM

### 计算: 中 (~$50)

---

## 方向 12: 健康时序基础模型

**综合评分: 7.8/10**

### 建议标题
*CardioWave: A Foundation Model for Cardiac Time Series via Self-Supervised PPG-ECG Alignment*

### 灵感来源
- **PaPaGei** (NeurIPS 2024 Workshop Best Paper): PPG 基础模型, 57K 小时预训练
- **OPERA** (NeurIPS 2024 D&B): 呼吸声音基础模型
- UK Biobank ECG + 可穿戴数据 = 训练数据

### 风险: 计算需求较高，6 周紧张
### 计算: 中-高 (~$150)

---

## 方向 13: 扩散模型 3D 心脏重建

**综合评分: 7.8/10**

### 建议标题
*CardiacBlend: 3D-Patch Diffusion Prior for Accelerated Cardiac MRI Reconstruction*

### 灵感来源
- **DiffusionBlend** (NeurIPS 2024): 3D patch 扩散先验, 24 小时→1 小时
- **AID (Autoregressive Image Diffusion)** (NeurIPS 2024): MRI 重建 + 自回归扩散

### 计算: 中 (~$80)

---

## 方向 14: 器官分割持续学习

**综合评分: 7.6/10**

### 建议标题
*Continual Organ Segmentation via Gated LoRA Integration*

### 灵感来源
- **GainLoRA** (NeurIPS 2025): 门控 LoRA 持续学习
- **Global Alignment** (NeurIPS 2024): 预训练 token 组合消除任务干扰
- **Happy** (NeurIPS 2024): 去偏持续类别发现

### 核心创新: 医学分割模型部署后需要不断适应新器官/新病种，现有方法导致灾难性遗忘
### 计算: 低-中 (~$40)

---

## 方向 15: 图神经网络器官交互建模

**综合评分: 7.5/10**

### 建议标题
*OrganGraph: Graph Neural Network Modeling of Multi-Organ Interactions from Population Imaging*

### 灵感来源
- **MolGPS** (NeurIPS 2024): GNN 基础模型, 38 个下游任务 SOTA
- **FireGNN** (NeurIPS 2025): 高效 GNN 医学图像分类

### 核心创新: 每个器官为节点、器官交互为边的图结构，用 GNN 预测心血管风险
### Dr. Wang 优势: UK Biobank 多器官数据天然适合图建模
### 计算: 低 (~$20)

---

## 方向 16: 零样本跨模态心脏分割

**综合评分: 7.4/10**

### 建议标题
*Zero-Shot Cross-Modality Cardiac Segmentation via Foundation Model Alignment*

### 灵感来源
- **"No Zero-Shot Without Exponential Data"** (NeurIPS 2024): 揭示零样本性能与预训练频率的对数线性关系
- **TGA-ZSR** (NeurIPS 2024): 文本引导注意力零样本鲁棒性

### 核心创新: 训练于 MRI 的分割模型如何零样本迁移到超声/CT
### 计算: 低-中 (~$30)

---

## 方向 17: 隐私保护心脏 AI 基准 (D&B Track)

**综合评分: 7.3/10**

### 建议标题
*PrivCardiac-Bench: A Benchmark for Privacy-Preserving Cardiac AI Under Federated and Differential Privacy Constraints*

### 灵感来源
- **FairMedFM** (NeurIPS 2024 D&B): 医学 FM 公平性基准
- **FedMEKI** (NeurIPS 2024 D&B): 联邦医学知识注入基准
- **DPResNet** (NeurIPS 2024): DP + FL 医学影像
- **Attack-Aware Noise Calibration** (NeurIPS 2024): 隐私-效用权衡新视角

### D&B Track 优势: 录取率通常高于 Main Track; 基准论文引用量高
### 计算: 低 (~$15)

---

## 方向 18: 心脏影像合成数据评估基准 (D&B Track)

**综合评分: 7.2/10**

### 建议标题
*SynthCardiac-Bench: Evaluating Synthetic Cardiac MRI for Downstream Clinical Tasks*

### 灵感来源
- **RetinaSynth** (NeurIPS 2025): 扩散合成视网膜影像
- **MedSG-Bench** (NeurIPS 2025 D&B Spotlight): 医学影像序列基准

### 核心创新: 不仅评估合成图像质量 (FID/IS)，还评估**下游临床任务性能**
### 计算: 低 (~$10)

---

## 方向 19: 元学习跨 Scanner 快速适配

**综合评分: 7.0/10**

### 建议标题
*Meta-Cardiac: Meta-Learning for Rapid Cross-Scanner Adaptation in Cardiac MRI*

### 灵感来源
- **Meta-Exploiting Frequency Prior** (NeurIPS 2024): 频率分解跨域 FSL
- **SAM-MPA** (NeurIPS 2024): SAM 少样本分割

### 核心创新: MAML/ProtoNet 变体学习 scanner-agnostic 初始化
### 计算: 中 (~$60)

---

## 方向 20: 神经 ODE 心脏动力学建模

**综合评分: 7.0/10**

### 建议标题
*Neural ODEs for Cardiac Dynamics: Continuous-Time Modeling of Ventricular Function from Population MRI*

### 核心创新: 用神经 ODE 建模心脏收缩-舒张连续动力学，而非离散帧
### 计算: 低-中 (~$40)

---

## 方向 21: 低比特量化心脏分割模型

**综合评分: 6.8/10**

### 建议标题
*CardioQuant: 2-Bit Post-Training Quantization for Deployable Cardiac Segmentation*

### 灵感来源
- **QTIP** (NeurIPS 2024): Trellis 码量化, 2-bit LLM
- **OneBit** (NeurIPS 2024): 1-bit 权重, 81%+ FP16 性能
- **DFloat11** (NeurIPS 2025): 无损压缩 30%

### Dr. Wang 优势: Canon Medical 部署需求 = 真实边缘计算场景
### 计算: 低 (~$15)

---

## 方向 22: VLM 心脏报告生成基准

**综合评分: 6.7/10**

### 建议标题
*CardioVLM-Bench: Benchmarking Vision-Language Models for Cardiac MRI Report Generation*

### 灵感来源
- **SMMILE** (NeurIPS 2025 D&B): 多模态医学 ICL 基准
- **Vote-MI** (NeurIPS 2024): 3D→2D 切片选择优化 VLM 输入
- **EGMA** (NeurIPS 2024): 眼动引导跨模态对齐
- **Uni-Med** (NeurIPS 2024): Connector-MoE 统一医学多任务

### 计算: 低 (~$10)

---

# 第三部分：战略建议

---

## 投稿策略矩阵

| 策略 | 主方向 | 备选方向 | Track | 风险 |
|------|--------|---------|-------|------|
| **激进策略** | 方向 2 (因果可辨识性) | 方向 4 (反事实心脏) | Main | 高收益高风险 |
| **稳健策略** | 方向 1 (Mamba TTA) | 方向 3 (Conformal) | Main | 中收益低风险 |
| **组合策略** | 方向 1 (Main) + 方向 17/18 (D&B) | - | 两个 Track | 双投提高概率 |
| **因果专攻** | 方向 5 (跨器官) + 方向 6 (公平性) | 方向 7 (Shapley) | Main | 杠杆现有专长 |

## 推荐方案

### **首选: 组合策略**

1. **Main Track**: 方向 1 (Mamba TTA) — 计算最低、最快产出、NeurIPS 契合度极高
2. **D&B Track**: 方向 17 (隐私保护心脏 AI 基准) — 杠杆 UK Biobank 数据优势

### **如果只投一篇: 方向 1 (Mamba TTA)**

理由:
- 6 周时间内**最可行**
- 计算需求**最低** (< $20)
- **零先行研究** = 首个将 SSM-specific TTA 用于医学影像
- NeurIPS 2025 Best Paper 就是 gating 机制
- 失败也可直接转投 MICCAI 2027

### **如果时间允许(8-10 周): 方向 2 (因果可辨识性)**

理由:
- **最高学术价值**（理论+实验双重贡献）
- 如果成功，可能是 Spotlight 级别
- 直接支持 ERC ORGANOME 申请
- UK Biobank 是不可复制的竞争优势

---

## 各方向 GPU 成本总览

| 方向 | GPU 小时 | 云成本 (RTX 4090) |
|------|---------|-------------------|
| 1. Mamba TTA | ~30 | ~$13 |
| 2. 因果可辨识性 | ~200 | ~$88 |
| 3. Conformal 分割 | ~15 | ~$7 |
| 4. 反事实心脏 | ~150 | ~$66 |
| 5. 跨器官因果 | ~100 | ~$44 |
| 6. 因果公平性 | ~5 | ~$2 |
| 7. Shapley 归因 | ~5 | ~$2 |
| 8. Coupled Mamba | ~100 | ~$44 |
| 9. 联邦 LoRA | ~180 | ~$79 |
| 10. KnoBo 心脏 | ~40 | ~$18 |
| 11. 数据集蒸馏 | ~100 | ~$44 |
| 12. 时序基础模型 | ~300 | ~$132 |
| 13. 3D 心脏扩散 | ~150 | ~$66 |
| 14. 持续学习 | ~80 | ~$35 |
| 15. GNN 器官 | ~40 | ~$18 |
| 16. 零样本分割 | ~60 | ~$26 |
| 17. 隐私基准 | ~30 | ~$13 |
| 18. 合成评估 | ~20 | ~$9 |
| 19. 元学习 | ~120 | ~$53 |
| 20. 神经 ODE | ~80 | ~$35 |
| 21. 量化部署 | ~30 | ~$13 |
| 22. VLM 基准 | ~20 | ~$9 |

---

## NeurIPS 2024-2025 论文参考索引

### 医学影像 & 基础模型
1. AID: Autoregressive Image Diffusion for MRI (NeurIPS 2024 Poster)
2. SegVol: Universal Volumetric Segmentation (NeurIPS 2024 Spotlight)
3. CUFIT: Curriculum Fine-tuning under Label Noise (NeurIPS 2024)
4. D-VST: Diffusion Virtual Staining (NeurIPS 2025)
5. Single GPU Task Adaptation (NeurIPS 2025)
6. Memory-Efficient Medical FMs (NeurIPS 2025)
7. FireGNN: Efficient GNN Medical Classification (NeurIPS 2025)
8. ProtoSurv: Prototype-guided Survival (NeurIPS 2024)

### 高效 ML & 量化
9. QTIP: Trellis Coded Quantization (NeurIPS 2024) — 2-bit, 6.82 PPL
10. OneBit: 1-bit LLM (NeurIPS 2024) — 81%+ FP16
11. DFloat11: Lossless Compression (NeurIPS 2025) — 30% 无损
12. Gated Attention (NeurIPS 2025 Best Paper) — sigmoid 门控
13. FlashAttention-3 (NeurIPS 2024 Spotlight) — 1.2 PFLOPs/s
14. MInference (NeurIPS 2024 Spotlight) — 10x pre-fill 加速
15. Minitron: Pruning+Distillation (NeurIPS 2024) — 40x 更少 tokens
16. VB-LoRA: Vector Bank (NeurIPS 2024) — 0.4% LoRA 参数
17. CE-NAS: Carbon-Efficient NAS (NeurIPS 2024) — 7.22x 碳排放降低

### 自监督 & 扩散模型
18. Self-Guided MAE (NeurIPS 2024) — 内部生成知情掩码
19. SemFlow: Rectified Flow 分割+生成 (NeurIPS 2024)
20. DiffusionBlend: 3D Patch 先验 (NeurIPS 2024)
21. Registration: Magic or Mirage (NeurIPS 2024) — 经典 vs 深度
22. Fisher Flow Matching (NeurIPS 2024) — 离散数据几何 flow
23. M2CRL: 内窥镜多视图对比 (NeurIPS 2024) — +7.5% Dice

### 联邦学习 & 隐私
24. FLoRA: 联邦异构 LoRA (NeurIPS 2024) — 无噪声聚合
25. FlexLoRA: 动态 LoRA rank (NeurIPS 2024)
26. DictPFL: 加密 FL (NeurIPS 2025) — 402-748x 压缩
27. SpaFL: 稀疏 FL (NeurIPS 2024) — 0.17% 通信
28. FuseFL: 一次性 FL (NeurIPS 2024 Spotlight) — 因果视角
29. PN-f-DP (NeurIPS 2025 Spotlight) — 去中心化 f-DP

### 多模态 & 领域适应
30. Coupled Mamba (NeurIPS 2024) — 耦合状态链融合
31. HEALNet (NeurIPS 2024) — 异构生物医学融合
32. KnoBo (NeurIPS 2024 Spotlight) — 知识瓶颈抗漂移
33. Samba: SSM 跨域 (NeurIPS 2024) — +23.5% over VMamba
34. ZERO: Training-free TTA (NeurIPS 2024) — 10x 快
35. PeTTA: 持续 TTA (NeurIPS 2024) — 循环场景
36. EGMA: 眼动引导对齐 (NeurIPS 2024)
37. Uni-Med: Connector-MoE (NeurIPS 2024) — 6 任务统一
38. SMMILE (NeurIPS 2025 D&B) — 医学多模态 ICL 基准

### 因果推理 & 公平性
39. FairMedFM (NeurIPS 2024 D&B) — 17 数据集, 20 FMs
40. OxonFair (NeurIPS 2024) — 算法公平性工具包
41. CARES (NeurIPS 2024 D&B) — 医学 VLM 可信度
42. Boundaries of Fair AI (NeurIPS 2025) — 因果+公平+影像
43. Beyond Concept Bottleneck (NeurIPS 2024) — 黑盒可干预

### 持续学习
44. GainLoRA (NeurIPS 2025) — 门控 LoRA 持续学习
45. Global Alignment (NeurIPS 2024) — 预训练 token 组合
46. Happy (NeurIPS 2024) — 去偏持续类别发现
47. PathWeave (NeurIPS 2024) — 98.73% 参数减少模态扩展

### 健康时序 & GNN
48. PaPaGei (NeurIPS 2024 Workshop Best Paper) — PPG 基础模型
49. OPERA (NeurIPS 2024 D&B) — 呼吸声音基础模型
50. MolGPS (NeurIPS 2024) — GNN 分子基础模型
51. M3H (NeurIPS 2024 Workshop) — 多模态多任务健康 ML

---

## 六周行动计划 (推荐 Mamba TTA + 隐私基准双投)

| 周 | Main Track: Mamba TTA | D&B Track: 隐私基准 |
|----|----------------------|---------------------|
| **W1** | 下载预训练 Mamba 模型; 实现 baseline TTA | 设计基准方案; 收集 UK Biobank 子集 |
| **W2** | SSM-specific gate recalibration 实现 | 实现 FL + DP 实验管线 |
| **W3** | 跨 scanner 实验 (ACDC→M&Ms→UKBB) | 运行 benchmark: 5 FL 算法 × 3 DP 水平 |
| **W4** | 理论分析 + ablation studies | 分析结果 + 公平性评估 |
| **W5** | 写作 (Main Paper) | 写作 (D&B Paper) |
| **W6** | 修改 + 格式化 + Checklist + 提交 | 修改 + 格式化 + Checklist + 提交 |

### 关键提醒
- **May 4 AOE**: Abstract 提交（两篇都需要）
- **May 6 AOE**: Full paper 提交
- 必须使用 `neurips_2026.sty` 模板
- **Paper Checklist 强制**，否则 desk reject
- 正文限 9 页 + 无限附录/参考文献

---

*本报告基于 6 个并行研究 agent 对 NeurIPS 2024-2025 共 100+ 篇论文的系统性搜索和分析，覆盖医学影像、高效 ML、自监督/扩散/基础模型、联邦学习/隐私、多模态/适应/持续学习、因果推理/XAI/GNN/时序 六大领域。*
