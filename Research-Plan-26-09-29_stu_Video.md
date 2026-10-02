# Project Name： Reducing Temporal Drift in Long-Horizon AI Video Generation: An Applied Study with Commercialization Analysis for the E-Commerce Video Market

# Research Plan 26-09-29 (Your Copy): Detail Drift in Long-Horizon Product Video Generation

**Your initial topic (verbatim):** "Reducing Temporal Drift in Long-Horizon AI Video Generation: An Applied Study with Commercialization Analysis for the E-Commerce Video Market"
**Date:** 2026-09-29 · **Literature checked:** 2026-09-29

---

## What This Document Is and How to Use It

This is your research plan. I wrote it after evaluating your topic against the current literature.

- **What it contains:**
  - my verdict on your proposal and my reasons;
  - the direction I want you to work on;
  - the reading path, method and experiments;
  - the phase-by-phase schedule and how to report to me;
  - what to do tomorrow.
- **How to use it:**
  - Read the Summary and Sections A1–A6 before our first meeting.
  - Read A7–A15 during Phase 1.
  - Re-read the relevant phase in A18 at the start of every phase.
  - Keep A20 (reporting format) next to you every Friday.
- **Conventions:**
  - **Evidence** marks what a cited paper reports; **Hypothesis** marks something you must test.
  - **(assumption)** marks a planning number I chose that you will replace with measurements.
  - Keys such as [SelfForcing] point to the References at the end.

## Summary

I think your topic targets a real problem, but as formulated it is not a defensible Master's contribution. When I searched the literature up to 2026-09-29, I found that generic drift reduction in long or autoregressive video generation is one of the most crowded areas of generative vision. Training-based methods ([SelfForcing], [SelfForcing++], [LongLive], [RollingForcing], [SVI], [BAgger], [ResamplingForcing], [ContextForcing], [CausalForcing]) and training-free methods ([DeepForcing], [TTC], [FreqForcing], [RelaxForcing], [TetherCache], [TetherMem], [RECAP], [RecencyForcing]) were appearing several times a month in 2026. Another generic anti-drift module evaluated on VBench-Long would be incremental and probably outdated by the time you submit. A market-size analysis is not a CS research contribution.

**My verdict: REDIRECT.** I want to keep your two interests, drift in long videos and usefulness for e-commerce. I have changed the research question to a narrower one that has received little study and can be measured: **fine-detail drift of a known product relative to its clean reference images** (label text, logo, colour, local texture) in long-horizon image-to-video generation. Existing drift metrics are global and ignore the external product reference: VBench subject consistency compares DINO features with the video's own first and previous frames [VBench], and VDE measures change relative to the first segment [BIFE]. I suspect they miss the errors that make a product video commercially unusable.

**Provisional title:** *Detail Drift: Measuring and Repairing Reference Fidelity in Long-Horizon Product Video Generation.*

**Contributions I expect from you:**
- **C1:** a reference-grounded, region-level, human-calibrated evaluation protocol (ProductDrift).
- **C2:** a measurement of detail drift across contemporary generator families, with a model of how drift propagates through context and a derived "usable horizon".
- **C3:** Reference-Grounded Context Repair (RGCR). This training-free plug-in copies geometrically aligned *high-frequency* detail from the clean reference into the product region of the generator's *context*. Outputs are never edited, so any gain comes from the generator's own re-rendering.

I have turned your commercialization component into a domain evaluation: a human acceptability study, the usable horizon, and cost per acceptable second. A market analysis can become an optional, secondary thesis chapter based only on verifiable sources.

I rate the novelty risk as **moderate**. The plan fits one or two 48–80 GB GPUs, uses 1.3B–5B open models and needs no model training. Schedule: 28 weeks plus a 4-week buffer. The first 12 weeks cover Phases 0–4, the MVP gate and a novelty re-check.

## 中文摘要

我认为你的初始题目指向一个真实问题，但按原表述不足以构成可辩护的硕士研究贡献。我检索了截至2026-09-29的文献，发现长时/自回归视频生成中的通用“时间漂移”缓解已是生成式视觉中最拥挤的方向之一。基于训练的方法（Self Forcing、Self-Forcing++、LongLive、Rolling Forcing、Stable Video Infinity、BAgger、Resampling Forcing、Context Forcing、Causal Forcing）和免训练方法（Deep Forcing、Pathwise TTC、FreqForcing、Relax Forcing、TetherCache、TetherMem、RECAP-Forcing、Recency Forcing）在2026年几乎每月都有多篇发表。再做一个在VBench-Long上评测的通用防漂移模块只会是增量工作，等你投稿时很可能已经过时；市场规模分析也不属于计算机研究贡献。

**我的结论：REDIRECT（转向）。** 我希望保留你的两个兴趣——长视频漂移和电商可用性，但我把研究问题改成一个研究不足、可以度量的子问题：在长时图生视频中，已知商品相对其干净参考图（标签文字、Logo、颜色、局部纹理）的**细节漂移**。现有漂移指标都是全局的，而且不参照外部商品图：VBench主体一致性只与视频自身首帧和前一帧比较DINO特征，VDE只度量相对第一段的变化。我认为它们可能恰好漏掉使商品视频无法商用的错误。

**暂定题目：** *Detail Drift: Measuring and Repairing Reference Fidelity in Long-Horizon Product Video Generation。*

**我希望你完成三项贡献：**
- **C1：** 以参考图为基准、区域级、经人工校准的评测协议（ProductDrift）。
- **C2：** 对多类当代生成器细节漂移的测量，以及漂移经由上下文传播的模型和由此导出的“可用时长”。
- **C3：** 免训练插件“参考对齐的上下文修复”（RGCR）。它只把几何对齐后参考图的**高频细节**写入生成器**上下文**中的商品区域，从不修改输出帧，因此任何改进都来自生成器自身的重新渲染。

我把商业化部分改写为领域评测：人工可接受度研究、可用时长和“每可接受秒成本”。市场分析可以作为可选的次要论文章节，但只能使用可核查的来源。

我评估新颖性风险为**中等**。计划可在1–2块48–80 GB GPU上执行，使用1.3B–5B开源模型，无需训练模型。总周期28周另加4周缓冲；我希望你在前12周完成阶段0–4、MVP关口和一次新颖性复查。

---

# Part A — Your Research Plan

## A1. Your Starting Point

*When you use this section: at our kickoff meeting, and again at the end of Phase 1.*

I only had your topic title, so this profile is **my assumption, and I will correct it at our first meeting**.

- **What I expect you can do now:**
  - Python and basic PyTorch: train a small network and load pretrained models.
  - Linear algebra, probability, and an introductory ML/DL/CV course.
- **What I expect you have not done yet:**
  - Run a large video-diffusion codebase.
  - Read research code.
  - Design a controlled experiment with statistics.
  - Write a paper.
- **Your interest as I read it:** from "commercialization analysis" in your title, I infer that you care about whether the technology is usable in real products. I kept that interest, in a form that produces research evidence.

**Learning bridge**

| You need | How you will learn it | By |
|---|---|---|
| Diffusion and flow matching | [UDL] Ch. 18; [FMGuide] §1–4 (optional) | Week 2 |
| Transformers, attention, KV cache | [UDL] Ch. 12; reading the Self Forcing code | Week 2 |
| Autoregressive video diffusion, exposure bias | [DiffusionForcing], [SelfForcing] | Week 3 |
| Long-video state of the art and anchoring | [LongLive], [TTC] | Week 3 |
| How drift is measured today | [VBench], [BIFE] | Week 3 |
| Vision tools: segmentation, features, matching, OCR, optical flow | Hands-on with [SAM2], [DINOv2], [LightGlue], [PaddleOCR], [RAFT] | Weeks 2–4 |
| Experimental design and paired statistics | We work through it together in Phase 3 | Week 6 |

**Research style:** empirical and algorithmic, with an applied evaluation. You will **not** train a video foundation model. The method I want you to build is training-free and runs on existing open models.

**Compute assumption:**
- One or two 48–80 GB GPUs on the university server (A6000/A100/H100 class), or equivalent cloud credits.
- About 800 GPU-hours over the project (assumption).
- About 2 TB of storage (assumption).

## A2. My Evaluation of Your Original Proposal

*When you use this section: at our kickoff meeting.*

**My verdict: REDIRECT.** I decided to keep your problem area and your application interest, but to change the research question.

**What I like about your topic**
- Drift in long videos is an important open problem. A 2026 survey of memory in autoregressive video generation names standardized evaluation and trustworthy state updating as open challenges [MemorySurvey].
- E-commerce is a demanding test case because the product must stay *exactly* the same product.

**Why I do not think it can stay as formulated**
1. **"Reducing temporal drift" is overcrowded.** Between late 2025 and September 2026 there were dozens of drift-reduction methods. Examples:
   - self-rollout training: [SelfForcing], [SelfForcing++], [LongLive], [RollingForcing], [CausalForcing], [ContextForcing];
   - error-recycling training: [SVI], [BAgger], [ResamplingForcing];
   - training-free cache, sink and frequency methods: [DeepForcing], [TTC], [FreqForcing], [RelaxForcing], [TetherCache], [TetherMem], [RECAP], [FLEX], [RecencyForcing].

   Authors now report stable generation at minute scale, for example up to 240 s for [LongLive] and up to 4 min 15 s for [SelfForcing++].
2. **Your title names no mechanism.** Any module you add to one of these systems would compete with these papers on their own benchmarks. That is a weak position for a first project.
3. **The usual metrics do not measure what e-commerce needs.** VBench subject consistency compares DINO features of each frame with the video's first and previous frames [VBench]. VDE measures change relative to the first segment [BIFE]. Neither checks whether the label text, logo or colour still matches the product's catalogue image.
4. **A market analysis is not a CS contribution.** In my search, public market figures on AI video were mostly vendor claims that cannot be checked.

**What we keep and what I changed**

| Keep | Change |
|---|---|
| Long-horizon drift as the core phenomenon | From *generic* drift to *reference-grounded fine-detail* drift of a known product |
| E-commerce product videos as the application | From T2V prompts to product image-to-video with catalogue reference images |
| Commercial usability | From a market study to a human-calibrated **usable horizon** and **cost per acceptable second**; market analysis becomes an optional thesis chapter |
| A method that reduces drift | A training-free, model-agnostic mechanism (RGCR) with a falsifiable explanation |

## A3. Provisional Research Title

*When you use this section: naming files and reports; we revise it at Gate 4.*

**Detail Drift: Measuring and Repairing Reference Fidelity in Long-Horizon Product Video Generation**

If the method (C3) fails at Gate 3 or 4, our fallback title is *"How Long Does the Product Stay the Product? A Reference-Grounded Benchmark of Detail Drift in Long-Horizon Video Generation."*

## A4. One-Sentence Research Question

*When you use this section: copy it to the top of every report.*

**The question:** When a product image is animated into a long (30–120 s) video, does fine-grained fidelity to the clean product reference decay in a way that generic drift metrics miss? And can repairing only the product's high-frequency detail in the model's *context*, using the geometrically aligned reference, stop that decay without suppressing motion?

## A5. Core Research Gap

*When you use this section: writing the introduction; I check it with you at Gate 1.*

**Evidence (what the literature establishes)**
- Long-video methods are measured with global, reference-free consistency metrics:
  - VBench-Long [VBench++] (and the VBench repository), where subject consistency means DINO similarity to the video's own frames [VBench];
  - VDE, computed relative to the first segment with a subject-identity encoder [BIFE];
  - endpoint quality drift [StreamAV-Bench].
- Anchoring methods anchor to the *first generated frames* or to cached history, not to an external clean reference:
  - [TTC] uses the whole initial frame;
  - [LongLive] and [DeepForcing] use attention sinks;
  - [FreqForcing] anchors low frequencies to the first frames;
  - [TetherCache] aligns token statistics to a trusted context;
  - [TetherMem] routes subject queries to history.
- E-commerce and reference-driven generation work targets product or subject fidelity, but none of the verified papers addresses fidelity **over long horizons** in its abstract: [DreamActor-H1], [AnchorCrafter], [ConsID-Gen], [VACE], [Phantom], [MAGREF], [OmniVBench].
- On-screen text is fragile in generated video [VideoTextPreservation]. Clean context tends to be copied ("detail leakage") by autoregressive models [InContextForcing].

**Gap (a hypothesis until you verify it in Phase 3)**
- I found no verified work that measures, over long horizons, how faithfully a generated video keeps the *exact* details of an externally specified product.
- I found no verified work that uses that clean external reference to correct the *content* of the model's context.

The gap is only real if detail drift actually occurs in current open generators at 30–60 s and generic metrics miss it. That is why I want you to test this in Phase 3, before you build any method.

## A6. Research Hypothesis

*When you use this section: designing every experiment; we judge the hypotheses at Gates 1, 3 and 4.*

- **H1 (measurement).** In long product image-to-video generation:
  - reference-grounded fine-detail fidelity (text, local features, colour) decays significantly between the first and last 5 s of 30–60 s videos in at least two generator families;
  - over the same interval, global consistency metrics change little and rank methods differently.
  - *Refuted if:* detail fidelity does not decline, or global metrics track it closely (rank correlation high, same drops).
- **H2 (propagation).** Detail drift propagates mainly *through the context*.
  - Model: the fidelity of the next chunk depends on the fidelity of its context, $f_{k+1}=a\,q_k+b+\varepsilon$, with $a>0$.
  - *Refuted if:* the context-corruption probe (A12) gives $a\approx 0$, meaning the model re-degrades details regardless of its context.
- **H3 (mechanism).** Repairing the product region's high-frequency detail in the context from the aligned reference (RGCR):
  - raises long-horizon fidelity and extends the usable horizon;
  - keeps motion and image quality;
  - gives a gain per generator that grows with that generator's $a$.
  - *Refuted if:* there is no gain, the gain comes only with frozen motion or artifacts, or the gain does not track $a$.

## A7. Proposed Technical Idea

*When you use this section: Phases 3–5; this is what you will implement.*

### A7.1 Setting

- **Reference:** a small set of clean catalogue images $R=\{r_v\}_{v=1}^{V}$ with product masks $m_v$ ($V\ge 1$; several views when available).
- **Prompt:** a text $p$ describing the showcase, for example "slow orbit on a marble table, soft morning light".
- **Generator:** a pipeline $G$ that produces the video chunk by chunk, $X_{k+1}=G(C_k,p,z_k)$, where $C_k$ is the *context*. The context is:
  - the conditioning frames of an extension pipeline (e.g., the overlapping history frames in [SkyReels-V2], or the last frame in image-to-video chaining with [Wan2.2]); or
  - the KV cache built from recent frames in a causal model ([SelfForcing], [LongLive]).
- **First chunk:** conditioned on $r_1$ (image-to-video).

### A7.2 Measuring detail drift: the ProductDrift protocol (C1)

**Per frame.** For each sampled frame $x_t$ (4 fps):
- the product mask $M_t$ is tracked with [SAM2];
- the best-matching reference view $r^*_t=\arg\max_v n_{\text{inl}}(x_t,r_v)$ is the view with the most [LightGlue] inliers.

**Four similarities:**
- Semantic: $s^{\text{sem}}_t=\cos\big(\bar\phi(x_t,M_t),\bar\phi(r^*_t,m^*)\big)$, where $\bar\phi$ is the masked mean of [DINOv2] patch features.
- Local detail: $s^{\text{geo}}_t=n_{\text{inl}}/n_{\text{kp}}(r^*_t)$, the RANSAC-homography inlier ratio of LightGlue matches on the product crops.
- Text (products with printed text only): $s^{\text{txt}}_t=1-\mathrm{NED}\big(\mathrm{OCR}(x_t\odot M_t),y\big)$. NED is normalized edit distance, OCR is [PaddleOCR], and $y$ is the manually verified label string.
- Colour: $s^{\text{col}}_t=\exp(-\Delta E_{00}/\kappa)$ between the median Lab colours of the two masked regions ($\kappa=10$, assumption). This term is lighting-sensitive, so you report it with and without white-balance normalization.

**Normalization.** Divide each similarity by its **ceiling** $c_j$, measured on *real* footage of the same product under similar motion: $\hat s_j=\min(1,s_j/c_j)$.

**Window score.** The Product Fidelity Score of a 1-s window is $\mathrm{PFS}_w=\frac{1}{|J|}\sum_{j\in J}\operatorname{median}_{t\in w}\hat s_{j,t}$. It uses equal weights by default; weights fitted to human judgments (Phase 8) are reported as a secondary variant.

**Video summaries:**
- $\mathrm{AUFC}$: mean PFS over the video.
- $\Delta\mathrm{PFS}$: PFS of the last 5 s minus PFS of the first 5 s.
- Drift slope.
- **Usable horizon** $T_\tau$: the first time PFS stays below $\tau$ for 2 consecutive windows. $\tau$ is calibrated by humans as the PFS at which 50% of raters accept the clip (Phase 8); we fix a provisional $\tau$ after your Phase 3 pilot.

**Report alongside PFS:**
- the VBench-Long dimensions (subject and background consistency, motion smoothness, dynamic degree, aesthetic and imaging quality) [VBench++];
- **dynamics**: mean [RAFT] flow magnitude, separately inside and outside the product mask, so that frozen videos are caught;
- **chunk-boundary discontinuity**: flow-warping error across chunk boundaries.

### A7.3 Reference-Grounded Context Repair (RGCR) (C3)

Every $m$ chunks (MVP), each frame $c$ of the context $C_k$ is repaired as follows.

1. **Mask.** $M$ is the product mask from online SAM 2 tracking.
2. **Align.** Choose $v^*$ with the most LightGlue matches to $c$ inside $M$. Estimate a homography $H$ with RANSAC (affine fallback); let $e_{95}$ be the 95th-percentile reprojection error.
3. **Gate.** If $n_{\text{inl}}<n_{\min}$ or $e_{95}>e_{\max}$, leave $c$ unchanged. Repair only when alignment is trustworthy.
4. **Warp.** $W=\mathrm{warp}(r_{v^*},H)$, $\Omega=\mathrm{feather}_\omega\big(M\wedge \mathrm{warp}(m_{v^*},H)\big)$.
5. **High-frequency detail transfer.** With $\mathrm{HP}_\sigma(I)=I-G_\sigma * I$:
$$\hat c \;=\; c+\lambda\,\Omega\odot\big(\mathrm{HP}_\sigma(W)-\mathrm{HP}_\sigma(c)\big).$$
Inside $\Omega$, the low frequencies (shading, lighting colour, motion-blur envelope) stay those of the generator, and the high frequencies (glyph edges, logo contours, texture) come from the reference. Outside $\Omega$ nothing changes.
6. **Refresh the context.**
   - Extension pipelines: the repaired frames replace the conditioning frames.
   - Causal KV-cache models: re-encode the repaired frames with the VAE and recompute their keys and values at the clean timestep. This is analogous to the KV re-cache in [LongLive].

**Outputs are never edited.** Any improvement in output frames is produced by the generator re-rendering from a repaired context. I insist on this because it keeps the claim scientifically clean, and it is also what makes the result different from post-hoc compositing (which you will run as a baseline).

**Phase 5 extensions:**
- multi-view reference bank (nearest view per frame);
- confidence-adaptive $\lambda$ (scaled by inlier ratio);
- adaptive trigger: repair only when an online $s^{\text{geo}}$ monitor falls below $\theta$;
- dense refinement with RAFT flow for non-planar products;
- porting to a KV-cache causal model.

### A7.4 Pseudocode

```text
RGCR(G, R, p, K, m, λ, σ, n_min, e_max):
  X1 ← G.first_chunk(image=R[0], prompt=p)
  tracker ← SAM2.init(frame=X1[0], mask=mask(R[0]))
  for k = 1 … K-1:
      C ← G.context()                       # conditioning frames or KV window (decoded)
      if k mod m == 0:                      # MVP: fixed interval; Phase 5: adaptive trigger
          for each frame c in C:
              M ← tracker.mask(c)
              v*, H, n_inl, e95 ← best_view_homography(R, c, M)   # LightGlue + RANSAC
              if n_inl ≥ n_min and e95 ≤ e_max:
                  W ← warp(R[v*], H);  Ω ← feather(M ∧ warp(mask(R[v*]), H))
                  c ← c + λ·Ω⊙(HP_σ(W) − HP_σ(c))
          G.refresh_context(C)              # replace frames / VAE-encode + KV recache
      X_{k+1} ← G.next_chunk(prompt=p)
      tracker.update(X_{k+1})
  return concat(X1 … XK)                    # outputs are never edited
```

### A7.5 Why I think it might work (mechanistic explanation; hypotheses, not facts)

1. **The copy channel runs in both directions.** Autoregressive models lean heavily on recent clean context; [InContextForcing] reports "detail leakage" and shortcut copying from clean context frames. I expect the channel that propagates a blurred label forward to also propagate a repaired one.
2. **Missing information must come from outside.** Once a label's glyphs are blurred in every context frame, the only source that still holds them is the reference image. Two kinds of existing anchor cannot supply that information in the right place:
   - Whole-frame anchors to the first frame [TTC] also pull pose and scene back toward frame 0. TetherMem's analysis of memory-anchored scene under-progression shows why this is a problem [TetherMem].
   - Statistical alignment of cached tokens [TetherCache] cannot recreate specific glyphs.

   RGCR supplies exactly the missing detail, only where the product is, and in the product's current pose.
3. **Frequency separation respects the scene.** Taking shading from the generator and detail from the reference lets lighting and camera changes proceed while restoring the albedo detail that encodes product identity.
4. **Control view.** With $f_{k+1}=a q_k+b$, drift without repair converges to $f^*=b/(1-a)$. If repair closes a fraction $g$ of the context's fidelity gap, the fixed point rises by $\frac{ag(1-f^*)}{1-a+ag}$. This is zero when $a=0$ and grows with $a$. That is the falsifiable prediction in H3.

**Where I expect it to fail:**
- rotation beyond the coverage of the reference views;
- deformable, transparent or mirror-like products;
- text too small for the generator's resolution, where the ceiling is limited by the VAE and resolution rather than by drift.

### A7.6 What RGCR is not

- It is not post-hoc compositing, which edits outputs; compositing is a baseline.
- It is not a new attention or sink design.
- It involves no training.
- It is orthogonal to anti-drift methods, so I also want you to test RGCR combined with [TTC].

## A8. Expected Contributions (C1–C3)

*When you use this section: planning experiments; we revise it at Gate 4.*

- **C1 — ProductDrift.** A reference-grounded, region-level evaluation protocol for long-horizon product video. It includes:
  - a metric-validity study (controlled corruptions of real product videos);
  - a small human study linking PFS to acceptability;
  - a released evaluation set of your own photographed products plus an [ABO] subset.
- **C2 — Characterization and analysis.** Detail-drift curves for four or five contemporary generator families ([SkyReels-V2], [Wan2.2] chaining, [FramePack], [LongLive] or [SelfForcing] with [TTC], and optionally [SVI]). It includes:
  - the propagation coefficient $a$ and fixed point $f^*$ of each family;
  - the usable horizon $T_\tau$;
  - evidence of whether global metrics miss detail drift.
- **C3 — RGCR.** A training-free, model-agnostic context-repair mechanism. It includes:
  - ablations showing which parts matter (alignment, high-pass band, mask, interval);
  - the test of the prediction "gain grows with $a$";
  - cost analysis: overhead, latency and cost per acceptable second.

## A9. Closest Existing Work

*When you use this section: Phase 1 reading; writing related work.*

| Work | What it does | How your project differs |
|---|---|---|
| [TTC] Pathwise Test-Time Correction (2026) | Training-free. Anchors on the *initial generated frame* during low-noise sampling steps, then re-noises. Tested on CausVid and Self Forcing at 30 s. | Uses an *external clean reference*, region-restricted and geometry-aligned, transferring only high frequencies. Edits context *content*, not the sampling path. Measures fidelity to the reference. |
| [TetherCache] (2026) | Training-free cache management. Recalled tokens are statistically aligned to a trusted context distribution. | Content-level repair from the reference can restore information (glyphs) that statistics alignment cannot. |
| [TetherMem] (2026) | Region- and age-conditioned memory routing: subject tethered to history, scene released. | Does not change attention routing. Repairs the product region itself using the external reference, because routing to degraded history cannot recover lost detail. |
| [FreqForcing] (2026) | Anchors *low-frequency* attention components to the first frames; high frequencies come from local attention. | Transfers *high-frequency image* detail from the external reference, only inside the product region. |
| [BIFE] VDE metric (2025/26) | Drift relative to the first segment (subject, clarity, motion, aesthetic, background) on minute-long videos. | ProductDrift is relative to the external catalogue reference, region-level, includes text, local-feature and colour components, and is human-calibrated. |
| [ConsID-Gen], [DreamActor-H1], [AnchorCrafter] | Product and object identity preservation in image-to-video or human–product videos, using trained models; long-horizon drift is not addressed in their abstracts. | Long-horizon drift, training-free, measured over time. |

## A10. Essential Reading Path

*When you use this section: Phase 1 (weeks 1–3).*

The path runs Textbook → Foundation → Modern Method → State of the Art → Closest Work → Our Gap. For each item, I want a one-page note from you: problem, mechanism, what is measured, limitation relevant to us.

**1. Textbook — [UDL]** S. J. D. Prince, *Understanding Deep Learning*, MIT Press, 2023. https://udlbook.github.io/udlbook/
- **Why:** gives the mathematical base in one consistent notation.
- **Read:** Ch. 12 (Transformers) and Ch. 18 (Diffusion models).
- **Concepts:** self-attention, causal masking, forward and reverse diffusion, the denoising objective, sampling steps.
- **Skip:** Chs. 14–16 initially. Skim Ch. 17 (variational autoencoders), because video models work in a VAE latent space and RGCR re-encodes frames through the VAE.
- **Code:** the book's notebooks, e.g. `12_1_Self_Attention` and `18_2_1D_Diffusion_Model`, at https://github.com/udlbook/udlbook.
- **Outcome:** you can write the diffusion training loss and a sampling loop from memory.
- **Optional:** [FMGuide] §1–4. Flow matching is the objective family used by several models here; [SVI] describes its Wan-based training in flow-matching terms.

**2. Foundation — [DiffusionForcing]** B. Chen et al., *Diffusion Forcing: Next-token Prediction Meets Full-Sequence Diffusion*, NeurIPS 2024. https://arxiv.org/abs/2407.01392
- **Why:** it introduced per-frame independent noise levels, the basis of today's long and autoregressive video diffusion ([SkyReels-V2] is a diffusion-forcing model).
- **Read:** introduction, method, sampling and rollout-past-horizon experiments.
- **Concepts:** causal rollout; why teacher-forced models diverge past the training horizon.
- **Skip:** robotics/planning experiments and theory appendices.
- **Outcome:** you can explain why errors accumulate in rollouts. For the classical notion of exposure bias, also skim the introduction of [ScheduledSampling].

**3. Modern method — [SelfForcing]** X. Huang et al., *Self Forcing: Bridging the Train-Test Gap in Autoregressive Video Diffusion*, NeurIPS 2025. https://arxiv.org/abs/2506.08009
- **Why:** many systems in this plan build on it, e.g. [SelfForcing++], [TTC], [FreqForcing] and [TetherCache].
- **Read:** the problem statement, self-rollout with KV caching, the video-level loss, and gradient truncation.
- **Concepts:** teacher forcing vs. diffusion forcing vs. self forcing; KV cache; few-step distilled generators.
- **Skip:** distillation-loss variants on first reading.
- **Code:** https://github.com/guandeh17/Self-Forcing (T2V, 1.3B, ≥24 GB GPU per README).
- **Outcome:** you can trace one generation step through the code.

**4. State of the art — [LongLive]** S. Yang et al., *LongLive: Real-time Interactive Long Video Generation*, ICLR 2026. https://arxiv.org/abs/2509.22622
- **Why:** it is a strong public minute-scale system; the authors report 20.7 FPS on one H100 and videos up to 240 s.
- **Read:** frame sink with short-window attention, KV re-cache, and streaming long tuning.
- **Skip:** the interactive prompt-switch UI and quantization details.
- **Code:** https://github.com/NVlabs/LongLive (now LongLive-2.0 [LongLive-2.0]).
- **Outcome:** you understand attention sinks and KV re-cache, which RGCR reuses.

**5. Closest work — [TTC]** X. Xiang et al., *Pathwise Test-Time Correction for Autoregressive Long Video Generation*, arXiv 2026. https://arxiv.org/abs/2602.05871
- **Why:** it is the closest training-free anchoring method.
- **Read:** the high-noise vs. low-noise regimes, the correction-and-re-noise procedure, and the colour-shift and drift evaluations.
- **Concepts:** anchoring on the initial frame; correcting the sampling path.
- **Code:** https://github.com/xbxsxp9/Pathwise_TTC
- **Outcome:** you can state precisely how RGCR differs.
- **Companion (abstract and method only):** [TetherCache], [TetherMem].

**6. Our gap — how drift is measured:** [VBench] (CVPR 2024) §3 on Subject/Background Consistency; the VBench-Long README in https://github.com/Vchitect/VBench [VBench++]; and the VDE definition in [BIFE] (https://arxiv.org/abs/2511.22973).
- **Why:** these are the metrics everyone reports.
- **Concepts:** similarity to the video's own first and previous frames; relative change vs. the first segment; global identity encoders.
- **Outcome:** you can explain why these metrics cannot tell whether a label still reads correctly.

**After this path I expect you to understand:**
- why autoregressive video models drift (exposure bias, compounding through context);
- how current systems fight drift (self-rollout training, sinks, anchors, cache policies) and how each is evaluated;
- why global, self-referenced metrics can miss product-level errors;
- what exactly RGCR changes in the pipeline, and why that change is testable.

Supplementary, not required: [InContextForcing] (context copying), [FramePack] (anti-drifting sampling), [ConsID-Gen] and [DreamActor-H1] (e-commerce identity).

## A11. Baseline to Reproduce

*When you use this section: Phase 2 (weeks 2–4).*

| Role | System | What you reproduce | Success criterion |
|---|---|---|---|
| MVP host (extension pipeline) | [SkyReels-V2] DF-1.3B-540P, I2V and video extension | 30-s I2V videos from 5 product photos with README defaults (`overlap_history=17`, `addnoise_condition=20`) | Runs end-to-end; peak VRAM close to the README's ~14.7 GB for 540P 1.3B |
| Closest-method baseline | [SelfForcing] + [TTC] | One published comparison: TTC vs. vanilla Self Forcing at 30 s on ≥50 prompts from their prompt set (VBench consistency plus their colour-shift measure) | Same sign on every reported metric, and gap within ±30% of the reported gap or a documented reason |
| Causal AR state of the art | [LongLive] 1.3B | 30–60 s generation; VBench-Long subset | Runs; numbers in the reported range on the same prompts |
| Industry-practice baseline | [Wan2.2] TI2V-5B, last-frame chaining | 6 × 5-s segments chained from the product photo | Runs (≥24 GB GPU per README) |
| Anti-drifting I2V | [FramePack] (F1 variant) | 30-s I2V on 5 products | Runs; timing recorded (README: ≥6 GB; ~2.5 s/frame on RTX 4090 unoptimized) |

**Getting image-to-video from causal T2V models.** [SelfForcing] and LongLive-1.3B are T2V. Use first-frame prefill: encode the product photo as the first latent frame; [CausVid] reports zero-shot I2V this way. Verify it in Phase 2. If it fails, use LongLive-2.0 I2V if a checkpoint is released, or keep the extension pipelines as the main hosts.

## A12. First Gap-Verification Experiment

*When you use this section: Phase 3 (weeks 5–6); we decide at Gate 1.*

**3a. Metric validity (no generation needed).**
- Take real footage: 20 self-captured product videos plus 20 [ABO] spin sequences rendered as turntable videos.
- Corrupt *only* the product region at 5 severity levels: text blur, logo elastic warp, hue shift, texture smoothing.
- Compute each metric: VBench subject consistency, global DINO and CLIP similarity, and each PFS component.
- *My expectation (a hypothesis):* global metrics barely respond to detail corruptions, while $s^{\text{txt}}$ and $s^{\text{geo}}$ respond monotonically (Spearman $\rho$ vs. severity).
- Also report test–retest: the same real video under two different SAM 2 initialisations.

**3b. Drift measurement.**
- 30 products × 2 prompts × 2 seeds × 30 s (and a 60-s subset of 10 products).
- Four pipelines: SkyReels-V2 DF; Wan2.2 chaining; FramePack-F1; Self Forcing (or LongLive) with first-frame prefill, with and without TTC.
- Plot PFS and VBench subject consistency against time.

**3c. Context-propagation probe (tests H2).**
- For 15 products, take a good context and a drifted context from 3b.
- Also build contexts with *controlled* fidelity by corrupting the product region at 5 severities.
- Generate the next chunk from each (3 seeds) and regress next-chunk PFS on context PFS to estimate $a$ and $b$ per pipeline.

**Pre-registered GO criteria** (write them in your Phase 3 plan and send them to me *before* running):
- (i) $\Delta\mathrm{PFS}<0$ with 95% bootstrap CI excluding 0 in ≥2 pipelines;
- (ii) the global metrics' change is not significant, **or** Kendall $\tau<0.5$ between method rankings by VBench subject consistency and by PFS;
- (iii) $a>0$ (95% CI) in ≥2 pipelines;
- (iv) visual spot-check of 40 late-segment pairs confirms visible label, logo or colour errors.

## A13. Minimum Viable New Method

*When you use this section: Phase 4 (weeks 7–9); we decide at Gate 3.*

**RGCR-v0 on the SkyReels-V2 DF extension pipeline** (optionally also on Wan2.2 chaining):
- one reference view; homography; high-pass transfer ($\sigma=3$ px at 540p, $\lambda=1$, feather 7 px; all assumptions);
- repair of every conditioning segment;
- gating $n_{\min}=50$ inliers and $e_{\max}=\sigma/2$ (assumptions).

**Test set:** 20 products × 1 prompt × 2 seeds × 30 s.

**Compare against:**
- (a) no repair;
- (b) hard reset (re-condition on the original photo every segment);
- (c) post-hoc compositing (track, warp and paste the reference into *outputs*);
- (d) RGCR without mask (whole-frame high-pass);
- (e) RGCR without high-pass (full-band paste inside the mask).

**Signal I want to see:**
- AUFC gain over (a), 95% CI > 0;
- motion inside and outside the mask not reduced by >10%;
- sticker or seam artifacts in <20% of clips on visual audit (thresholds are assumptions; we fix them before you run).

## A14. Analysis Required

*When you use this section: Phase 6 (weeks 13–16).*

1. **Drift-propagation model.**
   - Fit $f_{k+1}=a q_k+b$ per pipeline, with a product random intercept; report residuals, since the linear model is a first-order approximation.
   - Check that uncorrected trajectories approach $f^*=b/(1-a)$.
   - Test the prediction that RGCR's gain rises with $a$, across pipelines and across products within a pipeline.
2. **Repair interval.** From the model, the largest interval keeping fidelity above $\tau$ is $m^*=\big\lfloor \log\frac{\tau-f^*}{f_0-f^*}/\log a\big\rfloor$ (valid for $f^*<\tau<f_0$), where $f_0$ is the fidelity right after a repair. Compare this with an empirical sweep over $m\in\{1,2,4,8\}$.
3. **Misalignment tolerance.** A misalignment of $\delta$ px moves transferred edges and causes ghosting when $\delta$ is comparable to $\sigma$. Inject synthetic homography noise to find the largest tolerable $e_{95}/\sigma$ and justify the gate $e_{\max}$.
4. **Cost.**
   - Measured overhead per repair (tracking, matching, filtering, VAE encode, KV re-cache) as a fraction of generation time.
   - For real-time causal models, the change in FPS and latency.
   - **Cost per acceptable second**: CPAS = total GPU-seconds of all generated videos ÷ total acceptable seconds, where a second is acceptable if it lies before $T_\tau$.
5. **Metric validity and reliability** (3a plus the human study): sensitivity, test–retest, and agreement with humans (AUC for predicting acceptability).

## A15. Full Experimental Plan

*When you use this section: Phases 7–8 (weeks 15–23).*

### Research questions
- **RQ1 (solves the problem?):** Does RGCR raise PFS-AUFC and $T_\tau$ at 30 s and 60 s over the strongest baselines, without lowering quality or dynamics?
- **RQ2 (why?):** Is the gain explained by context propagation ($a$) and by high-frequency repair specifically?
- **RQ3 (which components matter?):** alignment, frequency band, mask, interval, strength, multi-view references, adaptive trigger.
- **RQ4 (when does it fail?):** large rotations, non-planar or deformable products, reflective or transparent products, tiny text, hand occlusion, cluttered scenes, prompt switches.
- **RQ5 (cost?):** GPU-seconds, latency and FPS, CPAS.

### Data
- **ProductDrift-Real (you capture it):**
  - 40–60 of your own products (bottles, boxes, cans, shoes, bags, small electronics), most with printed text or logos;
  - per product: 5–8 clean reference photos on a plain background (multiple views) and 1–2 real 30-s handheld or turntable videos, which provide the ceilings and the metric-validity footage;
  - ground-truth label strings, typed and verified.
- **[ABO] subset:** 100–150 products with catalogue images and 360° spin sequences (CC BY 4.0 per the dataset page). Spins supply multi-view references and real turntable footage.
- **Prompts:** 3 motion templates per product (slow orbit ±30°; push-in with lighting change; handheld drift in a lifestyle scene) plus 1 hard template (full 360° rotation).
- **Durations:** 10, 30 and 60 s; 120 s for causal models only.
- **Legal:** own photos or CC BY data only; in public releases, blur third-party trademarks if required.

### Generators and baselines (strong, contemporary)
- **Generator families:** [SkyReels-V2] DF-1.3B; [Wan2.2] TI2V-5B chaining; [FramePack]-F1; [LongLive] or [SelfForcing] (1.3B causal); [SVI] (Wan2.1-I2V-14B + LoRA, tested on A100 80 GB per README; subset only).
- **Anti-drift baselines on the causal model:**
  - [TTC];
  - [DeepForcing] or [FreqForcing] (whichever runs on the same backbone);
  - a *reference sink* (the product image's KV kept permanently), which you implement.
- **Product baselines:**
  - hard reset;
  - post-hoc compositing;
  - best-of-N chunk resampling with PFS as verifier, at matched compute (related in spirit to [Stream-T1]).
- **Ours:** RGCR, RGCR + TTC, and RGCR-adaptive.

### Metrics
- PFS components and summaries (A7.2);
- VBench-Long dimensions;
- dynamics inside and outside the mask;
- boundary discontinuity;
- overhead and CPAS;
- human acceptability and 2AFC preference (Phase 8).
- FVD is not a primary metric: it is known to be biased toward per-frame quality over temporal quality [FVD-Bias].

### Main experiments
- **E1:** all generators × {none, RGCR} at 30 s and 60 s.
- **E2:** causal model × {none, TTC, Deep/FreqForcing, reference sink, RGCR, RGCR+TTC}.
- **E3:** product baselines (hard reset, compositing, best-of-N) vs. RGCR at matched GPU-seconds.

### Ablations
- Alignment: none / homography / homography + RAFT refinement.
- Band: high-pass / full-band / low-pass only.
- Mask: product / whole frame.
- Interval $m$.
- Strength $\lambda$.
- Single vs. multi-view references.
- Fixed vs. adaptive trigger.
- Context-only vs. context + output repair.

### Sensitivity
Sweep $\sigma$, $\lambda$, $m$, $n_{\min}$, $e_{\max}$, feather width and $\theta$; report fidelity–dynamics curves.

### Robustness and generalization
- per-category results;
- the hard 360° template;
- 120-s runs;
- resolution change;
- reference-to-video (product placed into a new scene) with [VACE]-1.3B chaining;
- prompt switching with LongLive;
- synthetic alignment noise.

### Cost
- GPU-hours per experiment (logged);
- seconds of GPU time per generated second;
- latency and FPS for causal models;
- CPAS.
- Planning budget (assumption, re-estimated after your Phase 0 timing): E1–E3 ≈ 350 GPU-h; ablations and robustness ≈ 200 GPU-h. FramePack and SVI are restricted to 30 products × 1 prompt × 2 seeds.

### Statistical reliability
- **Unit and pairing:** the unit is the (product, prompt) pair; seeds are nested (3 seeds in the main runs). All comparisons are paired (same product, prompt and seed).
- **Intervals and tests:** hierarchical bootstrap 95% CIs (resample products, then seeds); Wilcoxon signed-rank tests with Holm correction across baselines.
- **Model:** mixed-effects model PFS ~ method × time + (1|product) + (1|prompt).
- **Reporting:** effect sizes, not only p-values.
- **Human study:** ~20 raters; Krippendorff's α for agreement; Bradley–Terry for 2AFC. Requires ethics approval before running.

### Expected tables and figures

| # | Content |
|---|---|
| Tab. 1 | Metric validity: sensitivity (Spearman ρ vs. corruption severity) and test–retest for each metric |
| Tab. 2 | Main results at 30 s / 60 s: AUFC, ΔPFS, $T_\tau$, text, local-feature and colour components, VBench-Long dimensions, dynamics |
| Tab. 3 | Ablations |
| Tab. 4 | Cost: overhead %, FPS/latency, CPAS |
| Tab. 5 | Human study: acceptability, 2AFC win rates, AUC of PFS vs. global metrics for predicting acceptability |
| Fig. 1 | Teaser: label close-ups at 0/15/30/60 s, baseline vs. RGCR |
| Fig. 2 | PFS and VBench subject consistency vs. time per pipeline (the divergence that motivates C1) |
| Fig. 3 | Context-propagation probe: next-chunk vs. context fidelity, fitted $a$ per pipeline |
| Fig. 4 | RGCR gain vs. $a$ (prediction test) |
| Fig. 5 | Repair interval: empirical vs. predicted $m^*$ |
| Fig. 6 | Fidelity–dynamics frontier for anchoring methods |
| Fig. 7 | Failure gallery |

## A16. Major Risks

*When you use this section: every weekly report (the "Blockers" part).*

| Risk | What you will notice | What I want you to do |
|---|---|---|
| No measurable detail drift at 30–60 s | Flat PFS curves in 3b | Test 120 s and the hard templates; tell me before you continue |
| PFS is noisy or invalid | Poor test–retest; OCR fails on real footage | Drop the unreliable component; annotate text boxes manually on a subset |
| A baseline will not run or lacks I2V | Errors or unusable output after 3 days of effort | Report it to me; switch to the extension pipelines |
| RGCR creates artifacts | Stickers, seams or frozen products in the visual audit | Lower $\lambda$, widen feathering, tighten gating |
| Alignment fails on rotation or non-planar shapes | Low inlier rates | Multi-view references; restrict the claim to supported motions |
| Compute overrun | GPU-hours >30% over plan | Reduce seeds or products following the priority list we agree on |

## A17. Fallback Direction

*When you use this section: after Gate 3 or Gate 4 if the outcome is negative.*

- **Fallback 1 (most likely; keeps C1 and C2): a measurement paper.**
  - Content: ProductDrift, validated against humans, used to audit 5–8 open generators plus anti-drift methods on product videos. The headline result is the usable horizon of each family and where global metrics mislead.
  - Why it holds: it does not depend on RGCR working.
- **Fallback 2: verifier-guided resampling.**
  - Content: use PFS as a chunk-level verifier for best-of-N resampling and study the compute–fidelity trade-off (compare with [Stream-T1]).
  - Why it holds: it uses the same metric pipeline.

## A18. Executable Phase Plan (Phases 0–9)

*When you use this section: at the start and end of every phase.*

**Phase 0 — Environment preparation (week 1; difficulty: low–medium)**
- **Tasks:**
  - Obtain server access; create a conda environment (Python 3.10, PyTorch ≥2.5 with CUDA 12.x).
  - Clone SkyReels-V2, Wan2.2, FramePack, Self-Forcing, LongLive, Pathwise_TTC, DeepForcing (or FreqForcing), VBench, SAM 2, LightGlue, PaddleOCR and RAFT.
  - Download the checkpoints.
  - Generate one 10-s product video with each generator.
  - Log peak VRAM and seconds per generated second.
  - Set up a run registry (config YAML, seed and git hash per run).
- **Deliverable:** `env.yml`, a run registry, and a timing/VRAM table.
- **Success:** ≥3 of the 4 main generators produce a 10-s product video.
- **Report to me:** the timing table and blocking errors.

**Phase 1 — Learn (weeks 1–3; medium)**
- **Tasks:**
  - Complete reading items 1–6, with a one-page note on each.
  - Exercise 1: a 100-line toy diffusion or flow-matching model on 2-D data.
  - Exercise 2: annotate Self Forcing's inference loop (where the KV cache is written and read).
  - Exercise 3: explain on one slide why VBench subject consistency cannot detect a changed label.
- **Deliverable:** notes and exercises, plus a 30-minute oral understanding check with me.
- **Success:** you correctly answer ≥6 of 8 check questions.
- **Report to me:** notes and open questions.

**Phase 2 — Reproduce (weeks 2–4; medium–high)**
- **Tasks:**
  - Run the A11 reproductions.
  - Build ProductDrift v0 (SAM 2 masks, DINOv2, LightGlue, OCR, ΔE, RAFT) with unit tests on real footage.
  - Photograph the first 20 products.
- **Deliverable:** reproduction report, metric pipeline v0, and the first 20 products.
- **Success:** A11 criteria met, and PFS on real footage is stable (test–retest difference <0.05, assumption).
- **Report to me:** reproduction table with deviations explained. Gate 2 at the end of week 4.

**Phase 3 — Verify the research gap (weeks 5–6; medium)**
- **Tasks:**
  - Pre-register the criteria.
  - Run 3a, 3b and 3c (A12).
  - Draft the ethics application for the human study (submit in week 7).
- **Deliverable:** gap report with Tab. 1 and Figs. 2–3.
- **Success:** the A12 GO criteria are met.
- **Report to me:** the gate report. Gate 1 at the end of week 6.
- If the problem cannot be reproduced, we reconsider the hypothesis together before you write any method code.

**Phase 4 — Minimum viable idea (weeks 7–9; medium–high)**
- **Tasks:** implement RGCR-v0 (A13) and run the comparison set (a)–(e).
- **Deliverable:** MVP report with a small results table and a visual audit sheet.
- **Success:** the A13 signal criteria are met.
- **Report to me:** the gate report. Gate 3 at the end of week 9.

**Phase 5 — Full design (weeks 10–14; high)**
- **Tasks:**
  - Novelty re-search in week 10, before investing further.
  - Add the multi-view reference bank, adaptive trigger, confidence-adaptive $\lambda$ and RAFT refinement.
  - Port to the causal KV-cache model with re-cache.
  - Batch-run infrastructure.
- **Deliverable:** RGCR v1 on ≥3 pipelines.
- **Success:** v1 ≥ v0 on a validation split of 10 products (not used in the main test).
- **Report to me:** a design note with pseudocode updates.

**Phase 6 — Analysis (weeks 13–16; medium)**
- **Tasks:** all A14 analyses; human-study pilot (5 raters) if ethics approval has arrived.
- **Deliverable:** analysis report and Figs. 3–5.
- **Success:** the model fits with interpretable residuals, and the prediction test is run (whatever its outcome).
- **Report to me:** the analysis report.

**Phase 7 — Main experiments (weeks 15–19; high)**
- **Tasks:** E1–E3 on the full test set; freeze the code before starting.
- **Deliverable:** Tabs. 2 and 4.
- **Success:** complete matrix with statistics.
- **Report to me:** the gate report. Gate 4 at the end of week 19.

**Phase 8 — Ablation, robustness, failure analysis and human study (weeks 20–23; medium–high)**
- **Tasks:** ablations, sensitivity, robustness set, failure gallery, and the main human study (~20 raters).
- **Deliverable:** Tabs. 3 and 5, Figs. 6–7.
- **Success:** each hypothesis has a supporting or refuting result.
- **Report to me:** the robustness report. Final novelty re-check in week 22.

**Phase 9 — Paper construction (weeks 23–28; medium)**
- **Story:** Problem → Evidence of gap (Tab. 1, Fig. 2) → Insight (propagation, Fig. 3) → Method (RGCR) → Analysis (Figs. 4–5) → Experiments (Tabs. 2–5) → Limitations (Fig. 7).
- **Deliverable:** full draft by week 26 and submission-ready paper by week 28, plus an artifact release (code, evaluation set, prompts).
- **Success:** the paper passes an internal review.
- **Report to me:** drafts.
- **Buffer:** weeks 29–32. The optional commercialization thesis chapter is written in parallel during weeks 20–28, at no more than one day per week. That chapter compares self-hosted open models, commercial APIs and conventional production on cost and turnaround, using only primary sources recorded with access dates (official price pages, cloud GPU list prices, public filings or platform documentation). It contains no vendor blog statistics.

## A19. 8–12 Week Milestone Plan

*When you use this section: every week.*

These 12 weeks cover **Phases 0–4 completely and the first three weeks of Phase 5**. Week 1 starts on 2026-09-30.

| Week (ends) | Milestone | Phase | Evidence you send me |
|---|---|---|---|
| 1 (Oct 6) | Environment works; pilot of 10 products photographed; notes on readings 1–2 | 0, 1 | Timing/VRAM table; photo folder |
| 2 (Oct 13) | Notes 3–4; SAM 2 + DINOv2 similarity curve on 5 real videos | 1, 2 | Curves; notes |
| 3 (Oct 20) | Notes 5–6; understanding check; TTC reproduction running; 20 products done | 1, 2 | Check result; logs |
| 4 (Oct 27) | **Gate 2**: baselines reproduced; ProductDrift v0 unit-tested | 2 | Reproduction report |
| 5 (Nov 3) | 3a metric validity done; 3b generation running | 3 | Tab. 1 draft |
| 6 (Nov 10) | **Gate 1**: gap report (3a–3c) | 3 | Gap report |
| 7 (Nov 17) | RGCR-v0 implemented; ethics application submitted | 4 | Code and sample videos |
| 8 (Nov 24) | Runs of variants (a)–(e) | 4 | Interim table |
| 9 (Dec 1) | **Gate 3**: MVP signal decision | 4 | MVP report |
| 10 (Dec 8) | Novelty re-search; decision on full-design scope | 5 | Search log |
| 11 (Dec 15) | Multi-view references and adaptive trigger | 5 | Validation results |
| 12 (Dec 22) | Causal-model port started; 4-page interim report | 5 | Interim report |

## A20. Reporting Format

*When you use this section: every Friday, and before every gate meeting.*

**Weekly one-pager** (send it to me by Friday; one page; file name `W##_report.md`):
1. **Done:** tasks completed, each linked to the plan item.
2. **Evidence:** numbers, one or two plots, run IDs and paths to videos. No claims without evidence.
3. **Blockers:** what stopped you, what you tried, and what you need from me.
4. **Next:** 3–5 tasks for next week.
5. **Log:** hours spent, GPU-hours used, and cumulative GPU-hours against the budget.

**Gate report** (2–4 pages; send it to me 2 days before the gate meeting):
1. The gate question.
2. The pre-registered criterion (copied, not edited).
3. Method and data actually used.
4. Results table and figure, with CIs.
5. Whether the criterion was met.
6. Your recommendation (GO, MODIFY or STOP) with reasons.
7. Risks you noticed.
8. Plan for the next phase.

Report negative results exactly like positive ones. I value them equally.

## A21. Immediate Assignment — What I Want You to Do Tomorrow

*When you use this section: 2026-09-30.*

1. **Get a GPU and run one generator.**
   - Log in to the server and run `nvidia-smi`; create the conda environment.
   - Clone SkyReels-V2 and follow its README to generate one I2V video from any product photo with the DF-1.3B-540P model.
   - Record peak VRAM and wall-clock time in `timing.csv`.
2. **Photograph 10 pilot products.** Choose items with printed text and a logo (shampoo bottle, snack box, drink can, etc.).
   - For each product, take 5 photos on a plain background (front, ±30°, ±60°) under fixed lighting.
   - Take one 30-s slow phone orbit.
   - Save as `P###/ref_*.jpg` and `P###/real_01.mp4`, and type the main label text into `P###/label.txt`.
3. **Read [SelfForcing] §1–3.** Write one page answering:
   - What is exposure bias?
   - How does Self Forcing train?
   - What is stored in the KV cache, and when is it written?
4. **Start the metric script.**
   - For one real product video, run SAM 2 with one click on frame 0 to track the product.
   - Compute a DINOv2 masked similarity to the front reference photo once per second, and plot the curve.
5. **Send me your first weekly one-pager** (A20 format) by Friday, including the timing table and the plot.

---

# References

Every entry below was opened or confirmed via search or fetch on **2026-09-29** (verified 2026-09-29). "arXiv preprint" means no peer-reviewed venue was confirmed.

- **[ABO]** J. Collins et al. *ABO: Dataset and Benchmarks for Real-World 3D Object Understanding.* CVPR 2022. https://openaccess.thecvf.com/content/CVPR2022/html/Collins_ABO_Dataset_and_Benchmarks_for_Real-World_3D_Object_Understanding_CVPR_2022_paper.html ; data and licence https://amazon-berkeley-objects.s3.amazonaws.com/index.html — verified 2026-09-29.
- **[AnchorCrafter]** Z. Xu, Z. Huang, J. Cao, Y. Zhang, X. Cun, Q. Shuai, Y. Wang, L. Bao, J. Li, F. Tang. *AnchorCrafter: Animate Cyber-Anchors Selling Your Products via Human-Object Interacting Video Generation.* arXiv preprint 2411.17383, 2024. https://arxiv.org/abs/2411.17383 — verified 2026-09-29.
- **[BAgger]** R. Po, E. R. Chan, C. Chen, G. Wetzstein. *BAgger: Backwards Aggregation for Mitigating Drift in Autoregressive Video Diffusion Models.* arXiv preprint 2512.12080, 2025. https://arxiv.org/abs/2512.12080 — verified 2026-09-29.
- **[BIFE]** Z. Zhang, J. Mao, S. Chang, Y. He, Y. Han, J. Tang, F. Wang, B. Zhuang. *BIFE: Better Interaction, Fewer Errors for Minute-Long Video Generation* (v1 titled "BlockVid"). arXiv preprint 2511.22973, 2025 (rev. 2026). https://arxiv.org/abs/2511.22973 — verified 2026-09-29.
- **[CausVid]** T. Yin, Q. Zhang, R. Zhang, W. T. Freeman, F. Durand, E. Shechtman, X. Huang. *From Slow Bidirectional to Fast Autoregressive Video Diffusion Models.* CVPR 2025. https://arxiv.org/abs/2412.07772 ; code https://github.com/tianweiy/CausVid — verified 2026-09-29.
- **[CausalForcing]** H. Zhu, M. Zhao, G. He, H. Su, C. Li, J. Zhu. *Causal Forcing: Autoregressive Diffusion Distillation Done Right for High-Quality Real-Time Interactive Video Generation.* ICML 2026. https://arxiv.org/abs/2602.02214 — verified 2026-09-29.
- **[ConsID-Gen]** M. Wu, A. Mishra, S. Dey, S. Xing, N. Ravipati, H. Wu, B. Li, Z. Tu. *ConsID-Gen: View-Consistent and Identity-Preserving Image-to-Video Generation.* arXiv preprint 2602.10113, 2026. https://arxiv.org/abs/2602.10113 — verified 2026-09-29.
- **[ContextForcing]** S. Chen, C. Wei, S. Sun, P. Nie, K. Zhou, G. Zhang, M.-H. Yang, W. Chen. *Context Forcing: Consistent Autoregressive Video Generation with Long Context.* arXiv preprint 2602.06028, 2026. https://arxiv.org/abs/2602.06028 — verified 2026-09-29.
- **[DINOv2]** M. Oquab et al. *DINOv2: Learning Robust Visual Features without Supervision.* TMLR 2024. https://arxiv.org/abs/2304.07193 — verified 2026-09-29.
- **[DeepForcing]** J. Yi, W. Jang, P. H. Cho, J. Nam, H. Yoon, S. Kim. *Deep Forcing: Training-Free Long Video Generation with Deep Sink and Participative Compression.* ICML 2026 (per official repository). https://arxiv.org/abs/2512.05081 ; code https://github.com/cvlab-kaist/DeepForcing — verified 2026-09-29.
- **[DiffusionForcing]** B. Chen, D. Martí Monsó, Y. Du, M. Simchowitz, R. Tedrake, V. Sitzmann. *Diffusion Forcing: Next-token Prediction Meets Full-Sequence Diffusion.* NeurIPS 2024. https://proceedings.neurips.cc/paper_files/paper/2024/hash/2aee1c4159e48407d68fe16ae8e6e49e-Abstract-Conference.html — verified 2026-09-29.
- **[DreamActor-H1]** L. Wang, Z. Xia, T. Hu, P. Wang, P. Wei, Z. Zheng, M. Zhou, Y. Zhang, M. Gao. *DreamActor-H1: High-Fidelity Human-Product Demonstration Video Generation via Motion-designed Diffusion Transformers.* arXiv preprint 2506.10568, 2025. https://arxiv.org/abs/2506.10568 — verified 2026-09-29.
- **[FLEX]** J. Li et al. *Train Short, Inference Long: Training-free Horizon Extension for Autoregressive Video Generation.* arXiv preprint 2602.14027, 2026. https://arxiv.org/abs/2602.14027 — verified 2026-09-29.
- **[FMGuide]** Y. Lipman, M. Havasi, P. Holderrieth, N. Shaul, M. Le, B. Karrer, R. T. Q. Chen, D. Lopez-Paz, H. Ben-Hamu, I. Gat. *Flow Matching Guide and Code.* arXiv preprint 2412.06264, 2024. https://arxiv.org/abs/2412.06264 — verified 2026-09-29.
- **[FVD-Bias]** S. Ge, A. Mahapatra, G. Parmar, J.-Y. Zhu, J.-B. Huang. *On the Content Bias in Fréchet Video Distance.* CVPR 2024. https://openaccess.thecvf.com/content/CVPR2024/papers/Ge_On_the_Content_Bias_in_Frechet_Video_Distance_CVPR_2024_paper.pdf — verified 2026-09-29.
- **[FramePack]** L. Zhang, S. Cai, M. Li, G. Wetzstein, M. Agrawala. *Frame Context Packing and Drift Prevention in Next-Frame-Prediction Video Diffusion Models.* NeurIPS 2025. https://arxiv.org/abs/2504.12626 ; https://openreview.net/forum?id=J8JCF64aEn ; code https://github.com/lllyasviel/FramePack — verified 2026-09-29.
- **[FreqForcing]** J. Li, L. Liang, L. Kong, Y. Zhang. *FreqForcing: Autoregressive Long Video Generation via Spectral Self-Anchoring.* arXiv preprint 2607.27110, 2026. https://arxiv.org/abs/2607.27110 ; code https://github.com/jiatongli2024/FreqForcing — verified 2026-09-29.
- **[InContextForcing]** L. Yang, L. Liu, M. Li, H. Feng, W. Cao, J. Zhang, Y. Shi. *In-Context Forcing: Uncovering Context Effects in Autoregressive Video Diffusion.* arXiv preprint 2608.05237, 2026. https://arxiv.org/abs/2608.05237 — verified 2026-09-29.
- **[LightGlue]** P. Lindenberger, P.-E. Sarlin, M. Pollefeys. *LightGlue: Local Feature Matching at Light Speed.* ICCV 2023. https://openaccess.thecvf.com/content/ICCV2023/html/Lindenberger_LightGlue_Local_Feature_Matching_at_Light_Speed_ICCV_2023_paper.html ; code https://github.com/cvg/LightGlue — verified 2026-09-29.
- **[LongLive]** S. Yang, W. Huang, R. Chu, Y. Xiao, Y. Zhao, X. Wang, M. Li, E. Xie, Y. Chen, Y. Lu, S. Han, Y. Chen. *LongLive: Real-time Interactive Long Video Generation.* ICLR 2026. https://arxiv.org/abs/2509.22622 ; code https://github.com/NVlabs/LongLive — verified 2026-09-29.
- **[LongLive-2.0]** Y. Chen et al. *LongLive-2.0: An NVFP4 Parallel Infrastructure for Long Video Generation.* arXiv preprint 2605.18739, 2026. https://arxiv.org/abs/2605.18739 — verified 2026-09-29.
- **[MAGREF]** Y. Deng, Y. Yin, X. Guo, Y. Wang, J. Z. Fang, S. Yuan, Y. Yang, A. Wang, B. Liu, H. Huang, C. Ma. *MAGREF: Masked Guidance for Any-Reference Video Generation with Subject Disentanglement.* ICLR 2026 (per official repository). https://arxiv.org/abs/2505.23742 — verified 2026-09-29.
- **[MemorySurvey]** H. H. Chen et al. *The Past Frames the Future: Memory for Autoregressive Video Generation* (survey). arXiv preprint 2609.28466, 2026. https://arxiv.org/abs/2609.28466 — verified 2026-09-29.
- **[OmniVBench]** W. Li et al. *OmniVBench: A Benchmark and Large-Scale Dataset for Omni Reference-to-Video Generation.* arXiv preprint 2609.22069, 2026. https://arxiv.org/abs/2609.22069 — verified 2026-09-29.
- **[PaddleOCR]** Cui et al. *PaddleOCR 3.0 Technical Report.* arXiv preprint 2507.05595, 2025; toolkit https://github.com/PaddlePaddle/PaddleOCR (Apache-2.0) — verified 2026-09-29.
- **[Phantom]** L. Liu, T. Ma, B. Li, Z. Chen, J. Liu, G. Li, S. Zhou, Q. He, X. Wu. *Phantom: Subject-Consistent Video Generation via Cross-Modal Alignment.* ICCV 2025. https://arxiv.org/abs/2502.11079 — verified 2026-09-29.
- **[RAFT]** Z. Teed, J. Deng. *RAFT: Recurrent All-Pairs Field Transforms for Optical Flow.* ECCV 2020. https://arxiv.org/abs/2003.12039 — verified 2026-09-29.
- **[RECAP]** H. Xu, Z. Ding, Z. Tu. *RECAP-Forcing: Retaining Content Appearances for Long Video Generation.* arXiv preprint 2608.26671, 2026. https://arxiv.org/abs/2608.26671 — verified 2026-09-29.
- **[RecencyForcing]** T. Cao, H. Nguyen, P. Nguyen, K. Nguyen. *Recency Forcing: Bridging the Long-Horizon Gap in Autoregressive Video Generation.* arXiv preprint 2609.19729, 2026. https://arxiv.org/abs/2609.19729 — verified 2026-09-29.
- **[RelaxForcing]** Z. Zhao, Y. Lu, Z. Liu, J. Song, J. Deng, I. Patras. *Relax Forcing: Relaxed KV-Memory for Consistent Long Video Generation.* BMVC 2026. https://arxiv.org/abs/2603.21366 — verified 2026-09-29.
- **[ResamplingForcing]** Y. Guo, C. Yang, H. He, Y. Zhao, M. Wei, Z. Yang, W. Huang, D. Lin. *End-to-End Training for Autoregressive Video Diffusion via Self-Resampling.* arXiv preprint 2512.15702, 2025. https://arxiv.org/abs/2512.15702 — verified 2026-09-29.
- **[RollingForcing]** K. Liu, W. Hu, J. Xu, Y. Shan, S. Lu. *Rolling Forcing: Autoregressive Long Video Diffusion in Real Time.* ICLR 2026. https://arxiv.org/abs/2509.25161 ; https://mlanthology.org/iclr/2026/liu2026iclr-rolling/ — verified 2026-09-29.
- **[SAM2]** N. Ravi et al. *SAM 2: Segment Anything in Images and Videos.* ICLR 2025. https://openreview.net/forum?id=Ha6RTeWMd0 ; https://arxiv.org/abs/2408.00714 — verified 2026-09-29.
- **[SVI]** W. Li, W. Pan, P.-C. Luan, Y. Gao, A. Alahi. *Stable Video Infinity: Infinite-Length Video Generation with Error Recycling.* ICLR 2026. https://arxiv.org/abs/2510.09212 ; code https://github.com/vita-epfl/Stable-Video-Infinity — verified 2026-09-29.
- **[ScheduledSampling]** S. Bengio, O. Vinyals, N. Jaitly, N. Shazeer. *Scheduled Sampling for Sequence Prediction with Recurrent Neural Networks.* NeurIPS 2015. https://arxiv.org/abs/1506.03099 — verified 2026-09-29.
- **[SelfForcing]** X. Huang, Z. Li, G. He, M. Zhou, E. Shechtman. *Self Forcing: Bridging the Train-Test Gap in Autoregressive Video Diffusion.* NeurIPS 2025. https://arxiv.org/abs/2506.08009 ; code https://github.com/guandeh17/Self-Forcing — verified 2026-09-29.
- **[SelfForcing++]** J. Cui et al. *Self-Forcing++: Towards Minute-Scale High-Quality Video Generation.* ICLR 2026. https://arxiv.org/abs/2510.02283 ; https://proceedings.iclr.cc/paper_files/paper/2026/hash/8a30aba6514b56d02976f49797f6338a-Abstract-Conference.html — verified 2026-09-29.
- **[SkyReels-V2]** G. Chen et al. *SkyReels-V2: Infinite-length Film Generative Model.* arXiv preprint 2504.13074, 2025. https://arxiv.org/abs/2504.13074 ; code https://github.com/SkyworkAI/SkyReels-V2 — verified 2026-09-29.
- **[Stream-T1]** Y. Tu, S. Wu, M. Huang, W. Wang, Y. Wang, C. Liu, Z. Mao. *Stream-T1: Test-Time Scaling for Streaming Video Generation.* arXiv preprint 2605.04461, 2026. https://arxiv.org/abs/2605.04461 — verified 2026-09-29.
- **[StreamAV-Bench]** K. Liu et al. *StreamAV-Bench: A Comprehensive Benchmark for Streaming Audio-Video Generation.* arXiv preprint 2608.26336, 2026. https://arxiv.org/abs/2608.26336 — verified 2026-09-29.
- **[TTC]** X. Xiang, Z. Duan, G. Zhang, H. Zhang, Z. Gao, J. Wu, S. Zhang, T. Wang, Q. Fan, C. Guo. *Pathwise Test-Time Correction for Autoregressive Long Video Generation.* arXiv preprint 2602.05871, 2026. https://arxiv.org/abs/2602.05871 ; code https://github.com/xbxsxp9/Pathwise_TTC — verified 2026-09-29.
- **[TetherCache]** Y. Meng, X. Luo, L. Li, W. Jiang, C. Gao, X. Chen, Y. Li, X.-P. Zhang. *TetherCache: Stabilizing Autoregressive Long-Form Video Generation with Gated Recall and Trusted Alignment.* arXiv preprint 2606.13035, 2026. https://arxiv.org/abs/2606.13035 — verified 2026-09-29.
- **[TetherMem]** C. Li, P. Zhang, H. Zhou, J. Zuo, F. Wang, D. Zhou, N. Sang, C. Gao. *Tether the Subject, Release the Scene: Query-Aware Memory Routing for Long-Horizon Autoregressive Video Generation.* arXiv preprint 2608.26902, 2026. https://arxiv.org/abs/2608.26902 — verified 2026-09-29.
- **[UDL]** S. J. D. Prince. *Understanding Deep Learning.* MIT Press, 2023. https://udlbook.github.io/udlbook/ — verified 2026-09-29.
- **[VACE]** Z. Jiang, Z. Han, C. Mao, J. Zhang, Y. Pan, Y. Liu. *VACE: All-in-One Video Creation and Editing.* ICCV 2025. https://arxiv.org/abs/2503.07598 ; code https://github.com/ali-vilab/VACE — verified 2026-09-29.
- **[VBench]** Z. Huang et al. *VBench: Comprehensive Benchmark Suite for Video Generative Models.* CVPR 2024. https://openaccess.thecvf.com/content/CVPR2024/html/Huang_VBench_Comprehensive_Benchmark_Suite_for_Video_Generative_Models_CVPR_2024_paper.html ; code https://github.com/Vchitect/VBench — verified 2026-09-29.
- **[VBench++]** Z. Huang, F. Zhang, X. Xu, Y. He, J. Yu, Z. Dong, Q. Ma, N. Chanpaisit, C. Si, Y. Jiang, Y. Wang, X. Chen, Y.-C. Chen, L. Wang, D. Lin, Y. Qiao, Z. Liu. *VBench++: Comprehensive and Versatile Benchmark Suite for Video Generative Models.* IEEE TPAMI 2025 (acceptance stated in the official repository, which also hosts VBench-Long). https://arxiv.org/abs/2411.13503 ; https://github.com/Vchitect/VBench — verified 2026-09-29.
- **[VideoTextPreservation]** Z. Liu, K. Valencia, J. Cui. *Video Text Preservation with Synthetic Text-Rich Videos.* arXiv preprint 2511.05573, 2025. https://arxiv.org/abs/2511.05573 — verified 2026-09-29.
- **[Wan2.2]** Wan-Video. *Wan2.2* (official repository; TI2V-5B, A14B models). https://github.com/Wan-Video/Wan2.2 — verified 2026-09-29.
