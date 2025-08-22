---
layout: default
title: Home
---

# CHEEREIO

CHEEREIO is a free, flexible, open-source software tool that can be used to estimate emissions of various pollutants using observations from a variety of platforms, including satellites. CHEEREIO users have published work using the tool to track global methane emissions, monitor carbon monixide from wildfires, and diagnose drivers of methane emissions growth in China.

## What does CHEEREIO do?

Satellites and ground-based monitors can measure pollutants in the air but cannot infer their sources directly. Knowledge of emissions comes instead from bottom-up inventories. Inventories are maps of pollutant sources along with their expected emissions magnitudes constructed from information including infrastructure plans, ship tracks, and economic reports. **Inventories thus link pollution to processes, and processes can be made targets of mitigation efforts.** However, inventory construction takes several years and is subject to error. Bayesian optimization can fuse observational data with the actionable information of inventories. 

CHEEREIO uses the localized ensemble transform Kalman filter (LETKF) to calculate a corrected emissions inventory, accounting for uncertainties both in the original emissions calculations and in observational data. CHEEREIO uses an ensemble of chemical transport model (CTM) simulations of the atmosphere, each driven by randomly perturbed emissions such that the ensemble of CTMs represents the spread of atmospheric states that could result given emissions uncertainty. CHEEREIO compares this suite of artificial atmospheres to observations and uses the difference to update prior emissions. Because CHEEREIO uses CTMs directly, it accounts for nonlinear chemistry and transport. It can ingest observations of many species simultaneously, exploiting empirical correlations. CHEEREIO works with a large library of species and observational instruments already and can be extended to include more.

## Why use CHEEREIO?

CHEEREIO is a tool for chemical data assimilation characterized by its flexibility. It can assimilate any kind of observation (satellite, surface, or aircraft) for any species in any configuration of GEOS-Chem, applying updates to both emissions scaling factors and chemical concentrations. CHEEREIO allows for wide flexibility in what can be assimilated, and for example allows for the user to (1) update observations at multiple time points in the assimilation window (e.g. hourly data updates for a daily window), and (2) assimilate observations of derived quantities such as PM2.5 or AOD. Many different kinds of observations can be used at once to update a family of species. For example, one might want to use NO2 satellite and surface data, SO2 satellite and surface data, NH3 satellite data, AOD, and surface PM2.5 to update emissions and concentrations of NOx, SO2, and NH3 . Whether applying this sort of update in a small **nested region** or for a **global simulation**, CHEEREIO can be configured from **a single JSON settings file to support just about any kind of chemical data assimilation problem: whether it’s multi-species, multi-platform, linear or non-linear.**

Users can easily extend to CHEEREIO to support new observational platforms without modifying CHEEREIO or GEOS-Chem source code. Instead, all users need to do is write a new class inheriting from the ``Observation_Operators`` template supplied with CHEEREIO. CHEEREIO allows users to go from idea to a working data assimilation demo in days, rather than months (or years).