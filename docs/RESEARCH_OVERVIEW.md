# Research overview

## Working title

**Detail Drift: Measuring and Repairing Reference Fidelity in Long-Horizon Product Video Generation**

## Motivation

Long generated videos can look coherent at a glance while drifting away from the product that was supplied as a reference. Global consistency scores may remain strong even after text, logos, colour, and local texture become commercially unacceptable.

This project narrows the broad temporal-drift problem to a falsifiable question: **does the generated product remain faithful to an external clean reference over long horizons?**

## Planned contributions

### C1 — ProductDrift

A reference-grounded, product-region evaluation protocol combining semantic, geometric, text, and colour fidelity. The protocol will be calibrated against real footage ceilings and human acceptability judgments.

### C2 — Drift measurement

A comparison across contemporary generator families, including an analysis of how context quality predicts the next generated chunk. The study will report a *usable horizon* rather than treating every generated second as equally valid.

### C3 — Reference-Grounded Context Repair

RGCR is a proposed training-free intervention. When alignment is reliable, it transfers high-frequency detail from a clean reference into the product region of context frames. Low-frequency appearance, lighting, and motion remain generated. Output frames are never directly composited.

## Falsifiable hypotheses

- **H1:** Reference-grounded fine-detail fidelity drops from the first to the last portion of long videos in at least two generator families, while common global metrics under-report or differently rank that loss.
- **H2:** Detail drift propagates through degraded generation context.
- **H3:** Repairing reference detail in context extends usable horizon without suppressing motion or reducing image quality.

Each hypothesis has an explicit failure condition in the detailed research plan. If H1 fails, the project should pivot to a benchmark/measurement result or stop before unnecessary method development.

## Intended scope

- Image-to-video product showcases lasting approximately 30–120 seconds.
- Open models that can be evaluated on available university or cloud GPU resources.
- Training-free method development for the initial implementation.
- Product categories with visible identity-bearing details and legally usable reference media.

## Out of scope for the initial study

- Training a video foundation model from scratch.
- Claiming general physical-world consistency from product fidelity alone.
- Treating market-size estimates as a computer-science contribution.
- Editing final output frames and presenting the result as improved generation.

## Success criteria

Success is not defined as producing a visually attractive demo alone. The project must establish a measurable gap, compare against credible baselines, preserve motion, report failure cases, and show statistical and human-evaluation evidence appropriate to the final claim.
