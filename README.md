# TOTEMS - Tidal Orbital decay Timing Extrapolation &amp; Modelling Software

This code originally evolved from the code I wrote as my primary contribution to my third year Astrophysics group project at University College London, titled "Planet-star interaction in Ultra-Short Period Hot Jupiters with Transit Timing Variations". This code analyses Exoplanet mid-transit times for signs of orbital decay, a sign of tidal interaction. Orbital period variations are generally expected to be very small, but in the case of ultra-short period planets they can reach hundreds of ms to a few seconds which over a number of years (now that sufficient archive data exists) can amount to “easily observable” time intervals. It also attempts to ascertain between these, or the sometimes similar effects of apsidal precession upon transits. The Levenberg-Marquadt algorithm, as part of ScipPy's `curve_fit`, is used to fit three models to data:

* Normal, circularised, stable orbit: ![equation](https://latex.codecogs.com/gif.latex?T_%7Bmid%7D%3DT_%7B0%7D&plus;P%5Ctimes%7BE%7D)
* Tidal orbital decay: ![equation](https://latex.codecogs.com/gif.latex?T_%7Bmid%7D%3DT_%7B0%7D&plus;PE&plus;%5Cfrac%7B1%7D%7B2%7DP%5Cfrac%7BdP%7D%7Bdt%7DE%5E2)
* Apsidal precession: ![equation](https://latex.codecogs.com/gif.latex?T_%7Bmid%7D%3DT_%7B0%7D&plus;P_%7BS%7DE-%5Cfrac%7BeP_%7Ba%7D%7D%7B%5Cpi%7D%5Ccos%28%7B%5Comega%28E%29%7D%29), where ![equation](https://latex.codecogs.com/gif.latex?%5Comega%28E%29%20%3D%20%5Comega_0%20&plus;%20%5Cfrac%7Bd%5Comega%7D%7BdE%7DE) and ![equation](https://latex.codecogs.com/gif.latex?P_a%20%3D%20P_s%5Cleft%281-%5Cfrac%7Bd%5Comega/dE%7D%7B2%5Cpi%7D%5Cright%29%5E%7B-1%7D)

(Equations from, and further explanation given in [Kishore C. Patra *et al* 2017 AJ 154 4](https://doi.org/10.3847/1538-3881/aa6d75) and [Kishore C. Patra et al 2020 AJ 159 150](https://arxiv.org/abs/2002.02606)).

These models can be extrapolated forward to predict what may happen in the future, and later compare additional transits to see how these change the models. Chi-squared analysis can be carried out on each model to judge the quality of the fit. The Akaike and Bayesian Information Criterion can be calculated for each model, to enable the judging of which model is the most suitable of the three.

In this notebook, I provide an example of doing this with WASP-12b. The ability to load in transit mid-times from the [Exoplanet Transit Database](http://var2.astro.cz/ETD/), or from a user's own CSV file, with automatic conversion between HJD and BJD, is included. Thanks to Dr Angelos Tsiaras for the [PyLightcurve](https://github.com/ucl-exoplanets/pylightcurve) package to enable conversion. Planetary parameters can also be obtained from the [Open Exoplanet Catalogue](https://github.com/OpenExoplanetCatalogue/open_exoplanet_catalogue). Future plans are to write this as standalone Python code, to be incorporated into a PyPI package. A long-term goal is to enable MCMC to replace `curve_fit`, probably using the emcee package.

---

Example plot generated with the notebook, showing extrapolation of fitted models from past literature data, plus the addition of a later transit (taken by the author's group as part of the university project this code was originally written for):

![alt text](https://ross-dobson.github.io/images/TOTEMS_wasp12_example_plot.png)
