# Adaptive Learning Lab

Reproducible simulations of rating systems and item selection for adaptive
learning. The first study reproduces _Keeping Elo alive_ and compares standard
Elo, parallel Elo and Urnings. Further experiments investigate sparse data,
changing abilities, item exposure and departures from model assumptions.

## Research scope

1. Reproduce the published simulation conditions and numerical results.
2. Compare estimators and selection policies under controlled synthetic conditions.
3. Investigate learning and forgetting with explicit assumptions and sensitivity
   analyses.
4. Publish reproducible methods, results and limitations.

The [research plan](docs/research-plan.md), revision 0.2, defines the experiments,
acceptance criteria and computational approach. The
[source register](docs/source-register.md) identifies the paper, pinned author
implementation and unresolved reproduction questions.

## Project status

Planning stage. Simulation software and experiment results are not yet available.
The proposed implementation uses Python for an independent simulator and
analysis, with the authors' R/C implementation as a separately managed reference.

Experiments use synthetic data. Accurate ability estimates do not by themselves
establish improved learning, retention or real-world assessment validity.
