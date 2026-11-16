# Cosmo-statistics with Type Ia Supernovae

**Authors:** Benjamín Carrillo, Nicolás Miranda<br>
Departamento de Física, Universidad Técnica Federico Santa María

This repository contains a Python notebook to estimate the deceleration parameter $q_0$, the matter-density parameter $\Omega_{m,0}$ and the Hubble constant $H_0$ using Type Ia supernovae (SNe Ia) from the Pantheon+ catalogue and the distance moduli calibrated by the SH0ES collaboration.

We compare two approaches:

- **Cosmography:** a second-order expansion of the luminosity distance at low redshift, which does not assume a specific cosmological model.
- **Flat ΛCDM:** the luminosity distance of a flat universe with matter and cosmological constant, fitted over the full redshift range.

## Method

1. **Marginalisation over $M$.** Since $H_0$ and the absolute magnitude $M$ are degenerate, we analytically marginalise over the combined offset and minimise

   $$\chi^2_{\mathrm{marg}} = \chi_0^2 - \frac{A^2}{B}$$

   which depends only on $q_0$ (cosmography) or $\Omega_{m,0}$ (ΛCDM). This step does not use any Cepheid calibration.
2. **Deceleration parameter from ΛCDM.** For a flat ΛCDM model, $q_0 = \frac{3}{2}\Omega_{m,0} - 1$.
3. **Hubble constant.** Using the SH0ES distance moduli $\mu_i = m_i - M$, where $M$ is calibrated with Cepheids, we fit $H_0$ with $q_0$ fixed to the value obtained from each approach.
4. **Uncertainties.** Approximate 68.3% intervals from $\Delta\chi^2 = 1$, assuming independent Gaussian errors (diagonal uncertainties of the catalogue).

### Samples

| Sample | Redshift range | Entries | Used for |
|---|---|---|---|
| Low redshift | $0.023 < z < 0.15$ | 496 | $q_0$ (cosmography) and $H_0$ |
| Hubble flow | $z > 0.01$ | 1580 | $\Omega_{m,0}$ (ΛCDM) |

The calibrator supernovae (Cepheid hosts) are excluded in both samples.

## Results

| Model | $q_0$ | $\Omega_{m,0}$ | $H_0$ (km s⁻¹ Mpc⁻¹) |
|---|---|---|---|
| Cosmography | $-0.518^{+0.231}_{-0.235}$ | — | $73.20^{+0.29}_{-0.29}$ |
| Flat ΛCDM | $-0.476^{+0.029}_{-0.028}$ | $0.349^{+0.019}_{-0.019}$ | $73.11^{+0.29}_{-0.29}$ |

Both approaches give $q_0 < 0$, consistent with an accelerating expansion of the Universe. The uncertainties of $H_0$ are conditional to a fixed $q_0$ and do not include the off-diagonal covariances of the catalogue.

## Requirements

- Python 3
- NumPy (≥ 2.0, for `np.trapezoid`)
- pandas
- SciPy
- Matplotlib

```bash
pip install numpy pandas scipy matplotlib
```

## Data

The notebook uses the file `Pantheon+SH0ES.dat` from the Pantheon+SH0ES data release:

https://github.com/PantheonPlusSH0ES/DataRelease

Download the file and place it in the same folder as the notebook.

## Usage

Open `PROYECTO_PANTHEON.ipynb` and run all cells in order. The notebook is organised as follows:

| Cell | Content |
|---|---|
| 1 | Dependencies |
| 2 | Data extraction and sample selection |
| 3 | Marginalised $\chi^2$ for the cosmographic model |
| 4 | Marginalised $\chi^2$ for the ΛCDM model |
| 5 | $\chi^2$ with the SH0ES distance moduli |
| 6 | Minimisation |
| 7 | Uncertainties ($\Delta\chi^2 = 1$) |
| 8 | Sensitivity of $H_0$ to $q_0$ |
| 9 | Luminosity distances |
| 10 | Hubble diagram |
| 11 | $\chi^2$ profiles |

The notebook saves two figures:

- `Hubble_diagram.png`: distance moduli of the Hubble-flow supernovae with the cosmographic and ΛCDM models, and the residuals relative to ΛCDM.
- `chi2_profiles_mnras.png`: marginalised $\Delta\chi^2$ as a function of $q_0$ and $\Omega_{m,0}$.

## References

- Brout D. et al., 2022, ApJ, 938, 110 — The Pantheon+ Analysis: Cosmological Constraints
- Scolnic D. et al., 2022, ApJ, 938, 113 — The Pantheon+ Analysis: The Full Data Set and Light-curve Release
- Riess A. G. et al., 2022, ApJL, 934, L7 — A Comprehensive Measurement of the Local Value of the Hubble Constant (SH0ES)
- Visser M., 2005, Gen. Relativ. Gravit., 37, 1541 — Cosmography: Cosmology without the Einstein equations
- Hogg D. W., 1999, arXiv:astro-ph/9905116 — Distance measures in cosmology
