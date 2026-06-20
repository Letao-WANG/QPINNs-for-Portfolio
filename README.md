# QPINNs for Portfolio Optimization

This repository contains the experiment code and saved results for the paper
`Learning PDEs for Portfolio Optimization with Quantum Physics-Informed Neural Networks`.

The paper studies QPINN and Quantum-inspired PINN models for solving the
Hamilton-Jacobi-Bellman (HJB) PDE from the Merton portfolio optimization
problem. The files in this repository correspond to the numerical validation
and experiments reported in the paper.

## Notebooks

| Notebook | Corresponding part of the paper |
| --- | --- |
| `verify_theorem3_td_qnn.ipynb` | Verification of Theorem 3. This notebook trains the constructive tensor-decomposed quantum model on the explicit target polynomial used in the theorem validation. |
| `run_QPINN_MPS_low_rank.ipynb` | Fixed-volatility Merton HJB experiment. This corresponds to the two-dimensional input case `(t,x)` and compares QPINN, Quantum-inspired PINN, Counterpart PINN, and FC PINN. |
| `run_QPINN_MPS_high_rank.ipynb` | Volatility-input Merton HJB experiment. This corresponds to the three-dimensional input case `(t,x,sigma)`, where volatility is treated as an additional input variable. |

## Saved Data

| Folder | Contents |
| --- | --- |
| `results/` | Saved outputs for the fixed-volatility experiment, including losses, trained model weights, seeds, and run configurations. |
| `results_parametric_volatility/` | Saved outputs for the volatility-input experiment, including losses, trained model weights, seeds, and run configurations. |

## Experiment Mapping

The fixed-volatility experiment solves the HJB PDE with a constant volatility
parameter. In the paper, this is the first numerical experiment for the Merton
portfolio optimization problem.

The volatility-input experiment treats volatility as an input variable, changing
the model input from `(t,x)` to `(t,x,sigma)`. In the paper, this is the
parametric-volatility HJB experiment used to test the models on a less separable
solution structure.

The Theorem 3 verification notebook is separate from the HJB experiments. It
checks the constructive tensor-decomposed polynomial implementation directly.
