# CropGRM

CropGRM is a general model for crops spatial recognition based on time series of remote sensing and climate data. 

## Description
CropGRM is a gradient boosting model (Catboost) and was trained on global crop data from Europe, the USA, Canada, and China. It can recognize 12 crops: winter wheat, spring wheat, spring oats, spring barley, spring rye, spring canola, sunflower, corn, soybean, sorghum, beet, potato. The features using for prediction are spectral, phenological and climate data.

The project contains 3 models with different size of predictors (they can be found in a folder --models):
- CropGRM-large.cbm - 134 features (list of features in --notebooks/making_prediction.ipynb)
- CropGRM-optimized.cbm - 82 features (list of features in --notebooks/making_prediction.ipynb)
- CropGRM-small.cbm - 24 features (list of features in --notebooks/making_prediction.ipynb)

Also we added a version of finetuned CropGRM-small.cbm on local data of scientific centers -  finetuned_model.cbm in folser --models

## Installation

```bash
git clone https://github.com/username/project.git
cd project
pip install -r requirements.txt
```

## Project structure
```powershell
CropGRM_main/
    requirements.txt #dependencies
    README.md
    notebooks/
        making_prediction.ipynb # instruction for making prediction in table format, as well as features required for different models
        map_generating.ipynb # instruction for making prediction in raster or vector format
    models/
        finetuned_model.cbm
        CropGRM-small.cbm
        CropGRM-large.cbm
        CropGRM-optimized.cbm
    data/ #test data
        raw/ # input shapefile with fields and necessary field 'field_id'
            2015.shp
            2015.dbf
            2015.shx
            2015.prj
            2015.cpg
        processed/ # input table with features for model prediction
            2015.parquet.gzip
        final/ # output files that can be get as shapeile or tif-file or tables
            2015.tif
            2015.dbf
            2015.shp
            2015.shx
            2015.cpg
            2015.prj
            2015_CropGRM-large_predictions.parquet.gzip
            2015_CropGRM-optimized_predictions.parquet.gzip
            2015_CropGRM-small_predictions.parquet.gzip
```