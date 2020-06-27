# TOTEMS - Tidal Orbital decay Timing Extrapolation &amp; Modelling Software

This code originally evolved from the code I wrote as my primary contribution to my third year Astrophysics group project at University College London, titled "Planet-star interaction in Ultra-Short Period Hot Jupiters with Transit Timing Variations". It reads in a series of archive mid-transit times (converting to Barycentric Julian Date) for an exoplanet, suspected of undergoing tidal orbital decay (apsidal precession also can look similar). The user's mid-transit-time from their own observations can also be added. It ensure it is all using the same epoch system, and utilises user-provided starting values with SciPy's `curve_fit` function (specifically the Levenberg-Marquardt algorithm) to try match the exoplanet transit to one of three options:

* Normal, circularised, stable orbit: ![equation](https://latex.codecogs.com/gif.latex?T_%7Bmid%7D%3DT_%7B0%7D&plus;P%5Ctimes%7BE%7D)
* Tidal orbital decay: ![equation](https://latex.codecogs.com/gif.latex?T_%7Bmid%7D%3DT_%7B0%7D&plus;PE&plus;%5Cfrac%7B1%7D%7B2%7DP%5Cfrac%7BdP%7D%7Bdt%7DE%5E2)
* Apsidal precession: ![equation](https://latex.codecogs.com/gif.latex?T_%7Bmid%7D%3DT_%7B0%7D&plus;P_%7BS%7DE-%5Cfrac%7BeP_%7Ba%7D%7D%7B%5Cpi%7D%5Ccos%28%7B%5Comega%28E%29%7D%29), where ![equation](https://latex.codecogs.com/gif.latex?%5Comega%28E%29%20%3D%20%5Comega_0%20&plus;%20%5Cfrac%7Bd%5Comega%7D%7BdE%7DE) and ![equation](https://latex.codecogs.com/gif.latex?P_a%20%3D%20P_s%5Cleft%281-%5Cfrac%7Bd%5Comega/dE%7D%7B2%5Cpi%7D%5Cright%29%5E%7B-1%7D)

(Equations from, and further explanation given in [Patra et al. 2017](https://arxiv.org/abs/2002.02606)).

Chi-squared analysis is carried out on each fit to ascertain which is best. If the user provided their own mid-time, this is also carried out with and without their datapoint, in order to ascertain the difference it makes.

In the future, this is planned to be a fully-fledged program with a GUI, leaning towards PyQT over Tkinter, but further research is needed. A long-term goal is to enable MCMC to replace `curve_fit`, probably using the emcee package. For now though, it's a Jupyter Notebook.
