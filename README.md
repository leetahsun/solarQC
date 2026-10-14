# Solar Measurement QC

A Python pipeline for quality-controlling ground-based solar irradiance measurements using physical limits, solar geometry, clear-sky modelling, and irradiance consistency checks.

## Overview

This project processes 1-minute time-series solar radiation data stored in NetCDF format from multiple monitoring stations.

The workflow evaluates **Global Horizontal Irradiance (GHI)**, **Diffuse Horizontal Irradiance (DHI)**, and **Direct Normal Irradiance (DNI)** using a combination of physically based and statistical quality-control tests.

Measured irradiance is compared against solar geometry, extraterrestrial radiation, clear-sky estimates, and relationships between irradiance components to identify suspect or inconsistent observations.

## Quality-Control Methods

The pipeline includes:

- **Physically Possible Limits (PPL)** for GHI, DHI, and DNI
- **Extremely Rare Limits (ERL)** for identifying unusual irradiance measurements
- **Three-component closure testing** using the relationship between GHI, DHI, DNI, and solar zenith angle
- **Two-component consistency checks** between irradiance measurements
- **K-value tests** for clearness, direct-beam transmittance, and diffuse-fraction consistency
- **Clear-sky comparison** using `pvlib`
- **Cloud-enhancement analysis** to distinguish unusual atmospheric events from possible measurement errors
- **Solar azimuth/elevation analysis** for identifying possible recurring shading effects
- **Combined QC flags and bitmask encoding** to preserve the reason for each flagged observation

## Features

- Reads and processes multi-station NetCDF measurement archives using `xarray`
- Extracts irradiance and meteorological variables
- Checks timestamp continuity and missing-data patterns
- Computes solar position and extraterrestrial irradiance using `pvlib`
- Generates clear-sky irradiance estimates
- Applies multiple independent QC tests
- Combines QC results into machine-readable quality flags
- Compares QC behaviour between measurement stations
- Visualizes daily and annual irradiance patterns using heatmaps and time-series plots

## Data

The input datasets contain 1-minute resolution measurements including:

- Global Horizontal Irradiance (GHI)
- Direct Normal Irradiance (DNI)
- Diffuse Horizontal Irradiance (DHI)
- Temperature
- Relative humidity
- Solar zenith and azimuth angles
- Station and sensor metadata

The current analysis compares measurements from two ground-based monitoring stations over approximately one year.

## Example Physical Consistency Check

The three irradiance components should approximately satisfy:

```text
GHI ≈ DHI + DNI × cos(SZA)
```

where `SZA` is the solar zenith angle.

Large deviations from this relationship can indicate measurement inconsistencies or sensor-related issues.

## QC Output

Each quality-control test produces an independent flag.

These flags are combined using a **bitmask**, allowing a single observation to retain information about multiple simultaneous QC failures.

This makes it possible to identify both:

- whether a measurement is suspicious
- why it was flagged

## Tech Stack

`Python` · `xarray` · `pvlib` · `pandas` · `NumPy` · `matplotlib` · `netCDF4`

`main.ipynb`

The notebook covers data inspection, solar-position calculations, QC testing, clear-sky analysis, flag aggregation, and comparison between monitoring stations.
