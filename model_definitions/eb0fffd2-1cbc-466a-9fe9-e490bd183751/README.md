# Bank Marketing in python with H2O GBM
## Overview
Bank Marketing demo model using H2O GBM in python

## Datasets
The dataset required to train or evaluate this model comes from the UCI Machine Learning repository available [here](https://archive.ics.uci.edu/ml/datasets/bank+marketing).
This dataset is available in Teradata Vantage and already configured in the demo environment.

Training
```json
{
    "table": "<training dataset>"
}
```
Evaluation

```json
{
    "table": "<test dataset>",
    "predictions": "<output predictions dataset>"
}
```

Batch Scoring
```json
 {
     "table": "<score dataset>",
     "predictions": "<output predictions dataset>"
 }
 ```

    
## Training
The [training.py](model_modules/training.py) produces the following artifacts

- model.h20        (h2o trained model binary)
- model.pmml       (pmml version of the trained model)
- mojo.zip         (h2o mojo version of the trained model)
- h2o-genmodel.jar (jar file with some libraries required for the mojo file when deployed in production)

## Evaluation
Evaluation is performed in [evaluation.py](model_modules/evaluation.py) by the function `evaluate` and it returns the following metrics

    Gini: <gini>
    MSE: <mse>
    RMSE: <rmse>
    LogLoss: <logloss>
    AUC: <auc>
    AUCPR: <aucpr>
    Accuracy: <accuracy>
    Mean Per-Class Error: <mpce>
    F1 score: <f1>
    Precision: <precision>
    Sensitivity: <sensitivity>
    Specificity: <specificity>
    Recall: <recall>

## Scoring
The [scoring.py](model_modules/scoring.py) loads the model and metadata and accepts the dataframe for prediction.

### Batch mode
In this example, the values to score are in the table 'BANK_MARKETING_DATA' at Teradata Vantage. The results are saved in the table 'BANK_MARKETING_PREDICTIONS'. When batch deploying, this custom values should be specified:
   
   | key | value |
   |----------|-------------|
   | table | BANK_MARKETING_DATA |
   | predictions | BANK_MARKETING_PREDICTIONS |

### RESTful Sample Request

    curl -X POST http://localhost:5000/predict \
            -H "Content-Type: application/json" \
            -d '{
                "data": {
                    "ndarray": [
                            35,
                            "blue-collar",
                            "married",
                            "primary",
                            "no",
                            5883,
                            "yes",
                            "yes"
                    ]
                }
            }' 
Evaluation dataset for bank marketing example
