# Nonlinear Dynamics and Chaos in a Driven Pendulum

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A numerical investigation of a damped, periodically driven nonlinear pendulum, focusing on chaotic dynamics, sensitivity to initial conditions, Lyapunov exponents, Poincaré sections, and coexisting regular and chaotic attractors.

## Overview

This project investigates the nonlinear dynamics of a periodically driven, damped pendulum by numerically solving its equations of motion.

The study begins by examining the sensitivity of nearby trajectories to small differences in their initial conditions. It then explores the dependence of the observed dynamics on the driving amplitude and investigates the system's long-term behavior using several complementary numerical techniques.

The analysis includes:

- Numerical integration of the nonlinear equations of motion.
- Sensitivity to initial conditions.
- Parameter dependence of trajectory separation.
- Largest Lyapunov exponent estimation using independent numerical approaches.
- Full Lyapunov spectrum calculation using the variational equations and QR decomposition.
- Poincaré sections for investigating long-term dynamics.
- Coexisting regular and chaotic attractors.
- Preliminary basin of attraction analysis.

The project is implemented in Python using NumPy, SciPy, and Matplotlib.

## Mathematical Model

The dimensionless equation of motion of the driven damped pendulum is

$$
\ddot{\theta}+q\dot{\theta}+\sin(\theta)
=F_D\cos(\Omega_D t)
$$

where:

- $\theta$ is the angular displacement.
- $q$ is the damping coefficient.
- $F_D$ is the driving amplitude.
- $\Omega_D$ is the driving angular frequency.
- $t$ is dimensionless time.

Defining the angular velocity as

$$
\omega=\dot{\theta},
$$

the second-order equation can be expressed as a system of first-order differential equations:

$$
\dot{\theta}=\omega
$$

$$
\dot{\omega}
=-q\omega-\sin(\theta)
+F_D\cos(\Omega_Dt)
$$

This formulation is used for numerical integration and subsequent dynamical analysis.

## Numerical Methods

The equations of motion are solved using Python's `scipy.integrate.solve_ivp` function.

Numerical integration is performed with adaptive time stepping and controlled relative and absolute error tolerances.

### Sensitivity to Initial Conditions

Two trajectories with nearly identical initial conditions are considered:

- First trajectory: $\theta_1(0)=0.2$
- Second trajectory: $\theta_2(0)=0.200001$
- Initial angular velocity: $\omega_1(0)=\omega_2(0)=0$

The main simulation parameters are:

| Parameter | Value |
|---|---:|
| Damping coefficient $q$ | $0.5$ |
| Driving amplitude $F_D$ | $1.2$ |
| Driving frequency $\Omega_D$ | $2/3$ |
| Initial angular difference | $10^{-6}$ |
| Simulation interval | $0\leq t\leq100$ |
| Number of evaluation points | 10,000 |

For these parameters, the initial angular separation is approximately $10^{-6}$, while the maximum absolute angular separation reaches approximately $0.481$.

A parameter study was also performed by varying the driving amplitude from $F_D=0.8$ to $F_D=1.4$, with the other parameters and initial conditions held fixed.

Among the tested amplitudes, the largest trajectory separation was observed at $F_D=1.20$.

Trajectory separation alone does not establish chaos; therefore, additional dynamical indicators are used.

## Chaos Analysis and Lyapunov Exponents

The largest Lyapunov exponent is used to quantify the average exponential growth or decay of infinitesimal perturbations.

A positive largest Lyapunov exponent indicates exponential sensitivity to initial conditions.

For the parameter set

$$
q=0.5,\qquad
F_D=1.2,\qquad
\Omega_D=\frac{2}{3},
$$

the largest Lyapunov exponent was estimated using three numerical approaches:

| Numerical method | Largest Lyapunov exponent |
|---|---:|
| Variational equations | Approximately $0.13$ |
| Two-trajectory method | $0.13251$ |
| Poincaré-period renormalization | $0.13023$ |

The two trajectory-based estimates differ by approximately $1.72\%$.

The agreement between these independent numerical approaches supports the consistency of the positive largest Lyapunov exponent.

Thus, for this parameter set,

$$
\lambda_{\max}\approx 0.13.
$$

### Full Lyapunov Spectrum

The full Lyapunov spectrum is calculated by integrating the variational equations together with the original dynamical system.

The tangent-space evolution is periodically orthonormalized using QR decomposition to prevent numerical alignment of perturbation vectors.

For a long integration time of 40,000 dimensionless time units, with strict solver tolerances, the estimated exponents are approximately

$$
\lambda_1\approx 0.131
$$

$$
\lambda_2\approx -0.631.
$$

Their sum satisfies

$$
\lambda_1+\lambda_2\approx -0.5.
$$

This is consistent with the constant phase-space divergence of the two-dimensional system:

$$
\nabla\cdot f=-q=-0.5.
$$

The negative sum indicates phase-space contraction due to damping.

The Kaplan–Yorke dimension estimated from this spectrum is approximately

$$
D_{KY}\approx 1.21.
$$

This is a numerical estimate derived from the Lyapunov spectrum, rather than a direct measurement of the geometric dimension of the attractor.

## Poincaré Sections

Poincaré sections are constructed by sampling the system once per driving period:

$$
T_D=\frac{2\pi}{\Omega_D}.
$$

An initial transient is discarded before collecting the sampling points.

For the chaotic parameter regime, the resulting points form a structured and nontrivial distribution.

Poincaré sections are also used to compare the long-term behavior of regular and chaotic trajectories under identical system parameters but different initial conditions.

The observed distributions provide complementary information about the system's long-term dynamics.

## Coexisting Regular and Chaotic Attractors

An important result of this investigation is the numerical observation of coexisting regular and chaotic attractors for the same system parameters.

The following parameters are used:

$$
q=0.5
$$

$$
F_D=1.1092578125
$$

$$
\Omega_D=\frac{2}{3}
$$

Two nearby initial conditions produce different long-term dynamical behaviors:

| Initial condition $(\theta_0,\omega_0)$ | Observed behavior | Largest Lyapunov exponent |
|---|---|---:|
| $(0.265,0)$ | Regular | Approximately $-0.25$ |
| $(0.266,0)$ | Chaotic | Approximately $+0.09$ to $+0.10$ |

The full Lyapunov spectrum provides additional confirmation:

For the regular trajectory,

$$
\lambda_1\approx-0.25,\qquad
\lambda_2\approx-0.25.
$$

For the chaotic trajectory,

$$
\lambda_1\approx+0.097,\qquad
\lambda_2\approx-0.597.
$$

The sum of the two exponents remains approximately $-0.5$, consistent with the system's phase-space divergence.

These results indicate that different attractors can coexist for the same parameter values and that the observed long-term behavior depends on the initial conditions.

The reported exponents are numerical estimates and may vary slightly with integration time and numerical settings.

## Basin of Attraction

A preliminary basin of attraction analysis is performed to investigate how different initial conditions lead to regular or chaotic long-term behavior.

The initial-condition space is sampled over a two-dimensional grid:

$$
0.24\leq\theta_0\leq0.28
$$

$$
-0.05\leq\omega_0\leq0.05.
$$

For each initial condition, the trajectory is integrated and sampled at successive driving periods after an initial transient.

The standard deviation of the wrapped angular Poincaré coordinates is used as a numerical indicator to distinguish the two observed types of behavior.

The resulting basin map illustrates regions classified as regular or chaotic.

Selected points from both regions are independently checked using the full Lyapunov spectrum calculated through QR decomposition.

The independent checks agree with the preliminary basin classification for the tested points.

**Methodological note:** The basin map is based on a finite-resolution grid and a threshold-based classification criterion. Only selected grid points are independently validated using Lyapunov exponents. Consequently, the map provides preliminary numerical evidence of the coexistence of different attractors; it does not establish the fractal nature of basin boundaries.

## Numerical Validation

Numerical reliability is examined through several checks:

1. Repeating trajectory integrations with different solver tolerances.
2. Comparing independent methods for estimating the largest Lyapunov exponent.
3. Varying the renormalization interval and total integration time.
4. Checking the sum of the full Lyapunov spectrum against the expected phase-space divergence.
5. Independently validating selected regular and chaotic initial conditions.

For the initial sensitivity analysis, the maximum trajectory separation obtained with the original solver tolerances is approximately $0.48065$.

Using stricter tolerances, the corresponding result is approximately $0.48034$.

The close agreement supports the numerical consistency of the observed trajectory separation.

Although the Lyapunov estimates show good agreement across independent approaches, their finite-time values retain some dependence on numerical settings and integration duration. Therefore, the reported exponents are presented as approximate values.

## Model Limitations

1. The model assumes linear damping and sinusoidal external forcing. Other physical effects, such as nonlinear friction, noise, and parameter uncertainty, are not included.

2. The numerical conclusions depend on the investigated parameter ranges and initial conditions. Different damping coefficients, driving amplitudes, or driving frequencies may lead to different dynamical regimes.

3. The basin of attraction analysis uses a finite grid and a threshold-based classification method. Its resolution and classification accuracy are therefore limited.

4. Numerical estimates of Lyapunov exponents depend on integration accuracy, transient removal, renormalization intervals, and total integration time. Convergence tests and independent numerical approaches are important for reliable interpretation.

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
├── LICENSE
├── README.md
└── .gitignore
```

## Future Work

Possible extensions include:

- Mapping transitions between regular and chaotic dynamics over a wider parameter range.
- Constructing bifurcation diagrams as functions of the driving amplitude and frequency.
- Investigating the variation of Lyapunov exponents across different dynamical regimes.
- Studying the influence of damping and driving frequency on attractor structure.
- Performing higher-resolution basin analysis and investigating basin boundary geometry.
- Comparing numerical predictions with experimental driven-pendulum systems.

## License

This project is distributed under the MIT License. See the `LICENSE` file for details.

## Author

**Abolfazl Amiri**

GitHub: [AbolfazlAmiri1998](https://github.com/AbolfazlAmiri1998)
