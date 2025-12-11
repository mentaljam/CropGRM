# CropGRM

CropGRM is a general model for crops spatial recognition based on time series of remote sensing and climate data.

## Description
CropGRM is a gradient boosting model (Catboost) and was trained on global crop data from Europe, the USA, Canada, and China. It can recognize 12 crops: winter wheat, spring wheat, spring oats, spring barley, spring rye, spring canola, sunflower, corn, soybean, sorghum, beet, potato. The features using for prediction are spectral (Landsat 5, 8, 9), phenological and climate (ERA5) data.

The project contains 3 models with different size of predictors (they can be found in a folder --models):
- CropGRM-large.cbm - 134 features (list of features in --notebooks/inference_tabular.ipynb)
- CropGRM-optimized.cbm - 82 features (list of features in --notebooks/inference_tabular.ipynb)
- CropGRM-small.cbm - 24 features (list of features in --notebooks/inference_tabular.ipynb)

Also we added a version of finetuned CropGRM-small.cbm on local data of scientific centers -  finetuned_model.cbm in folder --models

## Input data structure

In order to successfully apply the model:
- a FlatGeobuf file that contains information about the location of the fields. Each field should be assigned a unique identifier in the 'field_id' column of the attribute table. The example is in the folder --data/raw/fields.fgb
- preprocessed feature dataset from Google Earth Engine platform for each unique field. The example is in the folder --data/processed/input_data_for_model.parquet

The result can be obtained as tabular, vector or raster format.

## Project structure
```powershell
CropGRM_main/
    requirements.txt #dependencies
    README.md
    notebooks/
        inference_tabular.ipynb # instruction for making prediction in table format, as well as features required for different models
        inference_geospatial.ipynb # instruction for making prediction in raster or vector format
    models/
        finetuned_model.cbm
        CropGRM-small.cbm
        CropGRM-large.cbm
        CropGRM-optimized.cbm
    data/ #test data
        raw/ # input file FlatGeobuf
            fields.fgb
        processed/ # input table with features for model prediction
            input_data_for_model.parquet
        final/ # output files that can be get as FlatGeobuf or TIFF-file or tables
            CropMap_fields.tif
            CropMap_fields.fgb
            CropGRM-large_predictions.csv
            CropGRM-optimized_predictions.csv
            CropGRM-small_predictions.csv
```


