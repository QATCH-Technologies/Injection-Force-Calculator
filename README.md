# Viscosity & Injection Force Calculator

**QATCH Technologies** - [qatchtech.com](https://qatchtech.com)

A browser-based screening tool for predicting plunger injection force for prefilled syringes and staked needles. It fits a viscosity-shear-rate profile to the Carreau-Yasuda model and estimates force using a hydrodynamic framework.

---

## Overview

Predicting injection force is critical during the development of concentrated protein formulations, which often exhibit non-Newtonian, shear-thinning behavior. This tool uses a hydrodynamic approach to estimate the force required to inject a formulation through a needle, accounting for the effective shear rate inside the needle and the non-ideal geometry of the syringe. This provides a fast, in-browser estimate to support early-stage formulation screening and device selection.

> **This tool is an approximate educational / early-screening implementation**, not the original published models. Results must be validated experimentally before use in research, development, manufacturing, or regulatory decisions.

**Primary Reference:**
Allmendinger A., Fischer S., Huwyler J., et al. *Rheological characterization and injection forces of concentrated protein formulations: An alternative predictive model for non-Newtonian solutions.* Eur. J. Pharm. Biopharm. (2014).
[doi:10.1016/j.ejpb.2014.01.009](https://doi.org/10.1016/j.ejpb.2014.01.009)

---

## Features

* **Two-step workflow:** First, fit a viscosity profile; second, input syringe geometry and injection rate to estimate the force.
* **Multiple Viscosity Input Modes:**
* *Newtonian:* A single constant viscosity ($n = 1$).
* *Custom Fit:* Fits $\ge 4$ shear-rate/viscosity measurements to the Carreau-Yasuda model via manual entry or CSV upload.


* **Uncertainty bands:** Generates an ensemble of plausible fits to provide confidence bands that widen naturally in unmeasured (e.g., high-shear) regions.
* **Flexible injection rate specification:** Define the injection by total time, volumetric flow rate, or plunger velocity.
* **Empirical corrections:** Includes inputs for stopper/barrel sliding friction and an optional shape/needle-tip factor ($\phi$).
* **Fully client-side:** No server, no data upload, runs entirely in the browser.
* **About / Disclaimer drawer:** Accessible from the navbar; includes model explanation, geometry diagrams, disclaimer, and contact form.

---

## Files

```text
injection_force_calculator.html   Main application
injection_force_styles.css        External stylesheet
carreau_yasuda.js                 Algorithm for curve fitting and ensemble generation
injection_force.js                Force calculation logic and UI state management
icons/                            SVG/PNG icon assets
README.md                         This file

```

---

## Model Description

### What the model estimates

* The four parameters of the Carreau-Yasuda model: zero-shear viscosity ($\eta_0$), infinite-shear viscosity ($\eta_\infty$), power-law index ($n$), and critical shear rate ($\gamma_c$).
* The effective shear rate inside the needle during injection.
* The hydrodynamic force component and total predicted injection force.

### How force is estimated

The model relies on a simplified hydrodynamic framework:

1. **Effective Shear Rate:** Calculates the effective shear rate in the needle using the non-Newtonian flow index ($n$):

$$\gamma_{eff} = \left(\frac{2Q}{\pi R_n^3}\right) \cdot \left(\frac{3n+1}{2n+1}\right)$$


2. **Dynamic Viscosity:** Reads the viscosity at $\gamma_{eff}$ from the fitted Carreau-Yasuda profile (along with its uncertainty band).
3. **Hydrodynamic Force:** Applies the Hagen-Poiseuille equation adapted for syringe geometry:

$$F_{hydro} = \frac{8 \eta L Q R_b^2}{R_n^4}$$


4. **Total Force:** Adds the stopper/barrel sliding friction offset to the hydrodynamic force.

### Empirical correction $\phi$

Real prefilled syringes (PFS) and staked needles are not ideal flow channels. An optional shape / needle-tip factor ($\phi$) scales the hydrodynamic term to improve agreement with measured forces (e.g., using $\phi \approx 0.75$).

**Reference for $\phi$ factor:**
Wu et al. *Injection force modeling for prefilled syringes.* Eur. J. Pharm. Biopharm. (2024).
[doi:10.1016/j.ejpb.2024.114221](https://doi.org/10.1016/j.ejpb.2024.114221)

---

## Disclaimer

This software is provided **"as is"** without warranty of accuracy, fitness for a particular purpose, or regulatory suitability. Users are solely responsible for validating results experimentally before use in research, development, manufacturing, or process decisions. Comfort thresholds on the force scale are heuristic screening guides only and do not constitute regulatory, clinical, or engineering advice.

---

## Contact

Questions, feedback, or interest in QATCH's viscosity and injectability measurement solutions:

**Email:** [info@qatchtech.com]()
**Website:** [qatchtech.com](https://qatchtech.com)