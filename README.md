# Solar Measurement QC

A Python pipeline for quality-controlling solar irradiance measurements from ground-based monitoring stations.

## Overview

This project processes time-series solar radiation data (GHI, DHI, DNI, and related meteorological variables) stored in NetCDF format, applying automated quality control checks against physical and statistical limits. It compares measured irradiance against clear-sky and extraterrestrial radiation models to flag suspect or invalid data points.

## Features

- Reads and parses multi-station NetCDF solar measurement archives (`xarray`)
- Extracts irradiance channels (GHI, DHI, DNI) and associated QC flags/tests
- Computes solar position and extraterrestrial/clear-sky radiation using `pvlib`
- Applies configurable QC limits and flagging logic per station
- Visualizes daily/annual irradiance patterns as heatmaps and time-series plots

## Data

Input data consists of 1-minute resolution measurements from multiple stations, including:
- Global Tilted/Horizontal Irradiance (GTI/GHI)
- Direct Normal Irradiance (DNI)
- Diffuse Horizontal Irradiance (DHI)
- Relative humidity, temperature, and solar zenith angle
- Per-variable QC flags and test codes

## Tech stack

`xarray` · `pvlib` · `pandas` · `numpy` · `matplotlib`
