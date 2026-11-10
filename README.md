# Magnetic-processing-with-GeoPhy

[![DOI](https://zenodo.org/badge/1452708457.svg)](https://doi.org/10.5281/zenodo.24110955)

Jupyter Notebook workflow for processing magnetometric data (gradiometry, values in nT) with the **GeophPy** library (version used in the notebook: 0.32.2).

## Contents

```
notebooks/Geomag_elab_grad_nT.ipynb   # full workflow (outputs cleared)
data/raw/                             # input XYZ data (not versioned)
outputs/                              # maps, histograms, PDFs (not versioned)
requirements.txt
```

## Processing sequence

1. Import of the ASCII file (`.XYZ`, space-delimited; columns x, y, z = gradient; column 4, total field, is set up but commented out).
2. `threshold` (−10/+10) and `peakfilt` (median, halfwidth 5, threshold 15, absolute mode).
3. `destripecon` (additive, median reference) and `zeromeanprofile` (median).
4. Linear interpolation and Wallis filter (`wallisfilt`, 9×9 window).
5. Profile cross-correlation maps (`correlation_plotmap`, `correlation_plotsum`) and mean cross-track profiles (`meantrack_plot`).
6. Descriptive statistics (mean, median, standard deviation, skewness, kurtosis) and histogram.

`festoonfilt`, `ploughfilt` and `medianfilt` are included but commented out.

## Usage

1. Create an environment with the dependencies in `requirements.txt` and install GeophPy following the library's official documentation.
2. Copy the `.XYZ` file into `data/raw/` and set `file_path` in cell 2 of the notebook.
3. Run the cells in order. The filters modify `grad_ds` in place, so re-running an intermediate cell without restarting from the top applies that filter twice.

## Notes and limitations

- The parameters (thresholds, window sizes, Wallis targets) are those of the original case study and must be adapted to each survey.
- Figure titles carry the name of the case-study site (Rocavecchia).
- Units are not consistent within the notebook: files are named in nT, whereas histogram labels read nT/m. This should be checked against the instrument and the export format.
- The notebook saves files under fixed names in the working directory, so files with the same name are overwritten.

## License

MIT (see `LICENSE`). Compatibility with the GeophPy license should be verified.
