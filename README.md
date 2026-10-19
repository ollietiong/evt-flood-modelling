# Flood Frequency Analysis Using Extreme Value Theory

### Overview

This project investigates extreme river flows using Extreme Value Theory (EVT) and the Generalised Extreme Value (GEV) distribution. Using historical river flow data from the National River Flow Archive (NRFA), it explores how statistical models can be used to characterise flood extremes and estimate the magnitude of rare high-flow events.

The analysis focuses on the River Tummel at Pitlochry, Scotland, using gauged daily flow measurements from 1973 to 2024.

The project demonstrates a statistical workflow for flood frequency analysis, from data acquisition and exploratory analysis through to block maxima modelling and extreme quantile estimation.

### Objectives

Retrieve and validate historical river flow data using the NRFA API.

Explore the distribution of daily river flows and identify its tail characteristics.

Extract annual maximum flows using the block maxima approach.

Investigate temporal trends and assess the stationarity assumption.

Fit a Generalised Extreme Value (GEV) distribution to annual maxima.

Compare GEV and Gumbel distribution fits.

Estimate the magnitude of extreme flows associated with different return periods.

### Data

The analysis uses gauged daily flow data from the National River Flow Archive.

Monitoring station: Tummel at Pitlochry

Station ID: 15012

Data type: Gauged Daily Flow (GDF)

Period analysed: 1973–2024

Observations: 18,901 daily flow measurements

Daily flows are measured in cubic metres per second (m³/s).

Data is retrieved programmatically through the NRFA API using Python's urllib and json libraries.

### Methodology

1. Data acquisition and validation

The notebook retrieves daily flow measurements from the NRFA API and converts the response into a Pandas DataFrame.

Data quality checks verify:

Missing dates and values.

Duplicate dates.

Chronological ordering.

Continuity of the daily record.

2. Exploratory data analysis

Time-series plots and histograms are used to investigate the distribution and temporal behaviour of daily river flows.

Summary statistics include the mean, median, standard deviation, skewness and 99th percentile.

The daily flow distribution is strongly right-skewed, highlighting the influence of relatively infrequent high-flow events and motivating the use of extreme value methods.

3. Annual block maxima

The block maxima approach is used to extract the largest daily flow in each calendar year.

This produces 52 annual maximum observations for the period 1973–2024. Annual maxima provide a way to focus the analysis on extreme flows rather than the bulk of the daily flow distribution.

4. Stationarity assessment

The notebook investigates whether annual maximum flows exhibit temporal trends using:

A rolling mean of annual maxima.

A scatter plot of the five largest daily flows in each year.

The Augmented Dickey–Fuller (ADF) test.

These analyses provide an initial assessment of temporal behaviour. The stationarity assumption remains an important consideration when extrapolating extreme flow estimates to long return periods.

5. Empirical return periods

Annual maxima are ranked and assigned empirical exceedance probabilities using the Gringorten plotting-position formula.

The reciprocal of the estimated annual exceedance probability gives the corresponding empirical return period.

These empirical estimates provide a reference for comparison with the fitted extreme value distributions.

6. Extreme value modelling

A Generalised Extreme Value (GEV) distribution is fitted to the annual maxima using SciPy.

The fitted distribution is compared with the Gumbel distribution, which represents the zero-shape-parameter case of the GEV family.

Model behaviour is examined using quantile–quantile plots and comparisons of estimated upper quantiles.

The fitted GEV shape parameter is close to zero, suggesting behaviour broadly similar to a Gumbel distribution for this dataset.

Technologies

Python

NumPy

Pandas

Matplotlib

SciPy

Statsmodels

NRFA API

Jupyter Notebook

Key findings

Daily river flows exhibit substantial right skew, with a small number of high-flow observations contributing disproportionately to the upper tail.

Annual block maxima reduce the dataset to 52 observations for extreme value modelling.

The fitted GEV shape parameter is approximately 0.016 under SciPy's parameterisation, indicating a fit close to the Gumbel case.

At the 90th, 98th and 99th percentiles of the fitted annual maximum distribution, the GEV and Gumbel estimates are relatively similar.

These results illustrate how extreme value distributions can be used to model high-flow behaviour and estimate the magnitude of rare events.

Future work

Planned extensions include:

Add confidence intervals for annual maximum estimates and return levels using bootstrap resampling.

Implement a Peaks Over Threshold (POT) model using the Generalised Pareto Distribution (GPD).

Compare block maxima and POT approaches.

Expand model diagnostics and validation.

Investigate seasonality and potential non-stationarity more rigorously.

Quantify uncertainty in extreme return-level estimates.

Limitations

The analysis uses annual maxima from a single river gauging station, providing a relatively small sample for estimating rare extremes. Estimates associated with long return periods are therefore sensitive to model assumptions and parameter uncertainty.

The stationarity assessment is exploratory, and the fitted distribution should not be interpreted as a validated operational flood forecasting model.

Return periods describe probabilities under the assumed statistical model; they do not imply that an event will occur at regular intervals.

References

National River Flow Archive (NRFA)

NRFA Station 15012: Tummel at Pitlochry

NRFA API examples
