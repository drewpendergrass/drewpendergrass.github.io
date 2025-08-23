---
layout: default
title: Home
---

# CHEEREIO

CHEEREIO is a free, flexible, open-source software tool that can be used to **estimate emissions of various pollutants** using observations from a variety of platforms, including satellites and surface monitors. 

CHEEREIO users have published work using the tool to track **global methane emissions**, monitor **carbon monixide from wildfires**, and diagnose drivers of **methane emissions growth in China**.

## Code and documentation

CHEEREIO code is freely available from our [Github](https://https://github.com/drewpendergrass/CHEEREIO) repository. 

A high-level overview and demo of the software is given in our [model description paper](https://doi.org/10.5194/gmd-16-4793-2023). 

An *extensive* manual for CHEEREIO is provided in our [online documentation](https://cheereio.readthedocs.io). 

To get started with CHEEEREIO, you can read my [slides](http://drewpendergrass.com/2024_06_10_pendergrass_cheereio_IGC_clinic.pptx) from the 2024 International GEOS-Chem Meeting Clinic.

For support, please open a [Github issue](https://github.com/drewpendergrass/CHEEREIO/issues) so that all users can see the solution. You can also email the lead developer, Drew Pendergrass, at andrew.pendergrass [at] duke [dot] edu. Feel free also to inquire about whether CHEEREIO is a good fit for your project.


## What does CHEEREIO do?

Satellites and ground-based monitors can measure pollutants in the air but cannot infer their sources directly. Knowledge of emissions comes instead from bottom-up inventories. Inventories are maps of pollutant sources along with their expected emissions magnitudes constructed from information including infrastructure plans, ship tracks, and economic reports. **Inventories thus link pollution to processes, and processes can be made targets of mitigation efforts.** However, inventory construction takes several years and is subject to error. Bayesian optimization can fuse observational data with the actionable information of inventories. 

CHEEREIO uses the localized ensemble transform Kalman filter (LETKF) to calculate a corrected emissions inventory, accounting for uncertainties both in the original emissions calculations and in observational data. CHEEREIO uses an ensemble of chemical transport model (CTM) simulations of the atmosphere, each driven by randomly perturbed emissions such that the ensemble of CTMs represents the spread of atmospheric states that could result given emissions uncertainty. CHEEREIO compares this suite of artificial atmospheres to observations and uses the difference to update prior emissions. Because CHEEREIO uses CTMs directly, it accounts for nonlinear chemistry and transport. It can ingest observations of many species simultaneously, exploiting empirical correlations. CHEEREIO works with a large library of species and observational instruments already and can be extended to include more.

![Demonstration of the CHEEREIO workflow](/assets/cheereio_concept.png)

## Why use CHEEREIO?

CHEEREIO is a tool for chemical data assimilation characterized by its flexibility. It can assimilate any kind of observation (satellite, surface, or aircraft) for any species in any configuration of GEOS-Chem, applying updates to both emissions scaling factors and chemical concentrations. CHEEREIO allows for wide flexibility in what can be assimilated, and for example allows for the user to (1) update observations at multiple time points in the assimilation window (e.g. hourly data updates for a daily window), and (2) assimilate observations of derived quantities such as PM<sub>2.5</sub> or AOD. Many different kinds of observations can be used at once to update a family of species. For example, one might want to use NO<sub>2</sub> satellite and surface data, SO<sub>2</sub> satellite and surface data, NH3 satellite data, AOD, and surface PM<sub>2.5</sub> to update emissions and concentrations of NO<sub>x</sub>, SO<sub>2</sub>, and NH<sub>3</sub>. Whether applying this sort of update in a small **nested region** or for a **global simulation**, CHEEREIO can be configured from **a single JSON settings file to support just about any kind of chemical data assimilation problem: whether it’s multi-species, multi-platform, linear or non-linear.**

Users can easily extend to CHEEREIO to support new observational platforms without modifying CHEEREIO or GEOS-Chem source code. Instead, all users need to do is write a new class inheriting from the ``Observation_Operators`` template supplied with CHEEREIO. CHEEREIO allows users to go from idea to a working data assimilation demo in days, rather than months (or years).

Because CHEEREIO involves running an ensemble of GEOS-Chem simulations, it can only be run on a computational cluster. Hardware requirements are substantial but not prohibitive. For my [global methane inversion](https://doi.org/10.5194/egusphere-2025-1554), I used 48 cores. 

![Infographic on creating a CHEEREIO simulation](/assets/customization-1536x690.png)

## Citations

All CHEEREIO users should cite the original CHEEREIO paper in any publication:

Pendergrass, D. C., Jacob, D. J., Nesser, H., Varon, D. J., Sulprizio, M., Miyazaki, K., & Bowman, K. W. (2023). CHEEREIO 1.0: A versatile and user-friendly ensemble-based chemical data assimilation and emissions inversion platform for the GEOS-Chem chemical transport model. Geoscientific Model Development, 16(16), 4793–4810. https://doi.org/10.5194/gmd-16-4793-2023

All CHEEREIO users should also cite the original LETKF paper in any publication (and read before using):

Hunt, B. R., Kostelich, E. J., & Szunyogh, I. (2007). Efficient data assimilation for spatiotemporal chaos: A local ensemble transform Kalman filter. Physica D: Nonlinear Phenomena, 230(1), 112–126. https://doi.org/10.1016/j.physd.2006.11.008

CHEEREIO users that use TCCON or TROPOMI CO (version 1.4+) should cite the following paper:

Voshtani, S., Jones, D. B. A., Wunch, D., Pendergrass, D. C., Wennberg, P. O., Pollard, D. F., Morino, I., Ohyama, H., Deutscher, N. M., Hase, F., Sussmann, R., Weidmann, D., Kivi, R., García, O., Té, Y., Chen, J., Anderson, K., Stevens, R., Kondragunta, S., … Murata, I. (2025). Quantifying CO emissions from boreal wildfires by assimilating TROPOMI and TCCON observations. EGUsphere, 1–60. https://doi.org/10.5194/egusphere-2025-858

CHEEREIO users that use TROPOMI CH4, lognormal errors, or ObsPack should cite the following paper:

Pendergrass, D. C., Jacob, D. J., Balasus, N., Estrada, L., Varon, D. J., East, J. D., He, M., Mooring, T. A., Penn, E., Nesser, H., & Worden, J. R. (2025). Trends and seasonality of 2019&ndash;2023 global methane emissions inferred from a localized ensemble transform Kalman filter (CHEEREIO v1.3.1) applied to TROPOMI satellite observations. EGUsphere, 1–26. https://doi.org/10.5194/egusphere-2025-1554

### Other papers using CHEEREIO

Li, Y, D. C. Pendergrass, D. J. Jacob, Y. Tang, J. Qiu, and B. Zheng. Drivers of methane emissions regrowth in China after 2019. *In prep*

## Support

CHEEREIO has been supported in the past by the NASA Carbon Monitoring System (grant no. 80NSSC21K1057) and an NSF Graduate Research Fellowship Program (GRFP) grant to Drew Pendergrass. This material is based upon work supported by the National Science Foundation under Award No. 2516898.

Any opinions, findings, and conclusions or recommendations expressed in this material are those of the author(s) and do not necessarily reflect the views of the National Science Foundation.
