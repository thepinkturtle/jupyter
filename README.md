# jupyter
jupyter notebooks scratch
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/thepinkturtle/jupyter.git/master)
---
# Note to self:
### Run locally
0. Make sure your Anaconda environment is started ```conda activate``` .
1. Navigate to the project directory ```cd ~/jupyter``` .
2. Load your dependencies ```pip install -r requirements.txt``` .
3. Start jupyter notebook ```juypter notebook``` .

To install packages from inside jupyter simply run the following command:\
```! pip install --user <package-of-choice>```
To set the theme copy and paste the following
```python
from jupyterthemes import get_themes
import jupyterthemes as jt
from jupyterthemes.stylefx import set_nb_theme
set_nb_theme('onedork')
```

### Automate backward elimination 
```python
import statsmodels.formula.api as sm
def backwardElimination(x, sl):
    numVars = len(x[0])
    for i in range(0, numVars):
        regressor_OLS = sm.OLS(y, x).fit()
        maxVar = max(regressor_OLS.pvalues).astype(float)
        if maxVar > sl:
            for j in range(0, numVars - i):
                if (regressor_OLS.pvalues[j].astype(float) == maxVar):
                    x = np.delete(x, j, 1)
    regressor_OLS.summary()
    return x
 
SL = 0.05
X_opt = X[:, [0, 1, 2, 3, 4, 5]]
X_Modeled = backwardElimination(X_opt, SL)
```

### How to encode categorical data the new way
```python
from sklearn.preprocessing import OneHotEncoder, LabelEncoder
from sklearn.compose import ColumnTransformer

// [3] is the row that contains the categorical data
ct = ColumnTransformer([('encoder', OneHotEncoder(), [3])], remainder='passthrough')
X = np.array(ct.fit_transform(X), dtype=np.float)
```


