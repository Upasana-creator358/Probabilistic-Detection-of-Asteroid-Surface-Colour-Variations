# Probabilistic Detection of Asteroid Surface-Colour Variations

## Project Overview

Asteroids are observed from Earth as points of light. As an asteroid rotates, different regions of its surface face the observer. If these regions have different colours or compositions, the measured colour may vary with rotational phase.

This project investigates whether these variations can be detected using **sparse multiband photometric observations** from the **Zwicky Transient Facility (ZTF)**.

The project is based on the approach discussed by **Humes & Agarwal (2026)**, with an emphasis on testing the method using real survey data.

---

## Method

The analysis will:

1. Select an asteroid with a known shape and rotation period.
2. Obtain public ZTF observations in the `g` and `r` filters.
3. Calculate the rotational phase of each observation.
4. Model the expected brightness of a uniformly coloured surface.
5. Calculate the observed colour:

$$
g-r = m_g-m_r
$$

6. Search for colour variations that repeat at the same rotational phase.
7. Use Monte Carlo simulations to account for uncertainties in photometry, shape, rotation, and brightness.

The simulations will also test how often a **uniformly coloured asteroid** can produce a false colour signal.

---

## Validation

The pipeline will first be tested using simulated observations:

```text
Uniform surface
      ↓
False-detection test
      ↓
Heterogeneous surface
      ↓
Signal-recovery test
      ↓
Real ZTF observations
```

The initial study will focus on **one well-characterized asteroid**. If the method is successfully validated, the analysis will be extended to a larger sample of approximately **1--30 asteroids**.

---

## Data

* **ZTF / Fink** — multiband photometric observations
* **IRSA ZTF Archive** — ZTF archival data
* **DAMIT** — asteroid shape and rotation models
* **JPL Horizons** — ephemerides and observing geometry

---

## Expected Output

* Reproducible Python analysis pipeline
* Simulation-based validation
* Monte Carlo uncertainty analysis
* Initial results for real asteroid observations
* Candidate colour variations and detection limits

---

## References

* Humes & Agarwal (2026), *Prospects for detecting surface color heterogeneity on asteroid surfaces from sparse multiband photometric survey data*
* Carry et al. (2024)
* Mahlke et al. (2021)
