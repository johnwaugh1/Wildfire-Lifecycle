# Burn Severity Classification

This project aimed to build a end to end machine learning pipeline for predicting wildfire burn severity at the pixel level using remote-sensing data. The pipeline integrates Earth Engine-based data extraction, preprocessing, feature engineering, and supervised ML model training to classify burn severity into four MTBS-style classes: Unburned, Low, Moderate, High. The final model learns to estimate severity for a new, unseen wildfire using only pre and post fire spectral, topographical, and environmental features.

The project downloads and processes inputs from the following datasets:
  - MTBS Burned Area Boundaries (fire perimeters + assessment metadata)
  - Sentinel-2 SR (NDVI, NBR, pre/post composites @ 30 m)
  - SRTM DEM (elevation, slope, topographic derivatives)
  - ESA WorldCover (land-cover class)
  - ERA5-Land (temperature)
  - CHIRPS (precipitation)

The workflow is organized into five main notebooks:
  - Data Extraction: Queries MTBS fire boundaries, retrieves pre and post fire satellite imagery, computes vegetation indices (NDVI, NBR), downloads DEM, landcover, climate data, and saves everything as GeoTIFFs per fire event.
  - Data Validation: Ensures all rasters cover the fire AOI, checks CRS consistency and alignment, makes sure no files are missing or corrupted.
  - Data Preprocessing: Reprojects rasters into a unified CRS, builds reference grid per fire, resamples all rasters to same pixel alignment, flattens raster stacks into structure tabular feature matrices, attaches MTBS severity label to each pixel.
  - Model Training: Splits fires into train/validation/test by fire event, handles class imbalance via class weights, trains 5 models: Logistic Regression, Random Forest, XGBoost, LightGBM, CatBoost, and computes precision, recall, F1, confusion matrices.
  - Result Visualization: Generates confusion matrices, metric ranking tables, correlation matrices, etc based on training results.

Although models were trained sucessfully and performance shows good predictive skill despite class imbalance, there are still many future improvements that could boost performance of the models ability to predict on unseen fire events.
