# Project Gargantua: A Relativistic MCMC Rendering Engine

![C++17](https://img.shields.io/badge/C++-17-blue.svg) ![OpenMP](https://img.shields.io/badge/OpenMP-Parallel-red.svg) ![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)

A high-performance, volumetric physics engine that simulates the gravitational lensing of a supermassive black hole. Instead of relying on standard deterministic raytracing, this engine utilizes **Markov Chain Monte Carlo (MCMC)** via the **Metropolis-Hastings algorithm** to solve the high-dimensional light transport integrals of curved spacetime.

## 🌌 Visual Results

![3D Volumetric Sweep](blackhole_3D_sweep_HD.gif)
*Above: 3D Volumetric Sweep demonstrating infinite photon ring resolution and Relativistic Doppler Beaming.*

![Convergence Engine](blackhole_convergence.gif)
*Above: The MCMC algorithm converging on the solution over 20 Million stochastic samples.*

## ⚙️ The Core Engine: Why MCMC?

Standard geometric raytracing fails when rendering black holes because 99% of randomly cast rays fall into the event horizon or scatter into the void. To resolve the infinitely thin "photon ring" where light orbits the black hole, this engine treats rendering as a probability problem.

The solver utilizes **Metropolis Light Transport (MLT)**:
1. **Stochastic Search:** The engine randomly searches the coordinate space until it strikes the accretion disk.
2. **Markov Chain Mutation:** Once light is found, the algorithm takes mathematically weighted Gaussian steps to explore the micro-geometry of the local light paths.
3. **Variance Reduction:** The Metropolis-Hastings acceptance ratio strictly ensures the CPU spends its cycles resolving the most complex, brightest areas of the spacetime curvature, vastly outperforming brute-force sampling.

## 🧮 Physics & Mathematics
* **General Relativity:** Null geodesics are calculated using the Runge-Kutta 4th Order (RK4) numerical integration method.
* **Adaptive Stepping:** The engine dynamically shrinks the integration step size `dt` as photons approach the intense gravity of the event horizon.
* **Relativistic Doppler Beaming:** The accretion disk implements Special Relativity emission physics; the side of the disk rotating toward the observer is drastically blueshifted and brightened, while the receding side is redshifted and dimmed.

## 🚀 Performance & Architecture
Written entirely in **C++17** and optimized with `-ffast-math`. The stochastic workload is fiercely parallelized across all available CPU cores using **OpenMP** `#pragma omp parallel for` directives, allowing the engine to calculate ensembles of independent Markov Chains simultaneously.

The entire architecture is wrapped in a unified Jupyter Notebook, allowing seamless switching between High-Definition Static Rendering, 3D Volumetric Animation, and Interactive Geodesic Exploration.
