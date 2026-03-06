# MassEffect Plan

## Purpose
This file is the persistent project compass for the STE model. It exists so context compression or session resets do not lose direction.

## North Star
Build a scale-invariant, collapse-first STE simulation where:
- substrate flow is continuous (not quantized),
- mass emerges as resistance to flow,
- large structures interact through pre-contact saturation fronts,
- behavior is explainable with derived relations rather than magic constants.

## Direction Lock (Ontology First)
- Primary thesis: ontological modeling is the next compute leap, not hardware alone.
- Interpret "chance-like" behavior as emergent from deeper field relations unless diagnostics falsify it.
- Treat light and mass as co-emergent symptoms of one substrate motivation.
- Keep STE-native language and mechanisms as the source model; use mainstream terms only for comparison outputs.

Near-term physics objective:
- Formalize tunneling as pre-choke field permeation through saturation barriers.
- Build a benchmark that compares STE transmission curves against stochastic baselines.
- Promote only if predictive value and computational efficiency are demonstrated by diagnostics.

## Non-Negotiables
- No unexplained magic numbers in governing physics.
- Constants allowed only for:
  - numerical safety (`eps`, `void_threshold`),
  - unit selection (`parcel_radius_scale`, `dt` as integration resolution),
  - documented calibrated closure terms.
- Same physics stack across scales (proton, nebula, larger structures).
- Every claim must have diagnostics, not just visuals.

## Ontology Guardrails (Hard Constraint)
- Do NOT import standard-physics assumptions as hidden foundations.
- Standard physics terms are allowed only as observational labels or comparison metrics.
- The governing equations must remain STE-native:
  - substrate flow first,
  - collapse/resistance emergence,
  - structure from local relational state.
- Any new term must answer in code comments:
  - "What STE-native mechanism does this represent?"
  - "Why is this not a borrowed assumption?"
- If a proposal cannot be explained in ontology-native terms, do not merge it.

## Current State (As Of 2026-03-05)
Implemented:
- all-pairs field interactions (bond graph removed),
- overlap-capped attraction (prevents singular dot collapse),
- relative choke formation/lifecycle (absolute thresholds removed),
- emergent wave propagation model (time-budget, density-dependent speed),
- spin evolution via viscous torque (no unconditional spin decay),
- close-range spin-coupled parcel interaction,
- new saturation/pressure closure state:
  - saturation `S = C / <C_local>`
  - permeability `K = 1 / (1 + S)`
  - pressure potential `P = C * (1 - K)`
- pre-contact pressure force channel in `apply_forces`,
- proton + nebula views both show saturation/pressure diagnostics (`sat>1`, `fronts`, `Savg`) and pressure halos.
- diagnostics ledger in engine (`diagnostics.rs`) with conservation and force residuals,
- timestep convergence integration test (`tests/convergence.rs`),
- baseline scale-invariance integration test (`tests/scale_invariance.rs`),
- compound coexistence diagnostics in HUD (`pairs`, `dwell`, `pot`, `yield`),
- chirality diagnostics in HUD (`chi`, `zc`, `lock`).

Known caveats:
- pressure channel is early-stage and intentionally conservative (gradient-driven only) to preserve baseline attraction tests,
- diagnostics framework is still ad hoc in HUD and tests; no unified benchmark runner yet,
- centroid recycle can bias long-run morphology in visual modes.

## Immediate Objective
Move from "looks plausible" to "quantitatively defensible" via a diagnostics-first workflow.

Current execution priority (time-boxed):
- Run a focused 2-day "quantum ontology assassination" sprint on `physics-refine`.
- Defer new `game-dev` implementation work until sprint conclusions are documented.

## Phase Plan

### Phase 1: Diagnostics Backbone (Priority)
Goal: make every major statement falsifiable.
- Add conservation ledger per tick:
  - total STE,
  - linear momentum,
  - angular momentum,
  - kinetic + shell/choke energy proxies.
- Add action-reaction residual checks on force pairs.
- Add timestep convergence harness (`dt`, `dt/2`, `dt/4`).
- Emit machine-readable run artifacts (CSV/JSON).

Exit criteria:
- drift and residuals are measurable and stable,
- convergence plots are reproducible by script.

### Phase 2: Scale-Invariance Validation
Goal: prove same law stack across scales.
- Define dimensionless initialization template.
- Run proton/nebula/larger-scale comparisons.
- Compare normalized observables:
  - `g(r/r0)`,
  - structure/saturation histograms,
  - choke density and phase fractions,
  - `Savg` and fronts density.

Exit criteria:
- normalized curves collapse within tolerance across scales.

### Phase 3: Thermodynamic Closure Hardening
Goal: make saturation-pressure channel academically robust.
- Empirically fit `P(S)` from runs and report residuals.
- Test alternate derived closures (same variables, no hard thresholds).
- Separate force subchannels in diagnostics:
  - attraction,
  - pressure,
  - spin coupling.

Exit criteria:
- closure form is justified by data, not appearance.

### Phase 4: Publication-Grade Evidence Pack
Goal: withstand skeptical review.
- Produce automated report with:
  - invariants drift,
  - convergence,
  - phase map,
  - ablation matrix,
  - scale-collapse figures.
- Keep reproducible seeds and scripts committed.

Exit criteria:
- third party can rerun and reproduce headline plots.

## Branch Strategy (Dual Track)
Active branches:
- `physics-refine`: ontology + diagnostics + closure work.
- `game-dev`: gameplay loop, UX, progression, content, economy.

Workflow rules:
- `physics-refine` may change engine math and diagnostics only.
- `game-dev` consumes stable exported metrics/APIs and should avoid depending on unstable internals.
- Merge direction is one-way by default:
  - `main` <- `physics-refine` (after diagnostics gates pass)
  - `main` <- `game-dev` (after gameplay acceptance passes)
- If `game-dev` needs new telemetry, add it in `physics-refine` behind stable interfaces.
- Keep ontology guardrails enforced on both branches.

Release policy:
- Public builds default to stable gameplay mechanics.
- Experimental physics mode is opt-in until diagnostics confidence gates are met.

### Physics-Refine -> Main Confidence Gates (v1)
All gates must pass on the same commit before merge:
- AR residual gate:
  - `max(abs(force_ar_residual)) <= 1e-6` over benchmark run.
- STE drift gate:
  - `abs(ste_total_drift_fraction) <= 1e-4` over benchmark run.
- Convergence gate:
  - `tests/convergence.rs` passes (`dt`, `dt/2`, `dt/4` harness).
- Scale baseline gate:
  - `tests/scale_invariance.rs` passes and normalized observables remain within configured tolerance.
- Diagnostics integrity gate:
  - `tests/diagnostics_artifacts.rs` and `tests/baseline_report.rs` both pass.

Verification command (local):
`cargo test --manifest-path engine/Cargo.toml --test convergence --test scale_invariance --test chirality --test diagnostics_artifacts --test baseline_report`

Decision rule:
- Any failed gate blocks merge and requires either:
  - a targeted fix with unchanged ontology assumptions, or
  - a documented ontology-level hypothesis update in commit notes.

## Game Product Direction (Recorded)
Primary product path:
- Build a story-driven, mission-based sandbox first.
- Use STE physics to generate local world behavior and event dynamics.
- Keep simulation scope local/chunked for performance and production feasibility.

Why this path:
- Playability and ship speed are the priority.
- Full voxel-world simulation at sand-grain scale is a later-stage effort.
- Revenue and player feedback from a focused game can fund larger sandbox ambitions.

Design intent:
- Physics should shine through world behavior, not require players to learn equations.
- Core loop should be understandable in player language (stability, pressure fronts, surge, collapse, extraction).

Deferred scope (not MVP):
- Infinite Minecraft-style voxel world.
- Planet-scale fully simulated terrain.
- Massive streaming/storage/netcode systems.

## Change Protocol (To Avoid Regressions)
For each physics change:
1. State hypothesis.
2. Identify invariant risk.
3. Implement smallest change.
4. Run diagnostics suite.
5. Record pass/fail and next action in commit notes.

## Open Questions
- Exact long-range form of pressure kernel and interaction range scaling.
- Best energy bookkeeping for shell/choke state to close the thermodynamic loop.
- Boundary conditions for science runs (reduce visual-mode recycle bias).

## Short-Term Next Actions
1. `physics-refine`: commit and tag current diagnostics milestone.
2. `physics-refine`: define confidence gates for merge to `main` (AR residual, STE drift, scale baseline).
3. `physics-refine`: execute 2-day STE tunneling benchmark sprint (pre-choke permeation vs stochastic baseline).
4. `physics-refine`: publish sprint readout with pass/fail criteria, residuals, and ontology implications.
5. `game-dev`: after sprint readout, write one-page MVP spec for story-driven chunk sandbox.
6. `game-dev`: scaffold game architecture around a stable simulation adapter interface.
7. `game-dev`: implement first publishable core loop using current stable metrics.

## Scope Recovery Checklist
If context is compressed, resume in this order:
1. Re-read this file.
2. Re-assert Ontology Guardrails before making any physics edits.
3. Confirm current physics stack still matches "Current State" above.
4. Run diagnostics baseline.
5. Confirm branch roles (`physics-refine` vs `game-dev`) before coding.
6. Continue from "Short-Term Next Actions" item 1.

## Decompression Handoff
When resuming after context compression, restate these six anchors first:
1. Ontology-first is the primary direction.
2. Physics work stays on `physics-refine`; gameplay work stays on `game-dev`.
3. Diagnostics gate every physics merge (conservation, AR residual, convergence, scale baseline).
4. Compound/chirality metrics are core observables (`pairs`, `dwell`, `pot`, `yield`, `chi`, `zc`, `lock`).
5. Current product direction: story-driven chunk sandbox first; full voxel world deferred.
6. Next research target: STE tunneling benchmark (pre-choke permeation model).
