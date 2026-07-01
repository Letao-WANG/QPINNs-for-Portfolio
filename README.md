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
| `run_QPINN_MPS_low_rank.ipynb` | Fixed-volatility Merton HJB experiment (D=2,R=1). This corresponds to the two-dimensional input case `(t,x)` and compares QPINN, Quantum-inspired PINN, Counterpart PINN, and FC PINN. |
| `run_QPINN_MPS_high_rank.ipynb` | Volatility-input Merton HJB experiment (D=3,R=2). This corresponds to the three-dimensional input case `(t,x,sigma)`, where volatility is treated as an additional input variable. |

## Saved Data

| Folder | Contents |
| --- | --- |
| `results/` | Saved outputs for the fixed-volatility experiment (D=2,R=1), including losses, trained model weights, seeds, and run configurations. |
| `results_parametric_volatility/` | Saved outputs for the volatility-input experiment (D=3,R=2), including losses, trained model weights, seeds, and run configurations. |

## Experiment Mapping

The fixed-volatility experiment (D=2,R=1) solves the HJB PDE with a constant volatility
parameter. In the paper, this is the first numerical experiment for the Merton
portfolio optimization problem.

The volatility-input experiment (D=3,R=2) treats volatility as an input variable, changing
the model input from `(t,x)` to `(t,x,sigma)`. In the paper, this is the
parametric-volatility HJB experiment used to test the models on a less separable
solution structure.

The Theorem 3 verification notebook is separate from the HJB experiments. It
checks the constructive tensor-decomposed polynomial implementation directly.
In addition, the HJB experiment notebooks include a PennyLane verification that
compares the torch quantum-circuit implementation against PennyLane to verify the circuit output.

## Training and Plotting Mode

Both `run_QPINN_MPS_low_rank.ipynb` and `run_QPINN_MPS_high_rank.ipynb` expose a
`train_mode` flag near the beginning of the notebook:

```python
train_mode = False
```

Set `train_mode=True` to run the full training loop and save the generated
losses, model weights, seeds, and run configuration files to the local results
folder. Set `train_mode=False` to skip training, load the existing local result
files, and generate the figures directly from the saved data.

For the low-rank fixed-volatility notebook, saved data is read from and written
to `results/`. For the high-rank volatility-input notebook, saved data is read
from and written to `results_parametric_volatility/`.

## Reproducibility Environment

The saved HJB experiment data was generated with `torch_device=mps` and
`torch_dtype=torch.float32`. The key environment versions are:

| Package | Version |
| --- | --- |
| Python | 3.11.11 |
| PyTorch | 2.2.2 |
| NumPy | 1.26.4 |
| torch-optimizer | 0.3.0 |
