# CropGRM

CropGRM is a general model for crop spatial recognition based on time series of
remote sensing and climate data. It can predict 12 crop types globally.

## Features

- Recognizes 12 crops: winter wheat, spring wheat, spring oats, spring barley,
  spring rye, spring canola, sunflower, corn, soybean, sorghum, beet, potato.
- Uses spectral (Landsat 5, 8, 9), phenological, and climate (ERA5) features.
- Trained on global crop data from Europe, the USA, Canada, and China.
- Gradient boosting model implemented with [Catboost](https://catboost.ai/).

## Project structure

```sh
CropGRM
├── data # test data
│   ├── final # output files after prediction
│   ├── processed # preprocessed data for model predictions
│   └── raw # input files
├── models # pre-trained models
├── notebooks # examples and instructions
├── README.md
└── requirements.txt
```

## Models

The project includes three base models with different numbers of predictors and
a fine-tuned model (available in [models](./models)):

- [CropGRM-large.cbm](./models/CropGRM-large.cbm) - 134 features
- [CropGRM-optimized.cbm](./models/CropGRM-optimized.cbm) - 82 features
- [CropGRM-small.cbm](./models/CropGRM-small.cbm) - 24 features
- [finetuned_model.cbm](./models/finetuned_model.cbm) - fine-tuned
  CropGRM-small on local scientific center data

Feature lists are in [notebooks/inference_tabular.ipynb](./notebooks/inference_tabular.ipynb).

## Examples

Examples and instructions are available in [notebooks](./notebooks):

- [inference_tabular.ipynb](./notebooks/inference_tabular.ipynb) - instructions
  and examples for making tabular predictions including feature lists for
  different models
- [inference_geospatial.ipynb](./notebooks/inference_geospatial.ipynb) -
  instructions and examples for making geospatial predictions

Tested on Python 3.12.

## Input data

- Preprocessed feature dataset from Google Earth Engine for each field (example
  available at [data/processed/input_data_for_model.parquet](./data/processed/input_data_for_model.parquet))
- Vector dataset with field geometries, (example available at
  [data/raw/fields.fgb](./data/raw/fields.fgb)).

The two input datasets should have the same unique identifier for joining data.

The results can be obtained in tabular, vector, or raster format.
