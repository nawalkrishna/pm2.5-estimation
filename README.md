# Initial Project Contribution: Multi-Source PM2.5 Data Pipeline

## Overview

This notebook is the initial implementation contribution for the project
**Satellite-Based Ground-Level PM2.5 Estimation Using Multi-Source
Data**.

The purpose of this first contribution is to establish and test a small
end-to-end workflow for collecting, processing, and combining
ground-based PM2.5 observations with satellite-derived aerosol data and
meteorological data.

This is a preliminary proof of concept using a short sample from
**Delhi, India**. It is intended to demonstrate that the main data
sources can be accessed and brought into a common workflow before
expanding the implementation to a larger study region and time period.

## Data Sources

  -----------------------------------------------------------------------
  Data source             Data used               Purpose
  ----------------------- ----------------------- -----------------------
  OpenAQ                  Ground-level PM2.5      Provides the target
                          observations            air-quality
                                                  measurements

  ERA5                    2 m temperature, 2 m    Provides meteorological
                          dew-point temperature,  information
                          10 m u-component wind   
                          and 10 m v-component    
                          wind                    

  MODIS MCD19A2           Aerosol Optical Depth   Provides
                          (AOD) at 0.55 µm        satellite-derived
                          (`Optical_Depth_055`)   aerosol information
  -----------------------------------------------------------------------

## Work Completed

### 1. Environment and project setup

-   Set up the notebook environment and imported the required Python
    libraries.
-   Mounted Google Drive and created folders for raw data, processed
    data, and results.

### 2. Ground-level PM2.5 data collection

-   Accessed the OpenAQ API using an API key.
-   Retrieved a short sample of hourly PM2.5 observations for a Delhi
    monitoring station.
-   Converted timestamps to Indian Standard Time (IST).
-   Resampled the observations to an hourly time series and checked for
    missing values.

### 3. Meteorological data collection

-   Configured the Copernicus Climate Data Store API.
-   Downloaded a short ERA5 sample for the Delhi region.
-   Extracted temperature, dew-point temperature, and wind components.
-   Identified the ERA5 grid point nearest to the selected monitoring
    station.

### 4. Satellite AOD data collection

-   Retrieved MODIS MCD19A2 data for the relevant MODIS tile covering
    Delhi.
-   Extracted the `Optical_Depth_055` variable.
-   Applied the product scale factor and inspected valid and missing AOD
    values at the station location and its nearby pixels.

### 5. Initial data integration

-   Demonstrated how ground PM2.5, satellite AOD, and ERA5
    meteorological variables can be brought together.
-   Created a small sample containing the available observations from
    the selected period.

### 6. CNN-LSTM model implementation

-   Built a small CNN-LSTM model to test the model-building and training
    workflow.
-   Ran a short training and prediction demonstration using the very
    small integrated sample.

## Important Limitations

This notebook is an **initial technical proof of concept**, not a
completed scientific model or a full reproduction of the reference
paper.

-   The demonstration covers only a short period and one monitoring
    location in Delhi.
-   Satellite AOD is missing on several sampled days because valid
    retrievals were not available. These missing values have not been
    artificially filled.
-   The meteorological values used in the small model demonstration were
    reused across the daily sample; they are not a fully time-aligned
    meteorological time series for each day.
-   The CNN-LSTM was trained on an extremely small sample. Its
    prediction and error values must not be interpreted as evidence of
    model accuracy or generalisation.
-   The current implementation does not yet perform full spatial-grid
    construction, robust missing-data handling, chronological
    train/validation/test evaluation, or regional PM2.5 mapping.

## Next Steps

1.  Finalise the study region and the satellite variables to be used in
    the main project.
2.  Collect a longer and more consistent time series of ground PM2.5,
    satellite, and meteorological data.
3.  Develop a systematic spatial and temporal alignment procedure.
4.  Investigate and implement an appropriate strategy for missing
    satellite observations.
5.  Prepare chronological training, validation, and test datasets.
6.  Establish baseline models such as Linear Regression, Random Forest,
    and XGBoost.
7.  Develop and evaluate the proposed deep-learning model using suitable
    metrics such as MAE, RMSE, and R².
8.  Extend the workflow towards spatial estimation and PM2.5 mapping at
    locations without ground monitoring stations.

## Repository Contents

The initial contribution is expected to include:

-   `Shaban_Reproduction_Clean.ipynb` --- notebook containing the
    initial data collection, preprocessing, integration, and model
    demonstration.
-   `README.md` --- description of the notebook, data sources, completed
    work, limitations, and planned next steps.

## Notes

-   API credentials and access tokens should be entered securely at
    runtime and must not be committed to the repository.
-   Large raw datasets and generated files should generally be kept out
    of Git. Consider using `.gitignore` and documenting how to retrieve
    the data.
-   Before sharing the notebook, clear any outputs that may expose
    credentials or unnecessary personal information, and verify that it
    runs from top to bottom in the intended environment.
