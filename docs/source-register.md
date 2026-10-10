# Research sources and provenance

Sources inspected for plan revision 0.2 on 11 October 2026. This register pins
what was available for planning; stage 1 will add file hashes and the exact
figure-to-condition crosswalk used for execution.

## Published study

Maria Bolsinova, Bence Gergely and Matthieu J. S. Brinkhuis, _Keeping Elo alive:
Evaluating and improving measurement properties of learning systems based on
Elo ratings_. DOI [10.1111/bmsp.12395](https://bpspsychub.onlinelibrary.wiley.com/doi/10.1111/bmsp.12395).
First published online 6 June 2025; journal issue 2026, volume 79, pages 95–110.
Use the final article's equations and figure labels as the published target.

[OSF data repository](https://osf.io/yg8p6/) and the article's linked supporting
PDF are reference-data dependencies. Fetches failed during planning. No raw
result files or supplementary-only settings have been validated. Availability,
checksums and exact reuse terms remain stage 1 work. Algorithm development can
proceed from available sources; complete figure reproduction needs an explicit
disposition for unavailable reference material.

## Author implementation

Repository: [mrpogge/ELO_distribution](https://github.com/mrpogge/ELO_distribution).
Pinned commit: `f92a390e4b43c00e265df1cee291db8cd93862f3`.
The source tree and files below were retrieved through GitHub's public API/raw
endpoints. They were inspected, not executed.

| Source at the pinned revision                                                                                                                                                                                                                                                       | Use                                                                                         |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| [README](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/README.md)                                                                                                                                                                       | R/C workflow and source/output organization                                                 |
| [Shared parameters](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/simulations/fix_params.R)                                                                                                                                             | Counts, distributions, step sizes, adaptive targets and separate baseline replication count |
| [R wrappers](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/elo_functions.R)                                                                                                                                                             | Quantiles, shuffled learner order, initialization and C interfaces                          |
| [Core C](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/elo_for_simulations.c)                                                                                                                                                           | Standard and parallel Elo execution audit                                                   |
| [Parallel baseline](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/simulations/double_elo_baseline.R)                                                                                                                                    | 1,100 pairs and higher-replication baseline                                                 |
| [Parallel K sweep](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/simulations/double_elo_K.R) and [target sweep](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/simulations/double_elo_mu.R)  | Condition-specific pair counts                                                              |
| [Outcome measures](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/outcome_measures.R)                                                                                                                                                    | Centering, aggregation windows and hitting-time definitions                                 |
| [Revision simulations](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/revision_simulations.R) and [revision C](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/elo_for_simulations_revision.c) | Urnings comparison, count initialization, smoothing and extra metrics                       |
| [Auxiliary simulations](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/simulations/post_hoc_simulations.R)                                                                                                                               | Diagnostic controls and lagged-rating analysis                                              |
| [License](https://github.com/mrpogge/ELO_distribution/blob/f92a390e4b43c00e265df1cee291db8cd93862f3/LICENSE)                                                                                                                                                                        | Repository includes the GNU GPL version 3 text                                              |

Retain notices and the exact license with any upstream checkout or derived
reference patches. Author code is a separately identified reference. Do not
assume the independent implementation's eventual license covers upstream code
or derived patches. The planned Python implementation follows the
published specification; any code reuse must be recorded explicitly.

## Discrepancies to resolve before reference acceptance

- The main study describes 500 replications, while source figure-baseline
  scripts use `nreps_baseline = 10000`. Preserve both run profiles.
- The upstream README's figure numbering differs from the final paper. Build
  the mapping from actual final figures and analysis scripts.
- Audit averaging windows: some outcome helpers use the latter half of a run,
  while hitting time uses its last 500 recorded points. Match each reported
  quantity's actual definition rather than applying one global window.
- Confirm whether each variance concerns raw ratings, centered ratings or
  aggregated means; retain covariance effects when introducing per-replication
  centering in the independent analysis.
- The pinned revision C file's extra-MSE loop at line 188 contains an apparent
  self-initialized loop counter, `for(int i=i;...)`. This has not been executed
  or diagnosed. Audit compiler diagnostics and a tiny deterministic metric case
  before treating that output as a reference. Keep an unmodified source record
  and a separately documented correction if needed.
- Urnings starts with discrete counts and uses specific probability/logit
  transformations. Resolve text/code notation against the original Urnings
  method before implementing; do not translate a displayed equation blindly.
