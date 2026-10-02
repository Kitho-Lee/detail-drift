# Roadmap

The roadmap uses decision gates so that method development only proceeds if the measurement gap is real.

## Phase 0 — Project setup

- Define repository conventions and experiment metadata.
- Confirm compute, storage, dataset rights, and model-license constraints.
- Freeze an initial set of product categories and prompts.

**Gate:** resources and legal/ethical constraints are compatible with the planned study.

## Phase 1 — Literature and reproduction

- Re-check the novelty landscape close to implementation time.
- Reproduce one long-horizon baseline end to end.
- Record runtime, memory, seeds, and generation settings.

**Gate:** a reproducible baseline can generate sufficiently long clips on available hardware.

## Phase 2 — ProductDrift pilot

- Implement masks, reference-view matching, geometry, OCR, colour, and semantic measurements.
- Run a small annotated pilot.
- Test whether the proposed signals agree with human observations and remain robust to lighting and viewpoint.

**Gate:** at least one reference-grounded signal captures meaningful product-detail loss.

## Phase 3 — Gap verification

- Measure early-versus-late fidelity across at least two generator families.
- Compare with global consistency metrics.
- Estimate uncertainty and test rank disagreement.

**Stop/pivot condition:** detail fidelity does not decline, or global metrics already explain the observed failures well.

## Phase 4 — Context propagation

- Corrupt and repair context in controlled probes.
- Estimate how context fidelity predicts the next chunk.
- Separate propagation effects from per-chunk re-generation error.

**Gate:** evidence supports context as a meaningful intervention point.

## Phase 5 — RGCR minimum viable method

- Add alignment confidence gates.
- Transfer only high-frequency reference detail.
- Refresh context and generate the next chunk.
- Compare against no repair, anchoring, and post-hoc compositing.

**Gate:** reference fidelity improves without unacceptable motion or quality loss.

## Phases 6–8 — Full study

- Ablations, sensitivity analysis, robustness, and failure cases.
- Cross-category and cross-generator generalization.
- Human acceptability study and usable-horizon calibration.
- Compute cost and cost per acceptable second.

## Phase 9 — Release

- Reproducibility pass and clean-room setup test.
- Model, dataset, privacy, and license review.
- Paper, demo, documentation, and archived experiment artifacts.
- Add an explicit repository license and citation metadata.
