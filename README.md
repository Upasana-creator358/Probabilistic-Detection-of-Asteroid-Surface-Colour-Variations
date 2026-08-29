Probabilistic Detection of Asteroid Surface-Colour Variations

Project idea

Asteroids appear as points of light. However, as an asteroid rotates, different sides face Earth. If one side contains different material, its measured colour may change repeatedly.

This project will test whether these changes can be found in real telescope observations.

What I will do

Select asteroids with known shapes and rotation periods.

Download public ZTF observations from green (g) and red (r) filters.

Calculate which side faced Earth during each observation.

Predict the brightness expected from a uniformly coloured surface.

Search for colour changes that repeat at the same rotational position.

Test whether noise or uncertain asteroid properties could create the pattern.

Where probability is used

Monte Carlo simulations will vary uncertain brightness, rotation and shape values to estimate:

whether a possible colour signal is stable;

how often a uniform asteroid produces a false detection;

whether each result is strong, inconclusive or consistent with a uniform surface.

What is new

Humes and Agarwal (2026) tested this method mainly with simulated observations. This project will investigate whether it works reliably with real public ZTF data.

Expected output

A reproducible Python pipeline.

Validation with simulated asteroids.

Results for an initial sample of 1-30 real asteroids.

A ranked list of candidates or reliable detection limits.

Data

ZTF/Fink

IRSA ZTF Archive

DAMIT asteroid models

JPL Horizons

Main papers

Humes & Agarwal (2026)

Carry et al. (2024)

Mahlke et al. (2021)

The project will begin with one well-characterized asteroid and expand only after the first analysis is successfully validated.
