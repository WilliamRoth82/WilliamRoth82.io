# Will's bestest predicting model ever!


```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

from sklearn import linear_model
from sklearn import ensemble
from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline, make_pipeline 
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import StandardScaler 
from sklearn.preprocessing import OneHotEncoder 
from sklearn.compose import ColumnTransformer, make_column_selector
from sklearn.compose import make_column_transformer
from sklearn.model_selection import KFold, cross_validate, GridSearchCV
from sklearn.metrics import r2_score

from df_after_transform import df_after_transform
```


```python
# import data
housing_df = pd.read_csv('input_data2/housing_train.csv')
```


```python
# load sets 
y_train = np.log(housing_df.v_SalePrice)
X_train = housing_df.drop('v_SalePrice', axis = 1)
```


```python
# get all numerical variables
numerical = ['int16', 'int32', 'int64', 'float16', 'float32', 'float64']

numericalVars = X_train.select_dtypes(include = numerical).columns.tolist()
```


```python
# create pipeline
num_pipe = make_pipeline(SimpleImputer(strategy="median"), StandardScaler())
cat_pipe = make_pipeline(OneHotEncoder())

preproc_pipe = ColumnTransformer(
    [("num_impute", num_pipe, numericalVars), 
     ("cat_trans", cat_pipe, ['v_Lot_Config'])
    ], 
    remainder = 'drop'
)
```


```python
# preprocess X_train
preproc_df = df_after_transform(preproc_pipe, X_train)

# data descriptors
#print(f'There are {preproc_df.shape[1]} columns in the preprocessed data.')
#preproc_df.describe().T.round(2)
```


```python
# other regressor models 

# Linear Regression
# Support Vector Regression
# KNeighborsRegressor
# RandomForestRegressor
```


```python
# create template pipeline w/ GradientBoostingRegressor Model

temp_pipe = Pipeline([
    ('preproc', preproc_pipe), 
    ('feature_create', 'passthrough'), 
    ('feature_select', 'passthrough'), 
    ('estim', ensemble.GradientBoostingRegressor())
])
```


```python
# display template pipeline

#temp_pipe.get_params()
```


```python
# insert parameters here
params = [
    {'estim__learning_rate': [0.1128, 0.1129, 0.1130, 0.1131, 0.1127] 
     }
]
```


```python
# run grid serach
grid_search = GridSearchCV(estimator = temp_pipe, 
                           param_grid = params, 
                           scoring = 'r2', 
                           cv = KFold(10))

results = grid_search.fit(X_train, y_train)

resultsDF = pd.DataFrame(results.cv_results_)
```


```python
# print results
resultsDF
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>mean_fit_time</th>
      <th>std_fit_time</th>
      <th>mean_score_time</th>
      <th>std_score_time</th>
      <th>param_estim__learning_rate</th>
      <th>params</th>
      <th>split0_test_score</th>
      <th>split1_test_score</th>
      <th>split2_test_score</th>
      <th>split3_test_score</th>
      <th>split4_test_score</th>
      <th>split5_test_score</th>
      <th>split6_test_score</th>
      <th>split7_test_score</th>
      <th>split8_test_score</th>
      <th>split9_test_score</th>
      <th>mean_test_score</th>
      <th>std_test_score</th>
      <th>rank_test_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.770772</td>
      <td>0.020499</td>
      <td>0.005782</td>
      <td>0.000587</td>
      <td>0.1128</td>
      <td>{'estim__learning_rate': 0.1128}</td>
      <td>0.921781</td>
      <td>0.864645</td>
      <td>0.886064</td>
      <td>0.880770</td>
      <td>0.767492</td>
      <td>0.870976</td>
      <td>0.877148</td>
      <td>0.784574</td>
      <td>0.843924</td>
      <td>0.877631</td>
      <td>0.857500</td>
      <td>0.044852</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.774695</td>
      <td>0.016596</td>
      <td>0.005799</td>
      <td>0.000378</td>
      <td>0.1129</td>
      <td>{'estim__learning_rate': 0.1129}</td>
      <td>0.910405</td>
      <td>0.862323</td>
      <td>0.886096</td>
      <td>0.880246</td>
      <td>0.763579</td>
      <td>0.860863</td>
      <td>0.877658</td>
      <td>0.788509</td>
      <td>0.847795</td>
      <td>0.845040</td>
      <td>0.852251</td>
      <td>0.042579</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.826950</td>
      <td>0.022032</td>
      <td>0.006107</td>
      <td>0.000698</td>
      <td>0.113</td>
      <td>{'estim__learning_rate': 0.113}</td>
      <td>0.921323</td>
      <td>0.861661</td>
      <td>0.887722</td>
      <td>0.870243</td>
      <td>0.758338</td>
      <td>0.874552</td>
      <td>0.878520</td>
      <td>0.781549</td>
      <td>0.850395</td>
      <td>0.874005</td>
      <td>0.855831</td>
      <td>0.046686</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.828358</td>
      <td>0.027019</td>
      <td>0.006108</td>
      <td>0.000546</td>
      <td>0.1131</td>
      <td>{'estim__learning_rate': 0.1131}</td>
      <td>0.919507</td>
      <td>0.865085</td>
      <td>0.882495</td>
      <td>0.876536</td>
      <td>0.762048</td>
      <td>0.871911</td>
      <td>0.880452</td>
      <td>0.770487</td>
      <td>0.846752</td>
      <td>0.870076</td>
      <td>0.854535</td>
      <td>0.047426</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.821501</td>
      <td>0.034226</td>
      <td>0.006174</td>
      <td>0.000663</td>
      <td>0.1127</td>
      <td>{'estim__learning_rate': 0.1127}</td>
      <td>0.919244</td>
      <td>0.865185</td>
      <td>0.886335</td>
      <td>0.879806</td>
      <td>0.766001</td>
      <td>0.858832</td>
      <td>0.878918</td>
      <td>0.780664</td>
      <td>0.867277</td>
      <td>0.836307</td>
      <td>0.853857</td>
      <td>0.045110</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# create best model
best_model = results.best_estimator_
```


```python
# fit best model on train sets
X_test = pd.read_csv('input_data2/housing_holdout.csv')

best_model.fit(X_train, y_train)

y_pred = best_model.predict(X_test)
y_pred = pd.DataFrame(y_pred)
y_pred = y_pred.reset_index()

parcel = pd.DataFrame(X_test['parcel'])
parcel = parcel.reset_index()
```


```python
# merge sales est and parcels 

submission = parcel.merge(y_pred, on='index')
submission = submission.drop(columns=['index'])
submission = submission.rename(columns={0:'prediction', 1: 'parcel'})
```


```python
# export best estimate
submission.to_csv('submission/MY_PREDICTIONS.csv', index=False)
```
