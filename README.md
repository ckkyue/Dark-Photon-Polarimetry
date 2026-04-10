# Dark Photon Polarimetry

This repository contains the analysis code used to search for dark photon or axion soliton signatures in radio polarimetry observations of Sagittarius A*.

The notebooks compare observed polarization angles against theory predictions, scan a grid of soliton parameters, and extract upper limits on the dark photon coupling strength from chi-squared fits.

## What Is In This Repository

- `analysis.ipynb`: main analysis notebook. It loads the observation data, combines the day 81 and day 82 measurements, evaluates chi-squared values over the parameter grid, and produces the constraint plots.
- `in_medium.ipynb`: theory notebook for the in-medium calculation of the observable field and plasma suppression effects.
- `soliton.nb`, `dp_lab.nb`, `smbh.nb`: Mathematica notebooks with the underlying derivations and theoretical inputs.
- `sgrdata/`: observation data for day 81 and day 82.
- `paralist_all_SgrltNE.dat`: parameter grid used by the analysis.
- `chisqs_all_total_day81.npy`, `chisqs_all_total_day82.npy`, `chisqs_all_total_day81to82.npy`: precomputed chi-squared results saved by the analysis notebook.
- `Figure/`: generated figures, including the constraint curves and field visualizations.
- `2501.13849v2.pdf`: reference paper for the method and model.

## Analysis Workflow

1. Load the polarization measurements from `sgrdata/day81` and `sgrdata/day82`.
2. Build the combined day 81 to 82 dataset by concatenating and time-sorting the two days.
3. Load the theoretical interpolation data and the parameter list from `paralist_all_SgrltNE.dat`.
4. Scan over mass, coupling, phase, and background offset to compute the best chi-squared value for each parameter point.
5. Convert the chi-squared surface into 90 percent and 95 percent confidence level upper limits on the coupling.
6. Save the resulting arrays and plots into the repository.

## Data Layout

Each day folder under `sgrdata/` contains the observation channels used by the notebook:

- `dark.npy`: dark reference channel
- `blue1.npy`, `blue2.npy`: repeated blue-channel measurements
- `red1.npy`, `red2.npy`: repeated red-channel measurements

The repeated blue and red files are used to estimate measurement uncertainty, while the dark channel provides the reference curve.

## Requirements

The notebooks use Python together with common scientific packages:

- numpy
- pandas
- scipy
- matplotlib
- joblib
- tqdm
- jupyter

## How To Run

1. Open `analysis.ipynb` in Jupyter or VS Code.
2. Run the cells in order.
3. If the cached chi-squared arrays already exist, the notebook will reuse them instead of recomputing.
4. Review the generated figures in `Figure/`.

If you want to regenerate the theoretical inputs, update `in_medium.ipynb` or the Mathematica notebooks first, then rerun the analysis notebook.

## Notes

- The main results are expressed as upper limits on the dark photon coupling as a function of mass.
- The repository is organized as a research workflow rather than a packaged software project, so the notebooks are the primary entry points.

## License

See `LICENSE.txt`.