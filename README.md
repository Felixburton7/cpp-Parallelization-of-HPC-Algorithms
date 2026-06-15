# MPI Parallelisation of Molecular Dynamics

A C++17 / MPI molecular-dynamics solver written for the University of Cambridge. Velocity-Verlet integration for a 1D anharmonic oscillator and a 3D Lennard-Jones fluid, with a domain-decomposed parallel force computation. Scored 93% grade. 

**Full write-up:** [WA2_MPI_Parallelisation_of_Molecular_Dynamics.pdf](WA2_MPI_Parallelisation_of_Molecular_Dynamics.pdf)

---

## What's in here

- C++17 + MPI, domain-decomposed pair-force computation
- Velocity-Verlet integrator, validated to second-order accuracy
- Reproduces Rahman's 1964 radial distribution function for liquid argon
- Strong and problem-size scaling measured on a multi-node HPC cluster

---

## Parallel scaling

Strong-scaling speedup and parallel efficiency on up to 64 MPI processes, with a cost breakdown showing where communication starts to dominate. Full validation (Verlet convergence, energy conservation, RDF vs Rahman 1964) is in the [write-up](WA2_MPI_Parallelisation_of_Molecular_Dynamics.pdf).

<p align="center">
  <img src="results/results3_figure10abc_strong_scaling.png" width="85%" alt="Strong scaling" />
</p>

---

## Source layout

The solver, tests, and scripts live under [md-mpi/](md-mpi/). See [md-mpi/README.md](md-mpi/README.md) for full build, test, and run instructions.

```
md-mpi/
├── include/      # headers
├── src/          # solver source
├── tests/        # unit tests
├── scripts/      # data generation, plotting, validation
└── Makefile
```

## Build and run

```bash
cd md-mpi
make
make test
bash scripts/run_results.sh
```

Requires `mpicxx`, an MPI runtime, a C++17 compiler, and Python 3 with `numpy` and `matplotlib`.
