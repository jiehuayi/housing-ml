# CMPT353 Final Project

## Prerequisites
### Interpreter (Preferred)
- Python 3.12

### Packages
- numpy           (1.26.4)
- pandas          (2.2.2)
- scipy           (1.14.0)
- geopy           (2.4.1)
- matplotlib      (3.9.0)
- scikit-learn    (1.5.1)
- joblib          (1.4.2)
- selenium        (4.22.0)
- folium          (0.17.0)
- geopandas       (1.0.0)
- branca          (0.7.2)
- glob
- os
- re

## Running the Code
### 1. Gathering Data: Web Scraping
`webScraping.ipynb` is the script used to gather data from Zoocasa.

<i style="color:gray">
Notes:

Zoocasa frequently changes the DOM structure of its website for security reasons. 

Therefore, the XPaths in the script may no longer be valid if the script was to be ran at this moment. This will raise TimeoutErrors.
We recommend use existing scraped data for other parts of the pipeline.
</i>

### 2. Data Preprocessing
The first section of `cleanTotal.ipynb` handles the initial stage of basic column cleaning operations and outputs all data to `data/ungeocoded/`.

### 3. Geocoding Data
`geocode.ipynb` contains the main logic that geocodes addresses from `data/ungeocoded/` and output the results to `data/geocoded/`.

<i style="color:gray">
Notes:

This notebook also contains other code blocks that geocode other urban datasets, which are outputted into `data/features/*`.

If you wish to re-geocode everything, you must delete all existing output files in `data/geocoded/`. This is because the process takes hours to finish and we don't want to accidentally execute the loop again.
</i>

### 4. Data Cleaning + Feature Engineering
Returning to `cleanTotal.ipynb`. The second section, "Data Cleaning + Feature Manipulations," will concatenate all city-separated data files into one dataset and extract features from the existing data.

The output will be saved as `data/predict/total_clean.csv`

<i style="color:gray">
Notes:

All data processing steps done above is also applicable for the prediction data under `data/predict/*-active-listings.csv`.

Simply change the input and output directories in each section if you wish to do so.
</i>

### 5. Analysis
`makeGraph.ipynb` contains most, if not all, statistical analysis code for this project.

`regressors.ipynb` trains, predicts, and analyzes the machine learning models used in the predictive analysis.

`metroVancouverMap.ipynb` generates interactive maps in `maps/` for geospacial analysis.

## Project Structure
```
.
│   chromedriver.exe
│   cleanTotal.ipynb
│   geocode.ipynb
│   makeGraph.ipynb
│   README.md
│   regressors.ipynb
|   metroVancouverMap.ipynb
|   metroVancouver.geojson
│   webScraping.ipynb
│
├───data
│   │   *-listings.csv
│   │
│   ├───combined
│   │       total.csv
│   │       total_clean.csv
│   │
│   ├───extra
│   │       *-listings-extra.csv
│   │
│   ├───features
│   │   ├───cityCenters
│   │   │       centers.csv
│   │   │
│   │   └───schools
│   │           *-schools.csv
│   │           schools_total.csv
│   │
│   ├───predict
│   │   │   *-active-listings.csv
│   │   │   total.csv
│   │   │   total_clean.csv
│   │   │
│   │   ├───geocoded
│   │   │       *-active-listings-geocoded.csv
│   │   │   
│   │   ├───predicted
│   │   │       output.csv
│   │   │
│   │   └───ungeocoded
│   │           *-active-listings-ungeocoded.csv
│   │
│   ├───geocoded
│   │       *-listings-geocoded.csv
│   │
│   └───ungeocoded
│           *-listings-ungeocoded.csv
│
├───graphs
│   │   *.png
│   │
│   ├───distanceToCityCenter
│   │       *.png
│   │
│   └───distanceToNearestSchool
│           *.png
│
├───maps
│       metroVancouver.html
│
└───models
        gbr.joblib
        knnr.joblib
        mlpr.joblib
        rfr.joblib
```
