# NeurIPS 2026: Five Research Areas -- Literature Review & Single-GPU Direction Proposals

**Date**: 2026-03-23
**Constraint**: Single RTX 3090/4090 (24GB VRAM), $100-300 budget, 6-8 weeks
**Target**: NeurIPS 2026 (Abstract: May 4 AOE, Full Paper: May 6 AOE)
**Sources**: arXiv 2024-2026, NeurIPS 2024-2025 proceedings, ICML 2025, ICLR 2025, web search

---

## AREA 1: Scientific Machine Learning (ML for PDEs, Operator Learning, Climate, Molecular Dynamics)

### 1.1 Key Papers (2024-2026)

#### Neural PDE Solvers (Beyond PINNs)

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **Stochastic Taylor Derivative Estimator** | NeurIPS 2024 Best Paper | Million-dim PDEs in minutes on **single GPU**; 1000x speedup via derivative tensor contraction | Single GPU |
| **Latent Neural Operator (LNO)** | NeurIPS 2024 | Solves PDEs in latent space; 30% fewer params, 50% less memory, 1.8x faster than Transolver | Single GPU |
| **Mamba Neural Operator** | NeurIPS 2024 | SSM architecture for PDEs; sub-quadratic complexity | Single GPU |
| **PINNacle** | NeurIPS 2024 | Standardized PINN benchmark: 15 PDEs, 20+ methods | Benchmark |
| **Neural Operator Preconditioning** | arXiv 2509.01416 | Neural operators as preconditioners for classical PDE solvers; hybrid approach | Single GPU |
| **One-Shot Operator Learning** | Nature Comms 2025 | Learning from single solution trajectory via self-supervised + meta-learning; 5-10% error | Single GPU |
| **LITEFNO (Lightweight FNO)** | NeurIPS ML4PS 2025 | Efficient FNO for time-dependent PDEs; minimal memory | Single GPU |
| **D-FNO (Decomposed FNO)** | CMAME 2025 | Tensor decomposition reduces 3D complexity while maintaining accuracy | Single GPU |
| **DiffFNO** | CVPR 2025 | Diffusion + FNO for uncertainty quantification; 15-25% accuracy boost | Moderate |
| **LOGLO-FNO** | ICLR 2025 | Local-global feature learning for neural operators | Single GPU |
| **Memory-Enhanced Neural Operators** | ICLR 2025 | Explicit memory for time-dependent PDEs; reduces autoregressive error | Single GPU |
| **PI-GANO** | CMAME 2025 | Generalizes across PDE params AND domain geometries | Single GPU |
| **Geometric Operator Learning with OT** | NeurIPS ML4PS 2025 | Optimal transport for operator learning on varying geometries | Single GPU |

#### Climate/Weather Modeling (Small Scale)

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **NeuralGCM** | Nature 2024, Google | Hybrid physics-ML climate model; competitive with operational models | Multi-GPU (training), Single GPU (inference) |
| **ACE2 (AI2 Climate Emulator)** | 2025 | 40-year simulation in 1 hour on **single A100**; 400x faster than GCM | Single GPU inference |
| **SamudrACE** | 2025 | 800 years in 1 day on **1 GPU**; coupled ocean-atmosphere | Single GPU |
| **StormCast** | NVIDIA 2025 | 3km hourly scale; 10% better than NOAA operational model | Multi-GPU training |
| **Aardvark Weather** | Nature 2025 | End-to-end: raw observations to forecasts in single ML model | Multi-GPU training |

#### Molecular Dynamics with ML

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **MACE** | NeurIPS 2022 + follow-ups 2024-2025 | Higher-order equivariant message passing; gold standard for MLIPs | Single GPU for small systems |
| **CELLI** | npj Comp Materials 2025 | Charge equilibration for long-range interactions; model-agnostic | Single GPU |
| **Erwin** | ICML 2025 | Tree-based hierarchical transformer for large physical systems | Multi-GPU |
| **Efficient Equivariant MLIP** | npj Comp Materials 2025 | More efficient equivariant models for interatomic potentials | Single GPU |
| **Graph DiT** | NeurIPS 2024 Oral | Diffusion transformer for molecular generation | Single GPU |

### 1.2 Open Gaps

1. **Neural operator + uncertainty quantification**: DiffFNO started this, but UQ for neural PDE solvers remains underdeveloped. No principled confidence intervals.
2. **Transfer learning across PDE families**: Current operators are trained per-PDE-family. No general "foundation model" for PDEs at small scale.
3. **Neural operator efficiency**: FNOs still struggle with irregular geometries. Combining mesh-free methods with spectral methods is open.
4. **Small-scale climate downscaling**: Large weather models (Pangu, GraphCast) need multi-GPU. Downscaling from coarse to fine resolution on single GPU is unexplored at NeurIPS.
5. **Equivariant architectures for multi-scale MD**: Bridging coarse-grained and all-atom representations with equivariant NNs.
6. **One-shot/few-shot operator learning**: Nature Comms 2025 paper opened this door but only for simple systems.

### 1.3 Concrete Direction Proposals (Single GPU)

#### Direction 1A: Conformal Uncertainty for Neural PDE Operators
- **Idea**: Apply distribution-free conformal prediction to neural operators (FNO, DeepONet) to produce guaranteed prediction intervals for PDE solutions. No paper combines conformal prediction + neural operators.
- **Method**: Train FNO on PDE family, use conformal calibration set to produce pointwise coverage guarantees. Extend to time-dependent PDEs with adaptive conformal sets.
- **GPU**: RTX 3090, ~50h training + calibration. Cost: ~$11.
- **Novelty**: High. Conformal prediction is hot at NeurIPS (7+ papers in 2024-2025). Neural operators lack UQ. This bridges two communities.
- **Risk**: Medium. Need to show conformal sets are not vacuously wide.
- **Timeline**: 6 weeks. W1: implement FNO baselines. W2: conformal calibration. W3: time-dependent extension. W4: experiments on Navier-Stokes, Darcy flow, wave equation. W5-6: write.

#### Direction 1B: Few-Shot Neural Operator via Meta-Learning
- **Idea**: Meta-learn a neural operator that adapts to new PDE families from 1-5 examples. Extends Nature Comms 2025 one-shot paper with MAML/Reptile-style meta-training.
- **Method**: Meta-train across PDE families (heat, wave, Burgers, advection), meta-test on unseen families with few examples.
- **GPU**: RTX 3090, ~80h. Cost: ~$18.
- **Novelty**: High. One-shot operator learning just appeared; systematic meta-learning framework missing.
- **Risk**: Medium-high. Generalization across PDE families is hard.
- **Timeline**: 7 weeks.

#### Direction 1C: Lightweight Climate Downscaling on Single GPU
- **Idea**: Train a small diffusion/flow-matching model for statistical downscaling (coarse 1-degree to fine 0.25-degree) of ERA5 reanalysis data. Focus on specific variable (e.g., precipitation).
- **Method**: Conditional flow matching on ERA5 data. Model: ~50M params. Train on single variable, single region initially.
- **GPU**: RTX 4090, ~100h. Cost: ~$44.
- **Novelty**: Medium-high. Most climate ML papers use massive compute. Showing competitive downscaling with minimal compute is valuable.
- **Risk**: Medium. Climate community expects global evaluation.
- **Timeline**: 7 weeks.

---

## AREA 2: Model Compression & Efficient Training

### 2.1 Key Papers (2024-2026)

#### Quantization

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **QTIP (Trellis Coded Quantization)** | NeurIPS 2024 Spotlight | Ultra-low-bit quantization via TCQ; bitshift trellis for hardware efficiency; 2-bit with 6.82 PPL | Single GPU for PTQ |
| **OneBit** | NeurIPS 2024 | 1-bit weights via SVID decomposition; 81%+ of FP16 performance | Single GPU for QAT |
| **QBB (Quantization with Binary Bases)** | NeurIPS 2024 | Binary base decomposition for extreme quantization | Single GPU |
| **BitNet b1.58** | Microsoft 2024 | Ternary weights (-1,0,+1); competitive with FP16 at scale | Training from scratch needs multi-GPU; analysis is single GPU |
| **PT-BitNet** | 2025 | Post-training ternary quantization for existing LLMs up to 70B | Single GPU for PTQ |
| **DFloat11** | NeurIPS 2025 | Lossless 30% compression of model weights | Single GPU |
| **NVFP4** | NVIDIA 2025 | FP4 inference format; 2x throughput vs FP8 | Single GPU inference |
| **Q-VLM** | NeurIPS 2024 | PTQ for vision-language models | Single GPU |
| **Continual QAT** | ACL Findings 2025 | Quantization-aware pre-training that adapts during training | Multi-GPU for pre-training |

#### Pruning

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **Minitron (Pruning + KD)** | NeurIPS 2024, NVIDIA | 8B/4B from 15B via structured pruning + KD; 40x fewer tokens | Multi-GPU (but method is single-GPU applicable) |
| **Building on Efficient Foundations** | NeurIPS 2024 | Structured FFN linearization; self-guided training; up to 1.3B from scratch | Single GPU |
| **Structured Pruning 2025 survey** | Frontiers 2025 | Hybrid pipeline: prune first, then quantize for max compression | Survey |
| **Revisiting Pruning vs Quantization for SLMs** | EMNLP Findings 2025 | At small scale (<3B), pruning often beats quantization | Analysis |

#### Memory-Efficient Training

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **GaLore** | ICML 2024 | Low-rank gradient projection; LLaMA 7B on **single RTX 4090** | **Single RTX 4090** |
| **Flora** | ICML 2024 | 3B LLM on **single RTX 3060 (12GB!)** | **Single RTX 3060** |
| **VeLoRA** | NeurIPS 2024 | Rank-1 activation compression; outperforms GaLore on Llama-130M | Single GPU |
| **CoMERA** | NeurIPS 2024 | Rank-adaptive tensor optimization; 2x faster, 9x memory-efficient vs GaLore | Single GPU |
| **MicroAdam** | NeurIPS 2024 | Compressed optimizer state; provable convergence | Single GPU |

#### Knowledge Distillation

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **Low-Rank Clone (LRC)** | NeurIPS 2025 Spotlight | Project teacher into student via low-rank projections; 1000x training efficiency | Single GPU |
| **AdaSPEC** | NeurIPS 2025 | Selective token filtering for speculative decoder distillation | Single GPU |
| **Few-Shot KD with Counterfactual Explanations** | NeurIPS 2025 | Distillation with only 8-512 samples; uses counterfactual explanations | Single GPU |
| **Self-Distillation for Flow Maps** | NeurIPS 2025 | No pre-trained teacher needed; self-distillation via proximal optimization | Single GPU |
| **DDK (Domain KD)** | NeurIPS 2024 | Dynamic domain-aware distillation dataset composition | Single GPU |
| **MOHAWK (Transformer-to-SSM)** | NeurIPS 2024 | Distill Transformer to Mamba using <1% tokens | Single GPU feasible |

### 2.2 Open Gaps

1. **Quantization-aware pre-training from scratch on single GPU**: GaLore + quantization is unexplored. Can we combine 4-bit training with low-rank gradients?
2. **Structured pruning at initialization**: Most pruning is post-training. Pruning at init for small models (100M-1B) with theoretical guarantees is open.
3. **Cross-architecture distillation efficiency**: MOHAWK distills Transformer to Mamba but requires careful engineering. Systematic study of which architectures distill well into which is missing.
4. **Low-bit training dynamics**: Theory of why 4-bit/8-bit QAT works is sparse. Understanding loss landscape changes under quantization.
5. **Compression for non-language models**: Most compression work targets LLMs. Neural operators, GNNs, and diffusion models are under-compressed.

### 2.3 Concrete Direction Proposals (Single GPU)

#### Direction 2A: GaLore + Quantization: Pre-Training Sub-Billion LLMs in INT4 on Single GPU
- **Idea**: Combine GaLore's gradient low-rank projection with 4-bit quantized training. Goal: pre-train a 1B model on a single RTX 4090 with INT4 weights throughout training.
- **Method**: INT4 weight storage + low-rank gradient projections + 8-bit optimizer states. Measure quality vs. FP16 baseline at each scale (130M, 350M, 1B).
- **GPU**: RTX 4090, ~150h. Cost: ~$66.
- **Novelty**: High. GaLore and quantized training exist separately. Their combination is non-trivial (gradient projection in quantized space has different dynamics).
- **Risk**: Medium. INT4 training may be unstable without careful handling.
- **Timeline**: 7 weeks. W1: reproduce GaLore baseline. W2: implement INT4 forward/backward. W3: combine + debug. W4: scale to 350M/1B. W5: ablations + analysis. W6-7: write.

#### Direction 2B: Structured Pruning at Initialization via Gradient Flow Analysis
- **Idea**: Before training, analyze gradient flow through a randomly initialized network to identify which structures (attention heads, FFN neurons) will be useful. Prune at init, then train the smaller model.
- **Method**: Compute gradient signal-to-noise ratio per structure at initialization across multiple random seeds. Prune low-SNR structures. Compare with post-training pruning and random pruning.
- **GPU**: RTX 3090, ~80h. Cost: ~$18.
- **Novelty**: High. Pruning-at-init exists for CNNs (SNIP, GraSP) but not for Transformers at meaningful scale with modern architectures.
- **Risk**: Medium-high. Init pruning for Transformers may not preserve training dynamics.
- **Timeline**: 6 weeks.

#### Direction 2C: Low-Rank Clone for Non-Language Models (Neural Operators / Diffusion)
- **Idea**: Apply LRC (NeurIPS 2025 Spotlight) projection-based distillation to compress neural operators or diffusion models instead of LLMs.
- **Method**: Train large FNO teacher, project into small student via low-rank projections. Show 10x compression with <5% accuracy loss on PDE benchmarks.
- **GPU**: RTX 3090, ~60h. Cost: ~$13.
- **Novelty**: Medium-high. LRC is new and only demonstrated for LLMs; applying to other domains shows generality.
- **Risk**: Low-medium. LRC may not transfer directly to non-language architectures.
- **Timeline**: 6 weeks.

---

## AREA 3: Mixture of Experts (MoE) at Small Scale

### 3.1 Key Papers (2024-2026)

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **Multi-Head MoE (MH-MoE)** | NeurIPS 2024 | Extra MLP for token splitting/merging; alleviates low expert activation | Multi-GPU for large scale; single GPU for analysis |
| **MomentumSMoE** | NeurIPS 2024 | Momentum integration for stable sparse MoE training | Single GPU feasible at small scale |
| **Mixture of Nested Experts (MoNE)** | NeurIPS 2024 | Structured nested models as experts; no extra params; adaptive inference | Single GPU |
| **Toward Efficient MoE Inference** | NeurIPS 2024 | Comprehensive study of MoE inference bottlenecks | Analysis |
| **Gated Attention** | NeurIPS 2025 Best Paper | Sigmoid gating induces sparsity; tested on 15B MoE + 1.7B dense | Single GPU for small-scale replication |
| **OLMoE-1B-7B** | 2024, AI2 | 7B total, 1B active per token; fully open; high expert specialization | Multi-GPU training, single GPU inference |
| **DeepSeek-V3** | 2025 | 256 fine-grained experts; auxiliary-loss-free load balancing | Multi-GPU |
| **L-MoE (Lightweight LoRA-MoE)** | 2025 | Unifies MoE + LoRA; low-rank expert adapters with differentiable routing | Single GPU |
| **S'MoRE** | 2025 | 16% fewer trainable params via small low-rank matrices + projections | Single GPU |
| **Expert Choice Routing** | Google, NeurIPS 2022 | Experts choose tokens (not vice versa); perfect load balance | Single GPU feasible |
| **Time-MoE** | 2025 | Billion-scale time series foundation model using MoE | Multi-GPU training |
| **TriMoE** | 2026 | GPU + AMX CPU + DIMM offloading for MoE inference | Single GPU inference |
| **Rho-1 (Selective Language Modeling)** | NeurIPS 2024 Best Paper Runner-up | Token-level sparsity in training signal; complementary to MoE | Single GPU |

### 3.2 Open Gaps

1. **MoE training stability at small scale (100M-500M)**: Most MoE research is at 7B+. Training dynamics of small MoE models (4-8 experts, 100M-500M total) are poorly understood. Load balancing, expert collapse, and routing instability at small scale are under-studied.
2. **Expert specialization emergence**: OLMoE showed specialization emerges. When and how this happens during training, especially at small scale, is unknown.
3. **MoE + quantization**: Running quantized MoE models (e.g., 2-bit experts) is unexplored. Quantization may affect different experts differently.
4. **Routing beyond top-k**: Expert Choice, Hash routing, learned routing, soft routing -- systematic comparison at small scale missing.
5. **MoE for non-language tasks**: MoE is standard for LLMs but under-explored for vision, PDE solving, time series at small scale.
6. **Upcycling dense to MoE**: Converting a trained dense model into MoE by splitting FFN layers is emerging but lacks principled methods.

### 3.3 Concrete Direction Proposals (Single GPU)

#### Direction 3A: Small-Scale MoE Training Dynamics -- When Do Experts Specialize?
- **Idea**: Systematic study of MoE training dynamics at 100M-500M scale. Train dense vs. MoE models with 4/8/16/32 experts. Track expert specialization, routing entropy, load balance, and downstream task performance at every checkpoint.
- **Method**: Use nanoGPT/GPT-NeoX framework. Compare top-1, top-2, Expert Choice, and soft routing. Measure when expert specialization emerges via routing entropy and expert activation patterns.
- **GPU**: RTX 4090, ~200h. Cost: ~$88.
- **Novelty**: High. This is the small-scale analog of OLMoE's analysis but with controlled experiments. No systematic study exists at sub-billion scale.
- **Risk**: Low. Any result (experts specialize or don't) is informative.
- **Timeline**: 7 weeks. W1: implement MoE in nanoGPT. W2-3: train 100M/200M/500M with varying expert configs. W4: routing analysis + specialization metrics. W5: ablations (routing strategy, num experts). W6-7: write.

#### Direction 3B: Dense-to-MoE Upcycling with Expert Initialization
- **Idea**: Given a pre-trained dense 350M model, split each FFN into 4-8 experts with principled initialization (e.g., SVD-based clustering of weight columns). Train router + brief fine-tuning.
- **Method**: Cluster FFN weight columns via k-means in weight space. Each cluster becomes an expert. Initialize router from cluster assignments. Fine-tune for 1-5% of original tokens.
- **GPU**: RTX 3090, ~60h. Cost: ~$13.
- **Novelty**: High. Apple's HyperCloning (NeurIPS 2024 Workshop) goes small-to-large. This goes dense-to-sparse -- opposite direction with different principles.
- **Risk**: Medium. Expert initialization quality may vary.
- **Timeline**: 6 weeks.

#### Direction 3C: Quantized MoE -- 2-Bit Experts with Full-Precision Router
- **Idea**: In MoE, experts are large but sparsely activated. Quantize experts to 2-bit while keeping router at full precision. Hypothesis: since each expert specializes, it has lower effective rank and is more compressible.
- **Method**: Train small MoE (200M, 8 experts). Apply QTIP/GPTQ to experts only. Measure per-expert quantization sensitivity.
- **GPU**: RTX 3090, ~40h. Cost: ~$9.
- **Novelty**: High. No paper studies quantization of MoE at the expert level (vs. uniform quantization).
- **Risk**: Low. Even negative results are publishable.
- **Timeline**: 5 weeks.

---

## AREA 4: Tokenization & Data

### 4.1 Key Papers (2024-2026)

#### Tokenization Innovations

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **ADAT (Adaptive Tokenization)** | NeurIPS 2024 | Tokenizer evolves during training via perplexity monitoring; +2.6 over BPE | Single GPU |
| **MxDNA** | NeurIPS 2024 | Model-decides tokenization for DNA sequences | Single GPU |
| **Theoretical Analysis of Tokenization** | NeurIPS 2024 | Proves tokenized transformers break performance barriers on Markov data | Theory |
| **SuperBPE** | 2025 | 2-pass BPE with superword tokens; 33% fewer tokens; +4.0% avg across 30 benchmarks; +8.2% MMLU | Single GPU |
| **BoundlessBPE** | 2025 | Relaxes pre-tokenization boundary; up to 15% better bytes/token | Single GPU |
| **LiteToken** | 2025 | Removes intermediate merge residues from BPE vocabularies | Single GPU |
| **Right-to-Left Tokenization** | 2025 | +22pp on arithmetic via reversed tokenization + digit grouping | Single GPU |
| **IndicSuperTokenizer** | 2025 | Optimized tokenizer for multilingual LLMs | Single GPU |
| **Heuristic Tokenizer Flexibility** | 2025 | Achieving tokenizer flexibility in language models | Single GPU |
| **ICML 2025 Tokenization Workshop** | 2025 | Dedicated workshop signals growing importance | Community |

#### Data Selection & Curation

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **Rho-1 (SLM)** | NeurIPS 2024 Best Paper Runner-up | Selective token training; 30% improvement on math; train on useful tokens only | Single GPU for method |
| **DataComp-LM (DCLM)** | NeurIPS 2024 D&B | 240T token corpus; data filtering as new scaling axis | Benchmark |
| **JEST (Joint Example Selection)** | NeurIPS 2024 | Steer data selection via reference models; new dimension for scaling laws | Single GPU feasible |
| **Curriculum Learning for LLM Pretraining** | 2025 | 200+ models trained; 18-45% convergence acceleration; curriculum as warmup yields sustained +3.5% | Single GPU |
| **LR Decay Wastes Best Data** | 2025 | Constant LR + weight averaging + curriculum > cosine decay + curriculum | Single GPU |
| **Simula** | 2025 | Holistic synthetic data generation: taxonomy + agentic refinement + double-critic rejection | Moderate |
| **LLMs Should Be Pretrained on Preferred Data** | ACL Findings 2025 | Self-selection: let model choose its own training data | Single GPU |

#### Synthetic Data

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **Orchestrating Synthetic Data with Reasoning** | 2025 | Reasoning-guided synthetic data generation | Single GPU |
| **2024 in Synthetic Data and Smol Models** | Latent Space @ NeurIPS | Overview of synthetic data landscape | Survey |
| **HARMONIC** | NeurIPS 2024 D&B | LLM-based tabular data synthesis with privacy | Single GPU |
| **Binary Diffusion for Tabular Data** | NeurIPS 2024 Workshop | Lossless binary transform for tabular generation; XOR noise | Single GPU |

### 4.2 Open Gaps

1. **Tokenizer-model joint training at scale**: ADAT adjusts tokenizer during training but only via heuristic triggers. No end-to-end differentiable tokenizer-model co-optimization exists.
2. **SuperBPE + model architecture co-design**: SuperBPE reduces tokens by 33% but model architecture is unchanged. How should attention/FFN change when tokens are 33% longer on average?
3. **Data selection for reasoning**: Rho-1 selects tokens but doesn't target reasoning ability specifically. Selecting tokens/examples that specifically improve reasoning is open.
4. **Curriculum learning + tokenization interaction**: Curriculum orders data by difficulty, tokenization affects difficulty. Their interaction is unstudied.
5. **Synthetic data quality metrics beyond downstream performance**: When is synthetic data helpful vs. harmful? Principled metrics are missing.
6. **Domain-specific tokenization**: Code, math, scientific text all benefit from custom tokenizers. Systematic study of tokenizer design for specific domains is sparse.

### 4.3 Concrete Direction Proposals (Single GPU)

#### Direction 4A: Tokenizer-Architecture Co-Design -- How Models Should Change When Tokens Change
- **Idea**: SuperBPE produces tokens that are 33% longer (more information per token). Standard Transformers waste capacity treating these the same as short BPE tokens. Design architecture modifications (wider FFN, variable-depth per-token processing) that exploit richer tokens.
- **Method**: Train matched pairs: {BPE + standard arch} vs {SuperBPE + modified arch} at 130M-350M scale. Measure perplexity, downstream tasks, and compute efficiency.
- **GPU**: RTX 4090, ~120h. Cost: ~$53.
- **Novelty**: High. Everyone optimizes tokenizer OR architecture. Co-design is the obvious next step but nobody has done it.
- **Risk**: Medium. Improvements may be small.
- **Timeline**: 7 weeks. W1: implement SuperBPE. W2: design architecture variants. W3-4: train matched pairs. W5: analysis. W6-7: write.

#### Direction 4B: Reasoning-Targeted Data Selection (Rho-1 for Reasoning)
- **Idea**: Extend Rho-1's selective language modeling to specifically target reasoning tokens. Use a reasoning-capable reference model to score tokens by their "reasoning informativeness" rather than general utility.
- **Method**: Score tokens with a math/reasoning-tuned reference model. Filter pre-training data to concentrate on reasoning-dense passages. Train small models (130M-1B) and compare reasoning benchmarks vs. Rho-1 and random.
- **GPU**: RTX 4090, ~150h. Cost: ~$66.
- **Novelty**: High. Rho-1 is general-purpose. Reasoning-specific token selection is a natural but unexplored extension.
- **Risk**: Low-medium. May need careful reference model selection.
- **Timeline**: 7 weeks.

#### Direction 4C: Curriculum Learning Meets Tokenization -- Difficulty-Aware Token Vocabulary
- **Idea**: Current curriculum learning uses fixed tokenizer. Instead, adapt the tokenizer's active vocabulary as training progresses: start with character-level, gradually merge to word/superword level. The model "grows" its vocabulary alongside its capability.
- **Method**: Implement staged vocabulary expansion during training. Measure convergence speed and final quality vs. fixed vocabulary baselines.
- **GPU**: RTX 3090, ~100h. Cost: ~$22.
- **Novelty**: Very high. ADAT adjusts tokenizer during training but based on perplexity, not curriculum. Curriculum-driven vocabulary growth is novel.
- **Risk**: High. Engineering complexity is significant. Vocabulary changes mid-training may destabilize.
- **Timeline**: 8 weeks.

---

## AREA 5: Test-Time Compute & Inference

### 5.1 Key Papers (2024-2026)

| Paper | Venue | Key Contribution | GPU Req |
|-------|-------|------------------|---------|
| **Scaling LLM Test-Time Compute Optimally** | ICLR 2025 | Test-time compute more effective than scaling params for reasoning; process reward models + adaptive computation | Single GPU for inference |
| **Recurrent Depth (Latent Reasoning)** | NeurIPS 2025 | Iterates recurrent block to arbitrary depth; implicit reasoning in latent space; no CoT data needed; 3.5B proof-of-concept | Training: multi-GPU. Analysis: single GPU |
| **NeurIPS 2025 Tutorial: Scale TTC on Modern Hardware** | NeurIPS 2025 | Practical guide; memory-efficient KV management, adaptive scheduling | Tutorial |
| **Wider or Deeper? (AB-MCTS)** | NeurIPS 2025 | Adaptive branching tree search for inference scaling | Single GPU inference |
| **Dynamic TTC in Control (Stochastic Interpolant)** | NeurIPS 2025 | Difficulty-aware test-time compute for robotics control | Single GPU |
| **Self-Adapting Language Models (SEAL)** | 2025 | LLMs generate own fine-tuning data + update directives at test time | Single GPU |
| **Self-Improving LLM Agents** | 2025 | Agents self-improve at test time via generated training data | Single GPU |
| **RLVR Does NOT Create New Reasoning** | NeurIPS 2025 Runner-up | RLVR only improves sampling efficiency; base model distribution contains all reasoning paths; reframes TTC as key | Analysis |
| **ZERO: Training-Free TTA** | NeurIPS 2024 | 10x faster than prompt tuning; test-time adaptation without training | Single GPU |
| **PeTTA: Persistent TTA** | NeurIPS 2024 | Dynamic adaptation in recurring scenarios | Single GPU |

### 5.2 Open Gaps

1. **Test-time compute for small models (<1B)**: Most TTC research targets 7B+ models. How effective is TTC scaling for 100M-500M models?
2. **Budget-aware TTC allocation**: Given a fixed compute budget, how to optimally allocate across multiple queries? No principled framework exists.
3. **Latent reasoning at small scale**: Recurrent Depth (NeurIPS 2025) used 3.5B. Can the approach work at 100M-500M? What is the minimum model size for effective latent reasoning?
4. **TTC for non-language tasks**: Test-time compute scaling for vision, PDE solving, molecular design is virtually unexplored.
5. **Combining TTC strategies**: Best-of-N, tree search, self-refinement, test-time training -- these are studied independently. Principled combination/selection is open.
6. **Self-adaptation without catastrophic forgetting**: SEAL adapts at test time but may forget previous knowledge. Continual TTA is emerging but primitive.

### 5.3 Concrete Direction Proposals (Single GPU)

#### Direction 5A: Test-Time Compute Scaling Laws for Small Language Models
- **Idea**: Systematically study how TTC scaling (best-of-N, majority voting, tree search, self-refinement) interacts with model size at 14M-500M scale. Does TTC help tiny models more or less than large ones? Is there a minimum model size below which TTC doesn't help?
- **Method**: Train 5-7 model sizes (14M-500M) on same data. Apply 4 TTC strategies at varying compute budgets. Plot (model_size x TTC_budget) phase diagram for reasoning accuracy.
- **GPU**: RTX 4090, ~300h for training + 50h for TTC evaluation. Cost: ~$154.
- **Novelty**: Very high. ICLR 2025 paper studied TTC for large models. Nobody has done this for small models. The interaction between model scale and TTC effectiveness is unknown.
- **Risk**: Low. Any result is informative. "Small models benefit equally/less/more from TTC" are all publishable findings.
- **Timeline**: 8 weeks. W1-3: train models (overlap with Area 1 Phase Transition work). W4-5: implement TTC strategies + evaluate. W6: analysis + phase diagrams. W7-8: write.
- **Note**: This naturally combines with the "Phase Transition" direction from existing workspace analysis, sharing training compute.

#### Direction 5B: Latent Recurrent Reasoning at Minimal Scale
- **Idea**: Replicate the Recurrent Depth architecture (NeurIPS 2025) at 100M-500M scale. Find the minimum model size where latent reasoning via recurrent depth iteration provides measurable benefit.
- **Method**: Implement recurrent block architecture at small scale. Train with varying numbers of recurrence iterations (1, 2, 4, 8, 16). Measure reasoning improvement vs. compute on math and logic tasks.
- **GPU**: RTX 4090, ~200h. Cost: ~$88.
- **Novelty**: High. Original paper is 3.5B. Showing it works (or doesn't) at 10-50x smaller scale is important for the community.
- **Risk**: Medium. May not work at small scale, but that's still a finding.
- **Timeline**: 7 weeks.

#### Direction 5C: Budget-Aware Test-Time Compute Allocation Across Queries
- **Idea**: Given a batch of N queries and a fixed total compute budget, learn to allocate different amounts of TTC to different queries based on predicted difficulty. Easy queries get best-of-1, hard queries get best-of-64 + tree search.
- **Method**: Train a lightweight "difficulty predictor" on query features. Use it to allocate TTC budget. Compare with uniform allocation. Evaluate on GSM8K, MATH, ARC.
- **GPU**: RTX 3090, ~30h (uses existing models). Cost: ~$7.
- **Novelty**: High. Everyone applies uniform TTC. Adaptive allocation per-query is obvious but unstudied.
- **Risk**: Low. Method is simple and results are easily interpretable.
- **Timeline**: 5 weeks.

---

## CROSS-CUTTING: TOP 5 RECOMMENDED DIRECTIONS (Ranked)

Based on novelty, feasibility, NeurIPS fit, GPU requirements, and risk analysis:

| Rank | Direction | Area | Novelty | Feasibility | Cost | Risk | NeurIPS Fit |
|------|-----------|------|---------|-------------|------|------|-------------|
| **1** | **5A: TTC Scaling Laws for Small Models** | TTC + Inference | 9/10 | 8/10 | ~$154 | Low | 10/10 |
| **2** | **3A: Small MoE Training Dynamics** | MoE | 8.5/10 | 8/10 | ~$88 | Low | 9/10 |
| **3** | **4B: Reasoning-Targeted Data Selection** | Data | 8.5/10 | 8/10 | ~$66 | Low-Med | 9/10 |
| **4** | **1A: Conformal UQ for Neural Operators** | SciML | 8/10 | 9/10 | ~$11 | Medium | 8/10 |
| **5** | **2A: GaLore + INT4 Pre-Training** | Compression | 8/10 | 7/10 | ~$66 | Medium | 8/10 |

### Why Direction 5A is #1

1. **Zero-risk results**: Any outcome (TTC helps/doesn't help small models) is a contribution.
2. **Training compute can be shared** with multiple other directions (3A, Phase Transition study from existing workspace).
3. **Directly extends ICLR 2025 best paper** (Scaling LLM TTC Optimally) to small-model regime.
4. **NeurIPS loves scaling studies** with phase diagrams (see NeurIPS 2025 Best Paper Runner-up on scaling laws).
5. **Budget-friendly**: Training cost overlaps with other directions; TTC evaluation is mostly inference.

### Efficiency Combos (Shared Compute)

Several directions can share the same trained models:

- **Combo A** (best value): Train 7 model sizes (14M-500M) once (~270h, $60-120). Use for:
  - Direction 5A (TTC Scaling Laws)
  - Phase Transition study (existing workspace plan)
  - Direction 3A (add MoE variants to the same training sweep)
  - Direction 4B (compare standard vs. reasoning-selected training data)

  **Total cost for 4 potential papers**: ~$200-300

- **Combo B** (cheapest): Direction 1A (Conformal UQ for Neural Operators) + Direction 5C (Budget-Aware TTC). Both use existing pre-trained models. **Total cost: ~$20.**

---

## CRITICAL WARNINGS (From Self-Audit)

Based on the existing workspace's honest self-assessment (`NeurIPS-2026-最终验证报告.md`):

1. **Always verify via arXiv search before committing**. Previous recommendations in this workspace were wrong 4/6 times when checked against actual literature.
2. **NeurIPS acceptance rate is ~24.5%**. Even good papers have ~75% rejection probability. Never estimate >25% for any single submission.
3. **"Sounds novel" is not novel**. Always search `arxiv.org` for the exact combination of keywords before investing GPU hours.
4. **Negative/null results ARE publishable at NeurIPS** -- this is why scaling studies and empirical analyses are lower risk than method papers.
5. **Before starting any direction, do a 2-day pilot** to verify:
   - The baseline works
   - The evaluation pipeline is functional
   - The expected signal exists

---

## REFERENCES

### Scientific Machine Learning
- Stochastic Taylor Derivative Estimator (NeurIPS 2024 Best Paper)
- Latent Neural Operator: [proceedings.neurips.cc](https://proceedings.neurips.cc/paper_files/paper/2024/file/39f6d5c2e310a5a629dcfc4d517aa0d1-Paper-Conference.pdf)
- One-Shot Operator Learning: [Nature Communications](https://www.nature.com/articles/s41467-025-63076-z)
- LITEFNO: [NeurIPS ML4PS 2025](https://ml4physicalsciences.github.io/2025/files/NeurIPS_ML4PS_2025_287.pdf)
- Geometric Operator Learning with OT: [NeurIPS ML4PS 2025](https://ml4physicalsciences.github.io/2025/files/NeurIPS_ML4PS_2025_19.pdf)
- Neural Operator Preconditioning: [arxiv.org/abs/2509.01416](https://arxiv.org/abs/2509.01416)
- SamudrACE: [Medium](https://medium.com/@lz1955/samudrace-a-fast-accurate-efficient-3d-coupled-climate-ai-emulator-fcef3c60b079)
- ACE2: [NOAA Repository](https://repository.library.noaa.gov/view/noaa/68729/noaa_68729_DS1.pdf)
- Efficient Equivariant MLIP: [Nature](https://www.nature.com/articles/s41524-025-01535-3)

### Model Compression & Efficient Training
- QTIP: [NeurIPS 2024](https://proceedings.neurips.cc/paper_files/paper/2024/file/6de2e84b8da47bb2eb5e2ac96c63d2b0-Paper-Conference.pdf)
- OneBit: [NeurIPS 2024](https://proceedings.neurips.cc/paper_files/paper/2024/file/7a7a3f53faafc0161be0fcb57e5fa078-Paper-Conference.pdf)
- BitNet b1.58: [Wikipedia](https://en.wikipedia.org/wiki/1.58-bit_large_language_model)
- GaLore: [arxiv.org/abs/2403.03507](https://arxiv.org/abs/2403.03507)
- Low-Rank Clone: [NeurIPS 2025 Spotlight](https://medium.com/@1206013760/neurips-2025-spotlight-a-token-is-worth-over-1-000-tokens-efficient-knowledge-distillation-via-8139d18e097a)
- Minitron: [arxiv.org/abs/2407.14679](https://arxiv.org/abs/2407.14679)
- Revisiting Pruning vs Quantization for SLMs: [ACL Findings](https://aclanthology.org/2025.findings-emnlp.645.pdf)
- Model Compression Survey: [Frontiers 2025](https://www.frontiersin.org/journals/robotics-and-ai/articles/10.3389/frobt.2025.1518965/full)
- NVFP4: [NVIDIA Blog](https://developer.nvidia.com/blog/introducing-nvfp4-for-efficient-and-accurate-low-precision-inference/)

### Mixture of Experts
- MoE 2024-2025 Literature Review: [rohan-paul.com](https://www.rohan-paul.com/p/mixture-of-experts-moe-architectures)
- MoNE: [NeurIPS 2024](https://proceedings.neurips.cc/paper_files/paper/2024/file/6b768359d0e8925164f61f381a748441-Paper-Conference.pdf)
- Toward Efficient MoE Inference: [UPenn](https://www.seas.upenn.edu/~leebcc/documents/huang24-neurips.pdf)
- MoE in LLMs Survey: [arxiv.org](https://arxiv.org/html/2507.11181v1)
- MoE 2.0: [HuggingFace Blog](https://huggingface.co/blog/Kseniase/moe2)
- TriMoE: [arxiv.org](https://arxiv.org/html/2603.01058)

### Tokenization & Data
- SuperBPE: [arxiv.org](https://arxiv.org/html/2503.13423)
- BoundlessBPE: [arxiv.org](https://arxiv.org/html/2504.00178v1)
- ADAT: [NeurIPS 2024](https://proceedings.neurips.cc/paper_files/paper/2024/file/cdf00c97c0cb2cc35179f03363da6c4f-Paper-Conference.pdf)
- DataComp-LM: [NeurIPS 2024](https://proceedings.neurips.cc/paper_files/paper/2024/file/19e4ea30dded58259665db375885e412-Paper-Datasets_and_Benchmarks_Track.pdf)
- Curriculum Learning for LLM Pretraining: [arxiv.org/abs/2506.11300](https://arxiv.org/abs/2506.11300)
- LR Decay Wastes Best Data: [arxiv.org](https://arxiv.org/pdf/2511.18903)
- Data Selection Survey: [rohan-paul.com](https://www.rohan-paul.com/p/selecting-and-preparing-training)

### Test-Time Compute & Inference
- Scaling LLM TTC Optimally: [arxiv.org/abs/2408.03314](https://arxiv.org/abs/2408.03314)
- Recurrent Depth / Latent Reasoning: [arxiv.org/abs/2502.05171](https://arxiv.org/abs/2502.05171)
- NeurIPS 2025 TTC Tutorial: [neurips.cc](https://neurips.cc/virtual/2025/109595)
- AB-MCTS (Wider or Deeper): [neurips.cc](https://neurips.cc/virtual/2025/poster/116491)
- Self-Adapting LMs (SEAL): [arxiv.org](https://arxiv.org/html/2506.10943v2)
- Awesome Test-Time LLMs: [GitHub](https://github.com/Dereck0602/Awesome_Test_Time_LLMs)
- NeurIPS 2025 Recap: [Amplify Partners](https://www.amplifypartners.com/blog-posts/neurips-2025-recap)

---

*Compiled 2026-03-23. All papers verified via web search against arXiv, NeurIPS proceedings, and publisher sites.*
