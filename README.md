# pqe1: optimal lag times under uncertain antibiotic exposure

My PhD qualifying exam (PQE) project, spring 2019: a modelling study of how bacteria
should time their exit from lag phase when antibiotic exposure is unpredictable.

## Background and question

Fridman et al. (*Nature*, 2014) exposed *E. coli* to repeated cycles of antibiotic
and found that the populations' lag time evolved to match the duration of the exposure:
cells still dormant while the drug is present survive it. In reality both sides are
noisy: lag times vary from cell to cell, and an exposure need not last the same time
every cycle. This project asked which lag-time distribution maximizes population growth
in that setting, and how the optimum shifts as the exposure becomes less predictable.

## Model

Each cell stays in lag for a random time drawn from a lag-time distribution (normal,
later exponential). An antibiotic is present for a random time; cells that resume
growth before it ends are killed, and the survivors grow exponentially until the end
of the cycle. Fitness is the population's fold change over a cycle, averaged over many
cycles.

## What was done

- Monte Carlo simulation of the model, scanning the mean and spread of lag times;
  parallelized on Harvard Medical School's O2 cluster (SLURM) with Dask.
- An integral expression for the expected fitness, evaluated numerically with SciPy,
  which replaced the slower and noisier sampling.
- Scans of the fitness landscape and its optimum as the antibiotic duration becomes
  more variable, for different regrowth times and for normal and exponential lag-time
  distributions.

## Contents

Notebooks are named by date (YYMMDD) and kept as they were run in 2019, outputs included.

| Notebooks | Content |
|---|---|
| `190313_Modular`, `190320_Parallelization!` | Model and Monte Carlo simulations (results in `data/`) |
| `190402_LoadData` | Analysis of the simulations |
| `190409_Integration`, `IntegrationExponential` | Numerical integration for normal and exponential lag times (results in `idata/`, `edata/` and the top-level `iexp_*` files) |
| `190416_LoadIntegration`, `190417_LoadExponential` | Analysis and figures (the `.png` and `.eps` files at the top level) |
| `190423_IntegrationMixed`, `190424_MathSandbox` | Scratch |

Each `.npy` result file has a `_meta.csv` beside it with the run's parameters.

Python 3.7 with NumPy, SciPy, Matplotlib, seaborn, Dask and dask-jobqueue.
