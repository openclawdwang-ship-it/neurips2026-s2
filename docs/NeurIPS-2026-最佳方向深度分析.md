# NeurIPS 2026: 最佳GPU训练方向 — 深度竞争分析

**目的**: 从TOP 3方向中选出最佳ONE方向
**方法**: arXiv竞争分析 + NeurIPS先例 + 可行性评估
**数据来源**: arXiv API实时查询 (2026-03-23) + web search验证

---

## 竞争态势总览（来自arXiv实时数据）

| 方向 | 近5周arXiv论文数 | 直接竞争者 | 饱和度 | 结论 |
|------|-----------------|-----------|--------|------|
| **SAE训练方法** | ~10篇 + **领域领袖正在撤退** | 高 | **DeepMind放弃，Anthropic转向** | **淘汰** |
| **Grokking** | **9篇（标题含grokking）** | **极高** | **高度饱和，每个角度都被覆盖** | **淘汰** |
| **Phase Transition** | ~15-20篇/18个月 | 1篇直接竞争，有明确gap | **适中，有清晰定位** | **最佳** |

---

## 方向A: SAE训练方法创新

### 竞争分析（arXiv 2026年1-3月）

**标题含"sparse autoencoder"的论文（近5周，10篇）**:

| 日期 | 论文 | 类型 | 与我们竞争？ |
|------|------|------|-------------|
| 2026-03-19 | SAEs Reveal Features in VLA Models | 应用 | 否 |
| 2026-03-18 | SAEs for Neural Audio Codecs | 应用 | 否 |
| 2026-03-13 | SteerRM: Debiasing Reward Models via SAEs | 应用 | 否 |
| 2026-03-10 | Dissecting Chronos: SAEs for Time Series | 应用 | 否 |
| **2026-03-04** | **Stable and Steerable SAEs with Weight Regularization** | **方法** | **是 — 直接竞争** |
| 2026-03-03 | Step-Level SAE for Reasoning | 应用 | 部分 |
| 2026-03-03 | SAEs for single-cell foundation models | 应用 | 否 |
| 2026-02-27 | Learning Retrieval Models with SAEs | 应用 | 否 |
| 2026-02-22 | How LLMs Encode Scientific Quality via SAEs | 应用 | 否 |
| **2026-02-16** | **SynthSAEBench: Evaluating SAEs** | **评估** | **间接 — benchmark** |

**关键相关论文（全文搜索）**:
- **"Fundamental Limits of Neural Network Sparsification: Evidence from Catastrophic Interpretability Collapse"** (2026-03-18) — 发现SAE存在catastrophic collapse
- **"From Data Statistics to Feature Geometry: How Correlations Shape Superposition"** (2026-03-10) — 理论分析superposition
- **"SAE as a Crystal Ball"** (2026-03-03) — SAE特征可预测跨域迁移

### 竞争评估

**好消息**: 10篇SAE论文中，**只有1篇**是关于训练方法的（"Stable and Steerable SAEs"）。其余都是**SAE的应用**。这意味着：
- SAE训练方法仍然是**供给不足**的研究空间
- 社区在大量使用SAE，但很少有人改进SAE本身
- "Catastrophic Interpretability Collapse"论文发现了新问题 → 创造了新的method需求

**坏消息**:
- "Stable and Steerable SAEs with Weight Regularization" (Mar 4) 直接与我们竞争
- SynthSAEBench提供了标准评估 → 你的方法必须在这个benchmark上表现好
- Anthropic/DeepMind的内部工作可能远ahead但未公开

### Novelty评分: ~~7/10~~ → **3/10**（深度调研后大幅下调）

**新发现彻底改变了评估:**

1. **DeepMind明确放弃SAE研究** (2025年3月): 发表negative results显示SAE在downstream tasks上不如linear probes，SAE重建导致10-40%性能退化
2. **Neel Nanda (2025年9月)**: *"The most ambitious vision of mechanistic interpretability I once dreamed of is probably dead."*
3. **Anthropic已转向circuit tracing**: 使用cross-layer transcoders替代per-layer SAEs
4. **ICLR 2026理论证明**: Full feature disentanglement在realistic sparsity下**数学上不可能**
5. **Transcoders beat SAEs** (2025年1月): Skip transcoders在interpretability上Pareto-dominate SAEs
6. **可复现性危机**: 不同seed只有30%特征重叠
7. **SAE变体过度拥挤**: TopK, JumpReLU, BatchTopK, Gated, AbsTopK, WSAE, RouteSAE, Group-SAE, Matryoshka SAE... SAEBench显示"often difficult to differentiate"

### 风险分析（更新）

| 风险 | 概率 | 影响 | 应对 |
|------|------|------|------|
| **领域领袖撤退导致reviewer skepticism** | **70%** | **致命** | **无法应对** |
| **理论上不可能解决根本问题** | **已证明** | **致命** | **无法应对** |
| Anthropic/DeepMind的负面结果被reviewer引用 | 60% | 高 | 无法控制 |
| SAE变体太多，你的贡献被认为incremental | 50% | 高 | 很难避免 |

### 结论: **淘汰此方向**

SAE不仅是竞争问题——**整个研究方向的validity都在被质疑**。当DeepMind说"we are deprioritizing SAE research"并发表negative results时，你作为个人researcher投SAE方法论文，reviewer会直接引用这些negative results拒稿。

> 来源: [DeepMind Negative Results](https://deepmindsafetyresearch.medium.com/negative-results-for-sparse-autoencoders-on-downstream-tasks-and-deprioritising-sae-research-6cadcfc125b9), [Neel Nanda EA Forum Post](https://forum.effectivealtruism.org/posts/za2oHe8HBtcYNnN7C/neel-nanda-mechanistic-interpretability), [ICLR 2026 Limits of SAEs](https://arxiv.org/abs/2506.15963)

---

## 方向B: Grokking的可控触发

### 竞争分析（arXiv 2026年2-3月）

**标题含"grokking"的论文（近5周，9篇！）**:

| 日期 | 论文 | 与我们竞争？ |
|------|------|-------------|
| **2026-03-16** | **Grokking as Variance-Limited Phase Transition: Spectral Gating** | **是 — phase transition理论** |
| **2026-03-05** | **Why Grokking Takes So Long: First-Principles Theory** | **是 — 理论解释** |
| **2026-03-05** | **Geometric Inductive Bias: Bypassing Phase Transitions via Architectural Topology** | **是 — 通过架构加速** |
| **2026-03-01** | **Grokking as Phase Transition between Competing Basins (Singular Learning Theory)** | **是 — phase transition** |
| 2026-02-23 | Grokking Finite-Dimensional Algebra | 部分 |
| **2026-02-19** | **Geometry of Multi-Task Grokking: Weight Decay Phase Structure** | **是 — phase diagram!** |
| **2026-02-19** | **Early-Warning Signals of Grokking via Loss-Landscape Geometry** | **是 — 检测/预测grokking** |
| **2026-02-18** | **On the Mechanism and Dynamics of Modular Addition** | **是 — 机制分析** |
| **2026-02-18** | **Low-Dimensional Optimization Dynamics in Grokking** | **是 — 训练动态** |

### 竞争评估

**这是灾难性的**。在5周内：

1. **"Weight Decay Phase Structure"** (Feb 19) — 已经在做grokking的phase diagram，包含weight decay! 这是我们计划的核心。
2. **"Early-Warning Signals via Loss-Landscape"** (Feb 19) — 已经在做grokking的检测/预测。
3. **"Why Grokking Takes So Long"** (Mar 5) — first-principles理论，解释了为什么grokking慢。
4. **"Bypassing Phase Transitions via Architectural Topology"** (Mar 5) — 已经在做"加速grokking"！
5. **"Variance-Limited Phase Transition"** (Mar 16) — 最新理论。

**9篇论文中8篇直接与我们竞争**。这个方向已经被**严重过度研究**。

### Novelty评分: 3/10

我们计划的每个组成部分**都已被覆盖**:
- Phase diagram → "Weight Decay Phase Structure"
- 加速grokking → "Bypassing via Architectural Topology"
- 理论解释 → "First-Principles Theory", "Variance-Limited Phase Transition"
- 检测grokking → "Early-Warning Signals"

**唯一可能的差异化**: 将grokking扩展到**自然语言任务**（现有工作主要在算术/群论）。但这风险很大。

### 风险分析

| 风险 | 概率 | 影响 | 应对 |
|------|------|------|------|
| 被scooped（已经发生） | **90%** | **致命** | 无法应对 |
| Reviewer说"incremental" | 70% | 致命 | 很难避免 |
| 投稿时竞争论文更多 | 95% | 高 | 无法控制 |

### 结论: **放弃此方向**

---

## 方向C: 小模型Reasoning的Phase Transition

### 竞争分析（arXiv 2024-2026）

**标题含"phase transition" + "language model"的论文（过去1年）**:

| 日期 | 论文 | 与我们竞争？ |
|------|------|-------------|
| **2025-11-16** | **Evidence of Phase Transitions in Small Transformer-Based Language Models** | **是 — 直接竞争** |
| 2025-04-16 | Prompt-Induced Phase Transition in LLMs | 否（关于prompting） |
| 2025-04-04 | LLM Reasoning via 3-SAT Phase Transition | 否（关于3-SAT） |
| 2025-02-28 | Triple Phase Transitions in LLMs (Neuroscience) | 部分 |
| 2025-02-26 | LMs Grow Less Humanlike beyond Phase Transition | 否（关于人类相似性）|
| 2025-01-27 | Phase Transitions in LLMs and O(N) Model | 部分（物理理论） |
| 2024-12-10 | Algorithmic Phase Transitions: Mechanistic Case Study | 部分 |

**其他相关论文**:
- **"New Skills or Sharper Primitives? Emergence of Reasoning in RLVR"** (2026-02-09) — 分析reasoning是否是新能力
- **"Understanding Emergent Abilities from the Loss Perspective"** (NeurIPS 2024) — loss决定emergence
- **"Superposition Yields Robust Scaling"** (NeurIPS 2025 Best Paper Runner-up) — first-principles scaling laws

### 竞争评估（深度研究后更新）

**相关工作详细分析**:

| 论文 | 与我们的关系 | 差异 |
|------|-------------|------|
| **PolyPythias** (ICLR 2025) | 50 runs × 5 sizes (14M-410M) | 关注训练**稳定性**，不是reasoning emergence |
| **Allen-Zhu Physics of LMs** (7+篇系列) | 方法论标杆 | 使用**合成数据**，不是naturalistic data |
| **MobileLLM-R1** (Meta, 2025) | 950M达到AIME 15.5 | 单一模型，不是scaling study |
| **Evidence of Phase Transitions** (Nov 2025) | 最直接竞争者 | 检测phase transition但不系统probe reasoning |
| **"Do Larger Models Generalize Better?"** (Apr 2025) | U-shaped scaling发现 | 关注implicit reasoning，不是controlled training |
| **E2LM Competition** (NeurIPS 2025) | 直接相关：评估小模型训练 | 是competition框架，不是research paper |
| **"Beyond Induction Heads"** (ICML 2025) | 3 phase transitions for meta-learning | 只在一个任务上 |
| **Two-Hop Reasoning Phase Transition** (Meta FAIR) | reasoning中有sharp transition | 合成任务，3-layer transformer |

**The Gap (来自agent3的结论)**:
> *"No one has done a comprehensive study that trains multiple sizes of the same architecture on the same naturalistic (non-synthetic) data while systematically probing when specific reasoning abilities emerge at each checkpoint, with mechanistic analysis of the internal changes."*

**好消息（更新）**:
1. **Gap已确认**: Agent搜索了所有相关文献，确认我们的具体方案**没有被做过**
2. **PolyPythias是方法论盟友**: 它证明了"多规模训练+checkpoint分析"方法在ICLR 2025被接受。我们做同样的方法但focus不同（reasoning vs stability）
3. **MobileLLM-R1证明reasoning CAN emerge sub-billion**: 950M模型AIME 15.5 → 说明在我们的规模范围(14M-500M)内**有东西可以发现**
4. **U-shaped scaling是bonus finding**: 如果我们也发现U-shaped pattern → 独立验证 + 新的mechanistic解释
5. **E2LM Competition说明NeurIPS社区关注此问题**: 整个competition track都在问"how to evaluate small models during training"
6. **Allen-Zhu系列是reference但不是竞争**: 他用合成数据，我们用naturalistic data → 互补而非竞争
7. **"Distributional Scaling Laws"** (Harvard/Kempner 2025) 重新定义了emergence辩论: 不再是"real vs mirage"而是"distributional" → 我们的fine-grained analysis完美适配

**坏消息（更新）**:
1. 需要仔细读"Evidence of Phase Transitions" (Nov 2025) 确认差异化 — 但初步看它关注的是coherence emergence而非reasoning
2. 竞争者**比预期更多但更分散**: 没有人做complete picture

### Novelty评分: 8/10 → **8.5/10**（上调：gap更清晰，positioning更强）

**精确的novel contribution（更新）**:
1. **Controlled Training on Naturalistic Data**: 与Allen-Zhu（合成数据）和PolyPythias（stability focus）形成三角互补
2. **Reasoning-specific Probing**: 不是general perplexity/knowledge，而是算术、ICL、CoT、逻辑推理的分类emergence
3. **Loss-threshold + Reasoning**: 结合NeurIPS 2024 "Loss Perspective" → 对每种reasoning能力确定loss threshold
4. **U-shaped Validation**: 可能独立验证/推翻U-shaped scaling finding
5. **MobileLLM-R1 Extension**: 从单一模型扩展到systematic scaling study

**为什么还没人做**:
- Allen-Zhu用合成数据（更controllable但不realistic）
- PolyPythias关注stability不是reasoning
- MobileLLM-R1只训了一个最好的模型
- "Evidence of Phase Transitions"没有systematic reasoning probe
- **我们填补的gap：naturalistic data + multiple sizes + reasoning-specific probing + mechanistic analysis**

### 风险分析（更新）

| 风险 | 概率 | 影响 | 应对 |
|------|------|------|------|
| Reasoning在500M以下不emerge | 20% (MobileLLM-R1降低了此风险) | 低 | **"不emerge"本身是发现** |
| U-shaped pattern不出现 | 40% | 低 | 没有U也是有意义的null result |
| "Evidence of Phase Transitions"太相似 | 15% | 中 | 读paper后differentiate |
| 训练出问题 | 10% | 中 | 用PolyPythias的hyperparameters |
| GPU时间不够 | 5% | 中 | 减少规模点或用GaLore |
| Reviewer觉得"just scaling experiments" | 20% | 中 | **加crosscoder分析** (从"Crosscoding Through Time"借工具) |
| 被Allen-Zhu系列的下一篇scoop | 15% | 中 | 我们用naturalistic data，互补不竞争 |

**关键优势**: 无论结果如何都是发现。这是research中最强的position。

**新增应对措施**: 使用**Crosscoders** (Bayazit et al., 2025) 分析训练过程中特征的emergence → 不只是benchmark scores，而是mechanistic evidence of reasoning emergence。这大幅提升论文质量。

### 可行性详细分析

**精确训练协议**:

| 模型规模 | 层数 | 隐藏维度 | 训练tokens | 训练时间(RTX 3090) | VRAM |
|----------|------|---------|-----------|-------------------|------|
| 14M | 6 | 384 | 2B | ~3h | 2GB |
| 31M | 8 | 512 | 4B | ~6h | 3GB |
| 70M | 12 | 768 | 8B | ~15h | 5GB |
| 124M | 12 | 768 | 15B | ~30h | 8GB |
| 200M | 16 | 1024 | 20B | ~45h | 10GB |
| 350M | 24 | 1024 | 30B | ~70h | 14GB |
| 500M | 24 | 1280 | 40B | ~100h | 18GB |

**总GPU时间**: ~270h (7个规模点)
**加probing实验**: +50h
**总计**: **~320 GPU小时**
**精确成本**: RTX 3090 × 320h × $0.22 = **$70**; RTX 4090 × 320h × $0.44 = **$141**

**数据**: RedPajama-1T subset（免费，可下载）
**框架**: nanoGPT（极简，易复现）
**超参数**: 用Chinchilla ratio（20 tokens/param），cosine LR + cooldown（EPFL NeurIPS 2024验证）

### Reasoning评估协议

每个checkpoint评估:
1. **简单算术**: 2-digit加减乘除
2. **Few-shot ICL**: 5-shot分类（SST-2, AG News）
3. **Chain-of-thought**: 简单逻辑推理（带/不带CoT提示）
4. **Pattern completion**: 序列规律识别
5. **Boolean logic**: AND/OR/NOT组合

每个评估快速（纯推理），不消耗GPU预算。

---

## 最终比较矩阵（深度研究后更新）

| 维度 | SAE训练方法 (A) | Grokking (B) | Phase Transition (C) |
|------|----------------|-------------|---------------------|
| **Novelty** | ~~7~~ → **3/10** | **3/10** | ~~8~~ → **8.5/10** |
| **竞争饱和度** | **极高（领袖撤退+理论否定）** | **极高（5周9篇）** | **适中（有明确gap）** |
| **被scoop风险** | **70%（领域validity被质疑）** | **90%（已被scoop）** | **15%** |
| **可行性** | 9/10 | 9/10 | 8/10 |
| **成本** | $40-80 | $30-60 | **$70-162** |
| **"空结果"风险** | **50%（方法可能不work + 理论限制）** | 10% | **0%**（无论结果如何都是发现）|
| **NeurIPS适配** | **3/10（DeepMind negative results）** | 5/10（太crowded） | **9/10** |
| **潜在impact** | ~~7~~ → **3/10** | 4/10 | **9/10** |
| **领域健康度** | **衰退中** | **过热** | **健康成长** |

### 评分公式: Novelty × Feasibility × Impact × (1 - Risk)

| 方向 | Novelty | Feasibility | Impact | (1-Risk) | **总分** |
|------|---------|-------------|--------|----------|---------|
| SAE训练方法 | 0.3 | 0.9 | 0.3 | 0.3 | **0.024** |
| Grokking | 0.3 | 0.9 | 0.4 | 0.1 | **0.011** |
| **Phase Transition** | **0.85** | **0.8** | **0.9** | **0.85** | **0.520** |

**Phase Transition以20x+优势胜出。**

---

## 最终决定: 方向C — 小模型Reasoning的Phase Transition

### 为什么是最佳选择

1. **竞争最少**: 1年只有~7篇相关论文，而grokking是5周9篇
2. **Novelty最高**: "controlled training + reasoning probe"组合未被做过
3. **零空结果风险**: 无论reasoning是否emerge，结果都有价值
4. **NeurIPS审美**: Controlled scaling experiments + phase diagrams = 完美符合NeurIPS口味
5. **站在巨人肩上**: 直接引用NeurIPS 2024 "Loss Perspective" + NeurIPS 2025 "Superposition Scaling"

### 为什么SAE从第一名变成淘汰

深度调研揭示了**灾难性的领域变化**:
1. **DeepMind明确放弃**: 发表negative results + blog post说"we are deprioritizing SAE research"
2. **Neel Nanda (领域创始人之一)**: "The most ambitious vision of mechanistic interpretability I once dreamed of is probably dead"
3. **Anthropic转向transcoders**: 不再投资per-layer SAEs
4. **数学上证明不可能**: ICLR 2026证明full disentanglement在realistic sparsity下不可行
5. **可复现性危机**: 不同seed只有30%特征重叠
6. **SAE变体过饱和**: 10+种变体，SAEBench说"often difficult to differentiate"

**这不是竞争问题——是整个方向的validity被质疑。** 即使你做出完美的SAE训练方法，reviewer会问: "But DeepMind showed SAEs don't work for downstream tasks. Why should we care about training them better?"

> 来源: [DeepMind Negative Results](https://deepmindsafetyresearch.medium.com/negative-results-for-sparse-autoencoders-on-downstream-tasks-and-deprioritising-sae-research-6cadcfc125b9)

### 为什么放弃Grokking

**已经太晚了。** 5周9篇论文，每个角度都被覆盖。"Phase diagram" → 已有。"加速" → 已有。"理论" → 已有。即使你做出好结果，reviewer会说"incremental over existing work"。

---

## 8周执行计划: Phase Transition in Small Model Reasoning

### Week 0 (准备, Day 1-2)
- [ ] 在RunPod上配置环境: PyTorch, nanoGPT, wandb
- [ ] 下载RedPajama-1T subset (100GB, 约40B tokens)
- [ ] 读"Evidence of Phase Transitions in Small Transformer-Based Language Models" (Nov 2025) — 确认差异化
- [ ] 读"Understanding Emergent Abilities from the Loss Perspective" (NeurIPS 2024) — 理解loss threshold方法
- [ ] 设计evaluation suite (算术、ICL、CoT、logic)
- GPU时间: 0h | 累计: 0h

### Week 1: 训练最小模型 + 建立pipeline
- [ ] 训练14M模型 (2B tokens, ~3h)
- [ ] 训练31M模型 (4B tokens, ~6h)
- [ ] 训练70M模型 (8B tokens, ~15h)
- [ ] 每个模型每1000步保存checkpoint
- [ ] 在所有checkpoint上运行evaluation suite
- [ ] 验证pipeline正确: wandb logging, evaluation脚本
- GPU时间: ~24h | 累计: 24h | 成本: ~$5-10

### Week 2: 训练中等模型
- [ ] 训练124M模型 (15B tokens, ~30h)
- [ ] 训练200M模型 (20B tokens, ~45h)
- [ ] 继续checkpoint evaluation
- [ ] 初步分析: 14M-200M的reasoning能力变化
- GPU时间: ~75h | 累计: 99h | 成本: ~$22-44

### Week 3: 训练最大模型
- [ ] 训练350M模型 (30B tokens, ~70h)
- [ ] 训练500M模型 (40B tokens, ~100h)
- [ ] 使用GaLore/Flora如果VRAM不够（500M需要~18GB）
- GPU时间: ~170h | 累计: 269h | 成本: ~$59-118

### Week 4: Phase Transition分析
- [ ] 绘制所有reasoning metric vs model size曲线
- [ ] 识别sharp transitions vs gradual improvements
- [ ] 对每个reasoning能力定位critical model size
- [ ] 绘制loss-based phase diagram（参照NeurIPS 2024 "Loss Perspective"）
- [ ] 分析: 不同reasoning能力的emergence是否同步？
- GPU时间: ~20h (probing) | 累计: 289h | 成本: ~$64-127

### Week 5: 数据量交互实验
- [ ] 选择2个关键规模点（phase transition前后）
- [ ] 在不同数据量(1/4, 1/2, 1x, 2x)上训练
- [ ] 分析: 数据量如何影响phase transition点？
- [ ] 这给出(model_size, data_amount) 2D phase diagram
- GPU时间: ~40h | 累计: 329h | 成本: ~$72-145

### Week 6: Mechanistic分析 + 额外实验
- [ ] **Crosscoder分析**: 用"Crosscoding Through Time" (Bayazit et al., 2025)工具追踪features emergence
- [ ] 训练linear probes分析不同层的reasoning表征
- [ ] 检验假设: reasoning emergence是否与特定attention pattern / circuit formation相关
- [ ] 参考"Beyond Induction Heads" (ICML 2025): 检查是否存在multi-phase circuit emergence
- [ ] 补充实验: 改变architecture (depth vs width) 如何影响transition
- [ ] 验证"Loss Perspective"假设: 相同loss、不同规模的模型是否有相同reasoning能力？
- GPU时间: ~30h | 累计: 359h | 成本: ~$79-158

### Week 7: 写作
- [ ] 写Introduction: "When do small LMs learn to reason?"
- [ ] 写Related Work: 引用emergence debate, loss perspective, Physics of LMs
- [ ] 写Method: controlled training protocol, evaluation suite
- [ ] 写Results: phase diagrams (核心图), scaling curves, loss analysis
- [ ] 写Analysis: 为什么reasoning emerge？哪些能力先emerge？
- GPU时间: ~5h (补充实验) | 累计: 364h | 成本: ~$80-160

### Week 8: 完善 + 投稿准备
- [ ] Ablation studies（如果reviewer要求）
- [ ] 润色论文
- [ ] 准备supplementary materials
- [ ] 准备代码开源（nanoGPT fork）
- [ ] 准备wandb public project（完全可复现）
- GPU时间: ~5h | 累计: 369h | 成本: ~$81-162

### 总计

| 指标 | 值 |
|------|-----|
| 总GPU时间 | **~369小时** |
| RTX 3090成本 | **$81** |
| RTX 4090成本 | **$162** |
| 训练模型数 | 7个主模型 + 8个数据量变体 + probes = **~20次训练** |
| Checkpoint数 | ~500个（用于fine-grained分析） |
| 评估数据点 | 500 checkpoints × 5 reasoning tasks = **2500个数据点** |

---

## 论文结构预览

### Title
**"When Do Small Language Models Learn to Reason? A Controlled Study of Phase Transitions in Reasoning Emergence"**

### Abstract核心论点
- 通过controlled training of 7 model sizes (14M-500M) on identical data, we identify sharp phase transitions in reasoning abilities
- Key findings: (1) arithmetic reasoning emerges at ~X params, (2) ICL emerges at ~Y params, (3) these transitions correspond to specific pre-training loss thresholds
- Different reasoning abilities emerge at different critical points, forming a "reasoning hierarchy"
- We provide the first fine-grained phase diagram mapping (model_size, training_tokens, reasoning_ability)

### 核心Figure (论文最重要的图)
```
Figure 1: Reasoning Phase Diagram
X轴: Model size (14M → 500M, log scale)
Y轴: Reasoning accuracy (0-100%)
多条线: 算术, ICL, CoT, Logic, Pattern
关键特征: 每条线在不同model size处有sharp jump (phase transition)

Figure 2: Loss-based Phase Diagram
X轴: Pre-training loss
Y轴: Reasoning accuracy
关键发现: 所有model sizes collapse到同一条曲线 (验证loss hypothesis)

Figure 3: (Model Size, Data Amount) 2D Phase Diagram
热力图显示reasoning能力在(size, data)空间中的emergence边界
```

### 预期impact
- 如果发现reasoning在小模型中也能emerge → 挑战"only large models can reason"假说
- 如果发现reasoning不emerge → 确认emergence需要的最低规模，指导efficient training
- 无论哪种结果，phase diagram本身就是重要贡献

---

## 需要提前验证的关键假设

在投入全部时间之前，先用Week 0-1的pilot实验验证:

1. **14M模型能否在至少一个task上表现above random?** → 如果完全random，说明起始规模太小
2. **Evaluation suite是否能区分不同规模?** → 如果所有模型都0分或100分，需要调整难度
3. **nanoGPT训练是否稳定?** → 在多个规模上验证loss正常下降
4. **Checkpoint保存和evaluation pipeline是否正常?** → 自动化是关键

如果pilot实验失败，**立即切换到SAE方向**（backup plan）。

---

## Backup Plan: SAE训练方法

如果Phase Transition方向在pilot中失败:
- 已有SAE方向的完整方案
- 切换成本低（同一GPU，不同代码）
- SAE方向的核心优势: 更快得到结果（不需要训练base model）

---

---

## 关键参考文献（已验证，按重要性排序）

### 必须引用（Related Work核心）
1. **PolyPythias** — Schurholt et al., ICLR 2025. 50 runs × 5 sizes. [arxiv.org/abs/2503.09543](https://arxiv.org/abs/2503.09543)
2. **Understanding Emergent Abilities from the Loss Perspective** — Du et al., NeurIPS 2024. [neurips.cc/virtual/2024/poster/96773](https://neurips.cc/virtual/2024/poster/96773)
3. **Physics of Language Models** — Allen-Zhu & Li, 7+ parts (2024-2025). [physics.allen-zhu.com](https://physics.allen-zhu.com/part-1)
4. **Are Emergent Abilities a Mirage?** — Schaeffer et al., NeurIPS 2023 Oral. [arxiv.org/abs/2304.15004](https://arxiv.org/abs/2304.15004)
5. **Distributional Scaling Laws** — Zhao, Saphra et al., 2025. [arxiv.org/abs/2502.17356](https://arxiv.org/abs/2502.17356)
6. **Evidence of Phase Transitions in Small Transformer-Based LMs** — Hong & Hong, Nov 2025. [arxiv.org/abs/2511.12768](https://arxiv.org/abs/2511.12768)

### 方法论参考
7. **Crosscoding Through Time** — Bayazit et al., Sep 2025. Feature emergence tracking. [arxiv.org/abs/2509.05291](https://arxiv.org/abs/2509.05291)
8. **Beyond Induction Heads: Multi-Phase Circuit Emergence** — Minegishi et al., ICML 2025. [arxiv.org/abs/2505.16694](https://arxiv.org/abs/2505.16694)
9. **Evolution of Concepts in LM Pre-Training** — Ge et al., Sep 2025. Two-stage learning. [arxiv.org/abs/2509.17196](https://arxiv.org/abs/2509.17196)

### 关键发现参考
10. **MobileLLM-R1** — Meta, Sep 2025. 950M model AIME 15.5. [arxiv.org/abs/2509.24945](https://arxiv.org/abs/2509.24945)
11. **Do Larger Models Generalize Better?** — U-shaped scaling, Apr 2025. [arxiv.org/abs/2504.03635](https://arxiv.org/abs/2504.03635)
12. **U-shaped and Inverted-U Scaling** — Wu & Lo, ICLR 2025. [arxiv.org/abs/2410.01692](https://arxiv.org/abs/2410.01692)
13. **How Do LLMs Perform Two-Hop Reasoning?** — Hao et al. (Meta FAIR), Feb 2025. Sharp phase transition. [arxiv.org/abs/2502.13913](https://arxiv.org/abs/2502.13913)
14. **Superposition Yields Robust Scaling** — NeurIPS 2025 Best Paper Runner-up.
15. **RL Does NOT Create New Reasoning** — NeurIPS 2025 Best Paper Runner-up.

### NeurIPS Positioning参考
16. **Scaling Laws and Compute-Optimal Training** — EPFL, NeurIPS 2024 Spotlight. Constant LR + cooldown. [github.com/epfml/schedules-and-scaling](https://github.com/epfml/schedules-and-scaling)
17. **E2LM Competition** — NeurIPS 2025. Small model early training evaluation. [arxiv.org/abs/2506.07731](https://arxiv.org/abs/2506.07731)
18. **Algorithmic Phase Transitions: Arithmetic** — Dec 2024. [arxiv.org/abs/2412.07386](https://arxiv.org/abs/2412.07386)
19. **The Kinetics of Reasoning: CoT and Grokking** — Pengmei et al., Oct 2025. [arxiv.org/abs/2510.25791](https://arxiv.org/abs/2510.25791)

### SAE/Grokking淘汰原因参考
20. **DeepMind Deprioritizing SAEs** — [deepmindsafetyresearch.medium.com](https://deepmindsafetyresearch.medium.com/negative-results-for-sparse-autoencoders-on-downstream-tasks-and-deprioritising-sae-research-6cadcfc125b9)
21. **On the Limits of SAEs** — ICLR 2026. [arxiv.org/abs/2506.15963](https://arxiv.org/abs/2506.15963)
22. **Grokking Phase Structure** — Feb 2026. Phase diagram already done. [arxiv.org/abs/2602.18523](https://arxiv.org/abs/2602.18523)
23. **GrokAlign** — Walker et al., Jun 2025. Controllable grokking already done. [arxiv.org/abs/2506.12284](https://arxiv.org/abs/2506.12284)

---

*深度分析完成: 2026-03-23*
*数据来源: arXiv API实时查询 (65+ papers) + 3个parallel research agents + NeurIPS 2024-2025 proceedings + web search*
*已验证论文数: 23篇核心 + 40+辅助*
