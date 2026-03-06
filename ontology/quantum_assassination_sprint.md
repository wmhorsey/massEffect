# Quantum Ontology Assassination Sprint (2 Days)

## Purpose
Stress-test the STE ontology against "quantum-like" observations by attempting to reproduce core signatures with purely ontology-native mechanisms.

## Scope
- Branch: `physics-refine`
- Time box: 2 days
- Target mechanism: pre-choke permeation through saturation barriers (STE tunneling hypothesis)
- Comparison baseline: stochastic transmission model with matched boundary conditions

## Hard Rules
- No borrowed quantum postulates in governing equations.
- No new free constants without diagnostics-backed justification.
- Every variant must preserve conservation and action-reaction gates.

## Questions To Kill Or Keep
1. Can pre-choke permeation produce transmission curves with barrier-width sensitivity similar to quantum-like signatures?
2. Can the same mechanism produce phase-sensitive effects without quantization assumptions?
3. Do diagnostics remain stable while reproducing these signatures?

## Experiment Matrix
1. Barrier profile sweep
- Control parameters: barrier width, barrier height proxy, local saturation gradient shape.
- Outputs: transmission fraction, reflection fraction, dwell proxy.

2. Initial condition sweep
- Control parameters: packet compactness, incident momentum proxy, chirality seed.
- Outputs: transmission curve family, chirality coupling changes.

3. Kernel sensitivity sweep
- Control parameters: pressure/permeation kernel range and shape (derived forms only).
- Outputs: fit quality vs stochastic baseline, residual distribution.

## Required Metrics
- `force_ar_residual` max absolute value
- `ste_total_drift_fraction`
- transmission fraction vs barrier width
- dwell proxy vs barrier width
- residuals against stochastic baseline fit
- runtime cost per simulated step (for compute-efficiency claim)

## Pass/Fail Criteria
- Pass if all are true:
  - Confidence gates remain green.
  - At least one STE variant matches or beats stochastic baseline fit on transmission curve residuals.
  - Runtime cost is not materially worse than baseline stochastic benchmark for equivalent fidelity.
- Fail if any are true:
  - Requires non-ontology assumptions to fit signatures.
  - Conservation/residual gates regress.
  - Fits are weak or unstable across nearby parameter settings.

## Deliverables (End Of Day 2)
1. Benchmark artifact bundle (JSON/CSV + seed list)
2. One-page sprint readout:
- hypothesis
- experiment matrix
- best/worst fits
- diagnostic gate status
- ontology implications
3. Recommendation:
- proceed with STE tunneling line, or
- revise mechanism and rerun sprint
