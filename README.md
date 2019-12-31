# jupyter
jupyter notebooks scratch
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/thepinkturtle/jupyter.git/master)
---
### Note to self:
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


