# Nonlinear Driven Pendulum and Sensitivity to Initial Conditions

A numerical study of a damped, periodically driven nonlinear pendulum, focusing on the sensitivity of its trajectories to nearby initial conditions.

## Overview

This project investigates the dynamics of a nonlinear driven pendulum by numerically solving its equation of motion. Two trajectories with nearly identical initial conditions are compared to examine how small initial differences evolve over time.

The project also explores how the observed trajectory separation changes with the driving amplitude.

## Mathematical Model

The equation of motion is:

$$
\ddot{\theta}+q\dot{\theta}+\sin(\theta)
=F_D\cos(\Omega_D t)
$$

where:

- $\theta$ is the angular displacement.
- $q$ is the damping coefficient.
- $F_D$ is the driving amplitude.
- $\Omega_D$ is the driving angular frequency.

By defining the angular velocity as $\omega=\dot{\theta}$, the equation becomes a system of first-order differential equations:

$$
\dot{\theta}=\omega
$$

$$
\dot{\omega}=-q\omega-\sin(\theta)+F_D\cos(\Omega_Dt)
$$

## Numerical Method

The system is solved using Python and SciPy's `solve_ivp` numerical integration function.

Two nearby initial conditions are considered:

- First trajectory: $\theta_1(0)=0.2$
- Second trajectory: $\theta_2(0)=0.200001$
- Initial angular velocity: $\omega(0)=0$

The main simulation parameters are:

| Parameter | Value |
|---|---:|
| Damping coefficient $q$ | $0.5$ |
| Driving amplitude $F_D$ | $1.2$ |
| Driving frequency $\Omega_D$ | $2/3$ |
| Initial angular difference | $10^{-6}$ |
| Simulation interval | $0 \leq t \leq 100$ |
| Number of time points | 10,000 |

## Results

For the selected parameters, the initial angular difference between the two trajectories is approximately $10^{-6}$. During the simulation, the maximum absolute angular difference reaches approximately $0.481$.

A parameter study was performed by varying the driving amplitude from $F_D=0.8$ to $F_D=1.4$, while keeping the other parameters and initial conditions fixed. The largest trajectory separation among the tested amplitudes occurs at $F_D=1.20$.

### Largest Lyapunov Exponent

The largest Lyapunov exponent was estimated using three numerical approaches:

- **Variational equations:** approximately $0.13$.
- **Two-trajectory method:** $0.13251$.
- **Poincaré-period renormalization:** $0.13023$.

The estimates obtained from the two independent trajectory-based methods differ by approximately $1.72\%$. Their agreement, together with the variational-equation estimate, supports the numerical consistency of a positive largest Lyapunov exponent:

$$
\lambda_{\max}\approx 0.13
$$

A positive largest Lyapunov exponent indicates exponential sensitivity to small perturbations in the initial conditions.

### Poincaré Section

The Poincaré section was constructed by sampling the system once per driving period, after removing an initial transient.

The resulting section exhibits a structured, narrow, and nontrivial distribution of points. This provides additional information about the long-term dynamics and is consistent with a complex attractor structure.

### Interpretation

The observed trajectory separation, the positive largest Lyapunov exponent obtained using multiple numerical approaches, and the structure of the Poincaré section together provide strong numerical evidence consistent with chaotic dynamics for the investigated parameter values.

These conclusions apply to the selected parameters and numerical setup; further parameter-space analysis would be needed to characterize the full range of dynamical regimes.

## Numerical Validation

The numerical results are checked by repeating the simulations with different solver tolerances.

The maximum trajectory separation obtained using the original solver tolerances is approximately $0.48065$, while the result using stricter tolerances is approximately $0.48034$.

The close agreement supports the numerical consistency of the observed trajectory separation.

## Model Limitations

1. The model assumes linear damping and sinusoidal external forcing. Other physical effects, such as nonlinear friction, noise, and parameter uncertainty, are not included.

2. The numerical conclusions are specific to the investigated parameter range and initial conditions. Different values of the damping coefficient, driving amplitude, or driving frequency may lead to different dynamical regimes.

3. Numerical estimates of the largest Lyapunov exponent depend on integration accuracy, transient removal, renormalization interval, and total integration time. Therefore, convergence and cross-validation are important when interpreting the result.

## Requirements

- Python 3.14.7
- NumPy
- SciPy
- Matplotlib
- Jupyter Notebook
- IPython Kernel

The exact package versions are listed in `requirements.txt`.

## Installation and Usage

Clone the repository:

```bash
git clone https://github.com/AbolfazlAmiri1998/nonlinear-driven-pendulum.git
cd nonlinear-driven-pendulum
```

Create and activate a virtual environment on Windows:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

Install the required packages:

```bash
python -m pip install -r requirements.txt
```

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open `nonlinear_driven_pendulum.ipynb` and run the notebook cells.

## Repository Structure

```text
nonlinear-driven-pendulum/
│
├── nonlinear_driven_pendulum.ipynb
├── requirements.txt
└── .gitignore
```

## Future Work

Possible extensions include:

- Mapping the transition between regular and chaotic dynamics over a wider parameter range.
- Constructing bifurcation diagrams as a function of the driving amplitude or frequency.
- Investigating how the largest Lyapunov exponent changes across different dynamical regimes.
- Studying the influence of damping and driving frequency on the structure of the attractor.
- Comparing numerical predictions with experimental driven-pendulum systems.

## Author

**Abolfazl Amiri**

GitHub: [AbolfazlAmiri1998](https://github.com/AbolfazlAmiri1998)