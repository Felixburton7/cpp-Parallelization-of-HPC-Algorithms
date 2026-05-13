# MPI Parallelisation of Molecular Dynamics

A C++17 / MPI molecular dynamics solver, written as part of the MPhil in Scientific Computing at the University of Cambridge. The code implements a Velocity-Verlet integrator for both a 1D anharmonic toy model and a 3D Lennard-Jones fluid, and is parallelised with a domain-decomposed force computation using MPI.

**Full write-up:** [WA2_MPI_Parallelisation_of_Molecular_Dynamics.pdf](WA2_MPI_Parallelisation_of_Molecular_Dynamics.pdf)

## Highlights

- C++17, MPI, domain-decomposed pair-force computation
- Velocity-Verlet integration validated against analytical and published reference data
- Reproduces the Rahman (1964) radial distribution function for liquid argon
- Strong and problem-size scaling measured on a multi-node HPC cluster

## Selected Results

### Velocity-Verlet convergence (1D anharmonic oscillator)

Energy-drift error scales as O(Δt²), confirming the integrator is second-order accurate.

![Verlet convergence](results/results1_figure3_convergence.png)

### Lennard-Jones energy conservation

Total energy is conserved over a 100-step production run of the LJ fluid; kinetic and potential energy exchange cleanly.

![LJ energy](results/results2_figure6_lj_energy.png)

### Radial distribution function vs Rahman (1964)

The simulated RDF for liquid argon reproduces the structure reported in [Rahman, *Phys. Rev.* **136**, A405 (1964)](https://doi.org/10.1103/PhysRev.136.A405).

![RDF vs Rahman 1964](results/results2_figure8_rdf_rahman1964.png)

### Problem-size scaling (fixed p = 16)

Wall-clock cost grows linearly with the number of particles N at fixed process count, as expected for an O(N) cutoff-based force evaluation.

![Problem-size scaling](results/results3_figure9ab_problem_size_scaling.png)

### Strong scaling

Speedup and parallel efficiency on up to 64 MPI processes, with the cost breakdown showing where communication starts to dominate.

![Strong scaling](results/results3_figure10abc_strong_scaling.png)

## Source Layout

The solver, tests, and scripts live under [md-mpi/](md-mpi/). See [md-mpi/README.md](md-mpi/README.md) for build, test, and run instructions.

```
md-mpi/
├── include/      # headers
├── src/          # solver source
├── tests/        # unit tests
├── scripts/      # data generation, plotting, validation
└── Makefile
```

## Build And Run

```bash
cd md-mpi
make
make test
bash scripts/run_results.sh
```

Requires `mpicxx`, an MPI runtime, a C++17 compiler, and Python 3 with `numpy` and `matplotlib`.
