# OptiLine-Py: experiments

Notebooks, inputs and videos for the experiments of the paper
*OptiLine-Py: A Raceline Optimisation Framework*.

The OptiLine-Py package itself:
- GitHub: [github.com/amirali78frz/OptiLine](https://github.com/amirali78frz/OptiLine)
- PyPI: [pypi.org/project/OptiLine-Py](https://pypi.org/project/OptiLine-Py/)

## Requirements

```bash
pip install OptiLine-Py==0.2.10 pandas threadpoolctl jupyter
```

`OptiLine-Py` installs its own dependencies, including `fbga-py` (FBGA velocity
profiler) and `MLTS-point-mass` (point-mass optimal control). Run each notebook
from this folder. Figures are written to `paper_figs/`, which is created on the
first run.

The zeroth-order solvers are unseeded and every result is the mean over three
runs, so a rerun reproduces the reported numbers up to their standard deviation.

## Notebooks

| Notebook | Content | Paper |
|---|---|---|
| `Experiments.ipynb` | Vehicle 1 on Brands Hatch, Melbourne, Catalunya and Budapest: shortest path, minimum curvature, PM-OCP, bilevel (BZO) and direct blackbox (BBA) with ZORM and CMA-ES; computation times; initialisation modes; convergence; the RMS longitudinal-acceleration cost; QC/PQC verification on all 25 maps | Vehicle 1 results, QC and PQC verification, Appendix A |
| `Experiments_GGV_extraction.ipynb` | Full-scale Catalunya with the GGV envelope extracted from the double-track minimum-lap-time solution (MLT-DT): all methods against PM-OCP and MLT-DT, velocity profiles, racelines, path length and envelope usage | Benchmarking against an OCP-extracted GGV envelope |
| `Experiments_nondiff.ipynb` | Two non-differentiable costs on Budapest: the time spent near the acceleration limit, and the lap time of a simulated closed loop (kinematic bicycle, tracking controller, slow steering actuator), with the videos in `animations/` | Custom non-differentiable cost; closed-loop trackability |
| `Experiments_fbga.ipynb` | The FBGA profiler in place of the forward--backward profiler, for both proposed methods on Sepang, plus further FBGA tests (generic g--g envelopes, downforce, g--g usage, discretisation) | Appendix B |

## Folders

- **`maps/`**: the 25 real circuits of the track library (F1TENTH racetracks,
  scaled from the TUM racetrack database). Each folder holds
  `<name>_centerline.csv` with columns `x, y, w_tr_right, w_tr_left` in metres,
  and the circuit image and its `.yaml`.
- **`input_files/`**:
  - Vehicle 1: the GGV envelope (`ggv.csv`), the drive limit
    (`ax_max_machines.csv`), and the vehicle and solver parameters
    (`racecar.ini`).
  - Vehicle 2, the full-scale Catalunya case: the track (`Catalunya.txt`), the
    vehicle (`vehicle_2/vehicle.json`), the extracted GGV envelope
    (`ggv_sportcar.json`), and the two reference solutions, MLT-DT
    (`mlt_dt_sol_selected.csv`) and PM-OCP (`mlts_pm_solution.csv`).
- **`animations/`**: one video per line of the closed-loop example on Budapest,
  driven at its planned speed: minimum curvature, centreline, lap-time optimum,
  PM-OCP, and the median BBA-ZO and BBA-CMA runs. The left panel shows the
  whole track and where the car left the limits; the right panel follows the car
  and plots its excursion beyond the limits along the lap.
