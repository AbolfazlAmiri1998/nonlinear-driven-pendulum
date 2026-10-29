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

For the selected parameters, the initial angular difference is approximately $10^{-6}$. By the end of the simulation, the maximum absolute angular difference reaches approximately $0.481$.

A parameter study is also performed by varying the driving amplitude from $0.8$ to $1.4$ while keeping the other parameters and initial conditions fixed.

The largest trajectory separation among the tested driving amplitudes occurs at $F_D=1.20$, with a maximum difference of approximately $0.481$.

These results indicate sensitivity to initial conditions for the selected simulation parameters and time interval. However, trajectory divergence alone is not sufficient to establish mathematical chaos.

## Numerical Validation

The numerical results are checked by repeating the simulations with different solver tolerances.

The maximum trajectory separation obtained using the original solver tolerances is approximately $0.48065$, while the result using stricter tolerances is approximately $0.48034$.

The close agreement supports the numerical consistency of the observed trajectory separation.

## Model Limitations

1. The model assumes linear damping and sinusoidal external forcing. Other physical effects, such as nonlinear friction and measurement noise, are not included.
2. Trajectory divergence alone does not prove chaos. Further analysis, such as estimating the largest Lyapunov exponent or constructing a Poincaré section, would be needed for a stronger conclusion.

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

- Estimating the largest Lyapunov exponent.
- Constructing Poincaré sections.
- Investigating the effect of damping and driving frequency.
- Exploring the system's behavior over a wider range of parameters.

## Author

**Abolfazl Amiri**

GitHub: [AbolfazlAmiri1998](https://github.com/AbolfazlAmiri1998)