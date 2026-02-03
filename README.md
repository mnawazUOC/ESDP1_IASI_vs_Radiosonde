# ESDP Final Project – Data Processing Pipeline of Water Vapour Profiling over Ny-Ålesund
 
**Module:** Earth System Data Processing (ESDP1)  
**Semester:** Winter Semester 2025/26  
**Student:** Mohammed Fawaz Nawaz  
**Study Area:** Ny-Ålesund, Svalbard  
**Time Period:** January–February 2025  
 
---
 
## 1. Project Aim
 
The aim of this project is to **compare vertical profiles of atmospheric water vapour** over Ny-Ålesund using two independent observing systems:
 
- **Radiosondes** (in-situ reference)
- **IASI satellite observations** (space-based remote sensing)
 
The focus is on building a **clean, reproducible data-processing workflow** that allows meaningful comparison despite differences in:
- temporal sampling,
- vertical coordinates,
- and data formats.


The workflow focuses on:
- automated data access (API-based satellite retrieval),
- timestamp extraction and temporal matching,
- preprocessing and standardization of heterogeneous datasets,
- vertical alignment on a common pressure grid,
- generation of comparable water vapour profiles,
- and reproducible visualization of results.
 
The project emphasizes clean workflow design, reproducibility, and modular
implementation.
 
---
 
## 2. Datasets Used
 
### Radiosonde
- Source: Ny-Ålesund radiosonde dataset (`rs_iop4h2o.nc`)
- Variables used: pressure, specific humidity, launch time
- Used as the **reference dataset** due to high vertical resolution
 
### IASI (Infrared Atmospheric Sounding Interferometer)
- Source: EUMETSAT (via EUMDAC API)
- Product: IASI humidity profiles
- Vertical coordinate: pressure levels
- Spatial selection: nearest pixel to Ny-Ålesund
 
**Note:** Raw data files are not included in this repository due to size constraints.
 
---
 
## 3. Methodology Overview
 
The workflow implemented in this project consists of the following steps:
 
1. **Data Collection**  
   - Radiosonde data loaded from NetCDF file  
   - IASI products queried and downloaded via EUMETSAT API  
 
2. **Data Preprocessing**  
   - Conversion of radiosonde launch times to UTC  
   - Extraction of IASI profiles nearest to Ny-Ålesund  
 
3. **Temporal Matching**  
   - IASI overpasses matched to radiosonde launches within a ±1 hour window  
 
4. **Data Harmonisation**  
   - Conversion of humidity units to common units (g/kg)  
   - Pressure levels converted to a common pressure grid  
 
5. **Vertical Alignment**  
   - Interpolation of both datasets onto a fixed pressure grid  
 
6. **Quality Control**  
   - Removal of non-physical values  
   - Filtering of poorly matched profiles  
 
7. **Statistical Analysis**  
   - Computation of mean profiles  
   - Calculation of Bias and RMSE relative to radiosonde measurements  
 
---
 
## 4. Repository Structure

The repository is organised to clearly separate analysis, code, and documentation:
notebooks/
Contains the main Jupyter notebook used for the project.
This notebook includes the complete workflow: data access, preprocessing, temporal matching, analysis, and visualisation of IASI and radiosonde water vapour profiles.
README.md
Provides an overview of the project, datasets used, methodology, repository organisation, and instructions for reproducibility.
.gitignore
Ensures that large data files, credentials, and temporary outputs are excluded from version control.
outputs
It includes output such as figures obtained during results.
data
- Radiosonde data loaded from NetCDF file  (`rs_iop4h2o.nc`)
- IASI products queried and downloaded via EUMETSAT API 

---
 
## 5. Data Availability
 
- Radiosonde data loaded from NetCDF file  (`rs_iop4h2o.nc`)
- IASI products queried and downloaded via EUMETSAT API 
 
---
 
## 6. Key Findings (Summary)
 
- Both IASI and radiosonde show decreasing water vapour with height.
- IASI underestimates near-surface water vapour relative to radiosondes.
- Agreement improves in the mid–upper troposphere.
- Differences are consistent with known limitations of satellite infrared sounding in Arctic conditions.
 
---
 
## 7. Requirements
 
Main Python packages used:
- numpy
- pandas
- xarray
- matplotlib
- netCDF4
- eumdac
 
---
 
## 8. Notes
 
- No hardcoded timestamps are used; all temporal information is derived directly from datasets.
- Code is modular and can be extended to include additional datasets if needed.
 
---END---
 
