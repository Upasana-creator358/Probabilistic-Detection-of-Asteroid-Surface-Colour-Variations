```latex
\documentclass[12pt,a4paper]{article}

% --------------------------------------------------
% Packages
% --------------------------------------------------
\usepackage[margin=1in]{geometry}
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{graphicx}
\usepackage{booktabs}
\usepackage{hyperref}
\usepackage{enumitem}
\usepackage{xcolor}
\usepackage{float}
\usepackage{siunitx}

\hypersetup{
    colorlinks=true,
    linkcolor=blue,
    urlcolor=blue,
    citecolor=blue
}

% --------------------------------------------------
% Document
% --------------------------------------------------

\title{
    \textbf{Probabilistic Detection of Asteroid Surface-Colour Variations}
}

\author{
    Research Project
}

\date{\today}

\begin{document}

\maketitle

% --------------------------------------------------
\begin{abstract}

Asteroids are generally observed from Earth as unresolved points of light. 
Although individual surface regions cannot usually be spatially resolved, 
the rotation of an asteroid causes different parts of its surface to face the 
observer at different times. If these regions have different photometric 
properties or colours, the measured colour of the asteroid may vary with 
rotational phase.

This project investigates whether such rotationally repeating colour 
variations can be detected using sparse multiband photometric survey data. 
The initial analysis will use public observations from the Zwicky Transient 
Facility (ZTF), particularly observations obtained in the $g$ and $r$ bands.

A probabilistic framework will be used to account for photometric noise and 
uncertainties in asteroid shape, rotation, and brightness. Monte Carlo 
simulations will be used to determine how often an apparent colour signal 
could arise from a uniformly coloured asteroid. The method will first be 
tested using simulated observations and subsequently applied to a small 
sample of real asteroids.

\end{abstract}

% --------------------------------------------------
\section{Introduction}

Asteroids are small Solar System bodies whose surfaces can contain regions 
with different physical and compositional properties. Variations in 
composition, albedo, texture, or space-weathering state may produce spatial 
variations in their observed colour.

For most asteroids observed from Earth, the asteroid is not spatially 
resolved. The telescope therefore records the asteroid as a point source, 
and information about individual surface regions is lost in the image.

Rotation provides one way of recovering some information about the surface. 
As the asteroid rotates, different parts of the surface contribute to the 
observed brightness. If the surface is heterogeneous, the photometric signal 
may contain variations associated with the rotational phase.

In multiband observations, the corresponding colour may also change as 
different surface regions become visible.

The basic idea investigated in this project is therefore

\begin{equation}
\text{surface heterogeneity}
\rightarrow
\text{rotation}
\rightarrow
\text{changing visible surface}
\rightarrow
\text{photometric variation}.
\end{equation}

The difficulty is that the expected colour variations may be small compared 
with observational uncertainties. In addition, the observations from 
large-scale surveys are usually sparse rather than continuous.

The purpose of this project is to investigate whether these limitations can 
be handled statistically and whether a repeating colour signal can be 
distinguished from random observational variations.

% --------------------------------------------------
\section{Research Question}

The main research question is:

\begin{quote}
Can sparse multiband photometric observations be used to identify 
rotationally repeating colour variations associated with surface 
heterogeneity on unresolved asteroids?
\end{quote}

The analysis will also investigate the following related questions:

\begin{enumerate}
    \item How much colour variation can be detected with sparse ZTF data?
    \item How strongly does photometric noise affect the detection?
    \item How do uncertainties in the asteroid shape and rotation model 
    affect the result?
    \item How frequently can a uniformly coloured asteroid produce an 
    apparent colour signal?
    \item Under what conditions can a possible colour variation be 
    distinguished from noise?
\end{enumerate}

% --------------------------------------------------
\section{Physical Motivation}

Consider an asteroid with a spatially uniform surface. As the asteroid 
rotates, its total brightness may change because its projected cross-section 
and illumination geometry change. However, after accounting for these 
effects, its intrinsic colour should remain approximately constant.

For a heterogeneous asteroid, different surface regions may have different 
reflectance spectra. As these regions rotate into the visible portion of the 
surface, the integrated colour can change.

A simple schematic representation is

\begin{equation}
C(t) = C_0 + \Delta C(\phi(t)) + \epsilon(t),
\end{equation}

where

\begin{itemize}
    \item $C(t)$ is the observed colour at time $t$,
    \item $C_0$ is the mean colour,
    \item $\Delta C(\phi)$ is a possible rotationally dependent colour 
    variation,
    \item $\phi(t)$ is the rotational phase,
    \item $\epsilon(t)$ represents observational and modelling uncertainties.
\end{itemize}

For a uniform surface,

\begin{equation}
\Delta C(\phi) \approx 0,
\end{equation}

whereas a heterogeneous surface may produce

\begin{equation}
\Delta C(\phi) \neq 0.
\end{equation}

The important property is not simply that the colour changes with time. 
A possible surface signal should be related to the asteroid's rotational 
phase and should therefore repeat approximately after one rotation.

% --------------------------------------------------
\section{Multiband Photometry}

The initial analysis will use observations in the ZTF $g$ and $r$ filters.

The measured magnitudes are denoted by

\begin{equation}
m_g
\end{equation}

and

\begin{equation}
m_r.
\end{equation}

A colour index can then be calculated as

\begin{equation}
g-r = m_g - m_r.
\end{equation}

A useful alternative representation is obtained using fluxes. If $F_g$ and 
$F_r$ are the measured fluxes, the corresponding magnitude difference is

\begin{equation}
g-r
=
-2.5\log_{10}
\left(
\frac{F_g}{F_r}
\right)
+
ZP,
\end{equation}

where $ZP$ represents the relevant zero-point term.

The colour measurements will be associated with the rotational phase of the 
asteroid rather than simply plotted against observation time.

% --------------------------------------------------
\section{Rotational Phase}

The rotational phase is required to determine which part of the asteroid's 
rotation corresponds to each observation.

If the rotation period is $P$ and the reference rotational epoch is 
$t_0$, a simplified rotational phase can be written as

\begin{equation}
\phi(t)
=
\left[
\frac{t-t_0}{P}
\right]
\bmod 1.
\end{equation}

Here,

\begin{equation}
0 \leq \phi < 1.
\end{equation}

The actual implementation will use the available asteroid rotational model, 
including the spin state and shape information when required.

The general processing sequence is

\begin{equation}
t
\rightarrow
\text{rotational state}
\rightarrow
\phi
\rightarrow
\text{surface orientation}.
\end{equation}

This allows observations separated by several days or months to be compared 
if they correspond to similar rotational phases.

% --------------------------------------------------
\section{Asteroid Shape and Brightness Model}

The brightness of an asteroid depends on its shape, orientation, 
illumination, and viewing geometry.

A simplified model can be written as

\begin{equation}
F_{\mathrm{model}}
=
F(\mathbf{S},\mathbf{R},\mathbf{G},\mathbf{P}),
\end{equation}

where

\begin{itemize}
    \item $\mathbf{S}$ represents the asteroid shape,
    \item $\mathbf{R}$ represents the rotational state,
    \item $\mathbf{G}$ represents the observing geometry,
    \item $\mathbf{P}$ represents the photometric parameters.
\end{itemize}

For each observation, the model will provide an expected brightness for 
the assumed surface properties.

The residual can then be expressed as

\begin{equation}
\Delta F_i
=
F_{\mathrm{obs},i}
-
F_{\mathrm{model},i}.
\end{equation}

The purpose of this model is not to reproduce every detail of the asteroid's 
brightness perfectly. Instead, it provides a reference against which 
additional colour variations can be investigated.

% --------------------------------------------------
\section{Observation Geometry}

The observed brightness depends not only on the asteroid's rotation but also 
on its position relative to the Sun and observer.

For each observation, quantities such as the following may be required:

\begin{itemize}
    \item Heliocentric distance
    \item Observer distance
    \item Solar phase angle
    \item Observer direction
    \item Solar direction
    \item Rotational orientation
\end{itemize}

The observing geometry will be obtained using asteroid ephemerides and 
appropriate Solar System geometry tools.

JPL Horizons will be used where appropriate for ephemeris calculations.

% --------------------------------------------------
\section{Sparse Survey Data}

Unlike a dedicated observing campaign, a time-domain survey does not 
necessarily observe an asteroid continuously throughout a complete rotation.

The observations may therefore look schematically like

\begin{equation}
t_1,\quad t_2,\quad t_3,\quad \ldots,\quad t_N,
\end{equation}

with irregular time intervals between measurements.

Consequently, the corresponding rotational phases

\begin{equation}
\phi_1,\quad \phi_2,\quad \phi_3,\quad \ldots,\quad \phi_N
\end{equation}

may also be unevenly distributed.

This sparse sampling is one of the main difficulties of the problem.

A detected pattern must therefore be tested against the possibility that the 
apparent periodicity is produced simply by the sampling pattern and noise.

% --------------------------------------------------
\section{Probabilistic Framework}

The main statistical component of the project is the treatment of 
uncertainties.

Instead of assuming that the asteroid's parameters are known exactly, 
uncertain quantities will be allowed to vary within their expected ranges.

Possible sources of uncertainty include:

\begin{itemize}
    \item Photometric measurement uncertainty
    \item Rotation period uncertainty
    \item Spin-axis uncertainty
    \item Shape-model uncertainty
    \item Brightness-model uncertainty
    \item Sparse temporal sampling
\end{itemize}

The general idea is to generate many possible realizations of the 
observations.

For simulation $j$,

\begin{equation}
\Theta_j
=
\{
P_j,\,
\mathbf{S}_j,\,
\mathbf{R}_j,\,
\mathbf{F}_j,\,
\ldots
\},
\end{equation}

where $\Theta_j$ represents one realization of the uncertain parameters.

For each realization, the predicted observations are calculated and the 
corresponding colour behaviour is measured.

After many simulations, the distribution of possible outcomes can be 
examined.

% --------------------------------------------------
\section{Monte Carlo Simulations}

Monte Carlo simulations will be used to investigate whether an apparent 
colour signal is robust to uncertainties.

The basic procedure is:

\begin{enumerate}
    \item Define the nominal asteroid model.
    \item Assign uncertainties to the relevant parameters.
    \item Draw a random realization of these parameters.
    \item Generate or calculate the corresponding observations.
    \item Add observational noise according to the measurement 
    uncertainties.
    \item Calculate the colour signal.
    \item Repeat the procedure many times.
    \item Compare the simulated distribution with the observed data.
\end{enumerate}

Conceptually,

\begin{equation}
\text{uncertain parameters}
\rightarrow
\text{random realization}
\rightarrow
\text{predicted observations}
\rightarrow
\text{colour statistic}.
\end{equation}

Repeating this process produces a probability distribution for the 
statistic being investigated.

% --------------------------------------------------
\section{Uniform-Surface Null Model}

An important part of the analysis is determining whether a signal could be 
produced without any actual surface-colour variation.

A null model will therefore assume that the asteroid has a spatially 
uniform colour.

Under this assumption, simulated observations will include realistic 
effects such as:

\begin{itemize}
    \item Photometric uncertainties
    \item Sparse sampling
    \item Asteroid-model uncertainties
    \item Rotation uncertainties
\end{itemize}

The resulting simulations provide a reference distribution for a 
uniform asteroid.

If the real observations produce a statistic that is common within this 
distribution, the data may not provide strong evidence for a surface-colour 
variation.

If the observed statistic lies in a region rarely produced by the null 
model, the result becomes a candidate for further investigation.

% --------------------------------------------------
\section{Heterogeneous-Surface Simulations}

The method will also be tested using artificial surface heterogeneity.

For example, the surface can be divided into regions with different 
reflectance or colour properties.

A simple model can be represented as

\begin{equation}
C(\phi)
=
C_0
+
A f(\phi),
\end{equation}

where

\begin{itemize}
    \item $C_0$ is the mean colour,
    \item $A$ is the amplitude of the imposed colour variation,
    \item $f(\phi)$ describes its dependence on rotational phase.
\end{itemize}

Different amplitudes and surface configurations can be tested.

This allows the pipeline to be evaluated under controlled conditions before 
being applied to real observations.

% --------------------------------------------------
\section{False Detection Probability}

One of the main questions is how often a uniformly coloured asteroid could 
produce an apparent signal.

If $N$ Monte Carlo realizations are generated and $N_{\mathrm{false}}$ 
produce a statistic at least as extreme as the observed statistic, an 
empirical false-detection fraction can be estimated as

\begin{equation}
\hat{p}_{\mathrm{false}}
=
\frac{N_{\mathrm{false}}}{N}.
\end{equation}

This quantity will be used as one component of evaluating candidate signals.

The interpretation will depend on the exact statistic and null hypothesis 
used in the final implementation.

% --------------------------------------------------
\section{Signal Stability}

A possible colour signal should remain reasonably stable when the uncertain 
parameters are varied.

For example, if a colour variation is detected only for one very specific 
shape model or rotation period, the result may be strongly dependent on 
model assumptions.

Monte Carlo realizations will therefore be used to examine the distribution 
of the inferred signal.

Possible quantities of interest include

\begin{equation}
A_1,A_2,\ldots,A_N,
\end{equation}

where $A_i$ represents the recovered colour amplitude from simulation $i$.

The resulting distribution can be summarized using quantities such as the 
median, standard deviation, or credible intervals where appropriate.

% --------------------------------------------------
\section{Detection Categories}

The analysis will not treat every colour variation as a confirmed detection.

Instead, results will be described according to the statistical evidence 
available.

Possible categories are:

\begin{table}[H]
\centering
\begin{tabular}{p{0.25\textwidth} p{0.62\textwidth}}
\toprule
\textbf{Category} & \textbf{Meaning} \\
\midrule
Candidate signal &
A rotationally repeating colour variation is present and is not commonly 
produced by the adopted uniform-surface simulations. \\

Inconclusive &
A possible variation is present, but the available data or model 
uncertainties do not allow a reliable interpretation. \\

Consistent with uniform surface &
The observed colour behaviour is compatible with the adopted 
uniform-surface model and its uncertainties. \\
\bottomrule
\end{tabular}
\caption{Possible interpretation categories for the analysis.}
\end{table}

These categories describe the outcome of the statistical analysis rather 
than providing a definitive physical classification of the asteroid.

% --------------------------------------------------
\section{Data Sources}

The project will use publicly available astronomical data and asteroid 
models.

\subsection{Zwicky Transient Facility}

The Zwicky Transient Facility (ZTF) provides time-domain optical 
observations over a large fraction of the sky.

The initial analysis will focus on the ZTF $g$ and $r$ bands.

\subsection{Fink}

Fink provides access to processed time-domain astronomical data and can be 
used to identify and retrieve relevant ZTF observations.

\subsection{IRSA ZTF Archive}

The NASA/IPAC Infrared Science Archive (IRSA) provides access to ZTF 
archival data and associated metadata.

\subsection{DAMIT}

The Database of Asteroid Models from Inversion Techniques (DAMIT) provides 
asteroid shape and rotational models derived from light-curve inversion.

These models are important for connecting the observation time with the 
rotational geometry of the asteroid.

\subsection{JPL Horizons}

JPL Horizons will be used to obtain Solar System ephemerides and observing 
geometry where required.

% --------------------------------------------------
\section{Initial Asteroid Selection}

The project will begin with one well-characterized asteroid.

The first asteroid should have:

\begin{itemize}
    \item A reliable rotation period
    \item A suitable shape model
    \item A known rotational state
    \item Sufficient ZTF observations
    \item Observations in both $g$ and $r$ bands
    \item Adequate time coverage over different rotational phases
\end{itemize}

The purpose of starting with a single asteroid is to validate the complete 
analysis pipeline before introducing the additional complications associated 
with a larger sample.

After the first analysis is validated, the sample may be expanded to 
approximately $1$--$30$ asteroids.

% --------------------------------------------------
\section{Validation Strategy}

The project will proceed in several stages.

\subsection{Stage 1: Uniform Simulations}

A simulated asteroid with a uniform surface will be generated.

The objective is to determine the expected behaviour of the detection 
statistic in the absence of real colour heterogeneity.

\subsection{Stage 2: Heterogeneous Simulations}

Surface regions with controlled colour differences will be introduced.

The objective is to determine whether the analysis can recover a known 
signal.

\subsection{Stage 3: Sparse Sampling}

The simulated observations will be sampled in a manner similar to real ZTF 
observations.

This will test how incomplete temporal coverage affects the detection.

\subsection{Stage 4: Real Observations}

The validated pipeline will then be applied to real ZTF observations of the 
selected asteroid.

The overall workflow is

\begin{equation}
\text{uniform simulation}
\rightarrow
\text{heterogeneous simulation}
\rightarrow
\text{sparse sampling test}
\rightarrow
\text{real observations}.
\end{equation}

% --------------------------------------------------
\section{Expected Results}

The project is expected to produce a reproducible analysis pipeline capable 
of processing sparse multiband asteroid observations.

The expected outputs include:

\begin{enumerate}
    \item A Python pipeline for downloading and processing observations.
    \item Calculation of asteroid rotational phases.
    \item A brightness model based on asteroid geometry and shape.
    \item Colour measurements from $g$ and $r$ observations.
    \item Monte Carlo uncertainty simulations.
    \item False-detection tests using uniform-surface simulations.
    \item Signal-recovery tests using heterogeneous-surface simulations.
    \item An initial analysis of one well-characterized real asteroid.
    \item Expansion to a larger asteroid sample if the first analysis is 
    successfully validated.
\end{enumerate}

Possible final results may include candidate colour signals, inconclusive 
cases, and quantitative limits on the colour variation detectable with the 
available data.

% --------------------------------------------------
\section{Limitations}

Several limitations need to be considered.

\subsection{Sparse Sampling}

ZTF observations are not designed specifically for asteroid surface 
mapping. The rotational phases may therefore be unevenly sampled.

\subsection{Photometric Noise}

The expected colour variations may be comparable to or smaller than the 
photometric uncertainties.

\subsection{Asteroid Model Uncertainty}

Shape and rotational models are not exact. Errors in these models can 
propagate into the predicted brightness and rotational phase.

\subsection{Degeneracy Between Shape and Surface Properties}

Brightness variations can arise from the asteroid's shape as well as from 
surface properties. A reliable shape model is therefore important.

\subsection{Small Sample Size}

The initial sample will be small. Results from the first few asteroids 
should therefore not automatically be interpreted as representative of the 
whole asteroid population.

% --------------------------------------------------
\section{Reproducibility}

A major objective of the project is to maintain a reproducible workflow.

The analysis should allow another researcher to follow the sequence

\begin{equation}
\text{raw observations}
\rightarrow
\text{pre-processing}
\rightarrow
\text{geometry}
\rightarrow
\text{rotational phase}
\rightarrow
\text{brightness model}
\rightarrow
\text{colour analysis}
\rightarrow
\text{Monte Carlo analysis}.
\end{equation}

The repository will contain the Python code, configuration information, 
analysis notebooks where appropriate, and generated figures and results.

Large external datasets will not necessarily be stored directly in the 
repository. Instead, scripts should document how the required data can be 
retrieved from their original sources.

% --------------------------------------------------
\section{Planned Repository Structure}

A possible repository structure is:

\begin{verbatim}
.
├── data/
│   ├── raw/
│   ├── processed/
│   └── models/
│
├── simulations/
│   ├── uniform_surface/
│   └── heterogeneous_surface/
│
├── src/
│   ├── data_download.py
│   ├── geometry.py
│   ├── rotation.py
│   ├── photometry.py
│   ├── colour_analysis.py
│   └── monte_carlo.py
│
├── notebooks/
│   └── analysis/
│
├── figures/
├── results/
├── requirements.txt
└── README.md
\end{verbatim}

The structure may change as the implementation develops.

% --------------------------------------------------
\section{Project Status}

The project is currently under development.

\begin{itemize}[label=$\square$]
    \item Review the methodology of Humes and Agarwal (2026)
    \item Select the first well-characterized asteroid
    \item Obtain its shape and rotational model
    \item Obtain ZTF $g$ and $r$ observations
    \item Calculate observing geometry
    \item Calculate rotational phase
    \item Develop the uniform-surface brightness model
    \item Implement colour analysis
    \item Implement Monte Carlo simulations
    \item Validate the method with simulated observations
    \item Analyse the first real asteroid
    \item Expand the sample if the initial analysis is successful
    \item Estimate detection limits and false-detection rates
\end{itemize}

% --------------------------------------------------
\section{Relation to Previous Work}

This project is motivated primarily by the study of Humes and Agarwal 
(2026), which investigates the prospects for detecting surface-colour 
heterogeneity on asteroid surfaces using sparse multiband photometric 
survey data.

The present project focuses on testing the methodology using real public 
survey observations and on quantifying the effects of observational and 
model uncertainties.

The distinction between simulated and real observations is important. 
Simulations can establish whether a method is theoretically capable of 
recovering a signal, while real observations introduce additional effects 
such as irregular sampling, measurement errors, imperfect models, and 
survey-specific systematics.

% --------------------------------------------------
\section{References}

\begin{enumerate}

    \item Humes, C. \& Agarwal, J. (2026).
    \textit{Prospects for detecting surface color heterogeneity on asteroid
    surfaces from sparse multiband photometric survey data}.

    \item Carry, B. et al. (2024).
    Work concerning asteroid physical properties and characterization.

    \item Mahlke, M. et al. (2021).
    Work concerning asteroid photometry and time-domain survey observations.

    \item Zwicky Transient Facility (ZTF).
    \url{https://www.ztf.caltech.edu/}

    \item Fink.
    \url{https://fink-broker.org/}

    \item NASA/IPAC Infrared Science Archive (IRSA).
    \url{https://irsa.ipac.caltech.edu/}

    \item Database of Asteroid Models from Inversion Techniques (DAMIT).
    \url{https://astro.troja.mff.cuni.cz/projects/asteroids3D/web.php}

    \item JPL Horizons.
    \url{https://ssd.jpl.nasa.gov/horizons/}

\end{enumerate}

% --------------------------------------------------
\section{Conclusion}

This project investigates whether rotationally repeating colour variations 
can be extracted from sparse multiband observations of unresolved asteroids.

The main approach is to combine asteroid rotational and shape models with 
public ZTF photometry and a probabilistic treatment of uncertainties.

The analysis will first be validated using simulated uniform and 
heterogeneous asteroids. Only after the method has been tested will it be 
applied to real observations.

The initial goal is not to assume that a measured colour variation represents 
surface heterogeneity, but to determine whether the available observations 
provide sufficient statistical evidence to distinguish such a signal from 
noise, sparse sampling, and uncertainties in the asteroid model.

\end{document}
```
