## My answers

EDA summary should include AT LEAST this:
- N=1941. 
- The unit of observation is house sales, 
- from 2006-2008. 

### Regressions


```python
import pandas as pd
import numpy as np
from statsmodels.formula.api import ols as sm_ols
from statsmodels.iolib.summary2 import summary_col # nicer tables


housing = (pd
           .read_csv('input_data2/housing_train.csv')
           .assign(TotSF = lambda x: x.v_Total_Bsmt_SF + x.v_Gr_Liv_Area,
                         l_salePrice = lambda x:np.log(x['v_SalePrice']),
                         l_TotSF =  lambda x: np.log(x.TotSF)  ,
                         l_1st_Flr_SF =  lambda x: np.log(x.v_1st_Flr_SF)  ,
                         l_garage  =  lambda x: np.log(1+x.v_Garage_Area),
                         l_base  =  lambda x: np.log(1+x.v_Total_Bsmt_SF),
                         l_lot = lambda x: np.log(1+x.v_Lot_Area), 
                         age =  lambda x: x.v_Yr_Sold - x.v_Year_Built
                        )
          )

m1 = sm_ols('v_SalePrice ~ v_Lot_Area  ', data=housing).fit()
m2 = sm_ols('v_SalePrice ~ l_lot  ', data=housing).fit()
m3 = sm_ols('l_salePrice ~ v_Lot_Area  ', data=housing).fit()
m4 = sm_ols('l_salePrice ~ l_lot  ', data=housing).fit()
m5 = sm_ols('l_salePrice ~ v_Yr_Sold  ', data=housing).fit()
m6 = sm_ols('l_salePrice ~ C(v_Yr_Sold)  ', data=housing).fit()

# # format extra stats for the regression table
info_dict={'No. observations' : lambda x: f"{int(x.nobs):d}"}
info_dict={'No. observations' : lambda x: "{:,.0f}".format(x.nobs)}

# print out multiple regression results at once
table = summary_col(results=[m1,m2,m3,m4,m5,m6],
                    float_format='%0.2f',
                    stars = True,
                    model_names=['m1','m2','m3','m4','m5','m6'],
                    info_dict=info_dict,
                    regressor_order=['Intercept','v_Lot_Area','l_lot','v_Yr_Sold',
                                    'C(v_Yr_Sold)[T.2007]','C(v_Yr_Sold)[T.2008]'],
                   )
table.add_title('OLS Regressions of Sale Price')
print(table)

```

                              OLS Regressions of Sale Price
    =================================================================================
                              m1            m2         m3       m4      m5      m6   
    ---------------------------------------------------------------------------------
    Intercept            154789.55*** -328012.43*** 11.89*** 9.40*** 22.29   12.02***
                         (2911.59)    (30226.42)    (0.01)   (0.15)  (22.94) (0.02)  
    v_Lot_Area           2.65***                    0.00***                          
                         (0.23)                     (0.00)                           
    l_lot                             56037.99***            0.29***                 
                                      (3315.65)              (0.02)                  
    v_Yr_Sold                                                        -0.01           
                                                                     (0.01)          
    C(v_Yr_Sold)[T.2007]                                                     0.03    
                                                                             (0.02)  
    C(v_Yr_Sold)[T.2008]                                                     -0.01   
                                                                             (0.02)  
    R-squared            0.07         0.13          0.06     0.13    0.00    0.00    
    R-squared Adj.       0.07         0.13          0.06     0.13    -0.00   0.00    
    No. observations     1,941        1,941         1,941    1,941   1,941   1,941   
    =================================================================================
    Standard errors in parentheses.
    * p<.1, ** p<.05, ***p<.01



```python
housing.groupby('v_Yr_Sold')[['l_salePrice','v_SalePrice']].mean()
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
      <th>l_salePrice</th>
      <th>v_SalePrice</th>
    </tr>
    <tr>
      <th>v_Yr_Sold</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2006</th>
      <td>12.022869</td>
      <td>181761.648000</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>12.048460</td>
      <td>185138.207493</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>12.012588</td>
      <td>178841.750804</td>
    </tr>
  </tbody>
</table>
</div>



Written answers:

1. List $\beta_1$ for Models 1-6 to make it easier on your graders.
    - See above
1. Interpret $\beta_1$ in Model 2. 
    - A 1% increase in lot size is associated with sales prices that are \$560 dollars higher, all else equal.
1. Interpret $\beta_1$ in Model 3. 
    - A 1 st ft increase in lot size is associated with sales prices that are 0.0013% higher, all else equal.
(0.0013% is the right amount!) Not 0.000013%. 
    - I had to print out the model with more decimal points to figure that out. 
1. Of models 1-4, which do you think best explains the data and why?
    - Model 4 has the highest R2 and Adj R2
    - I had to print out the model with more decimal points to figure that out. 
1. Interpret $\beta_1$ In Model 5
    - Mechanical version: A 1 unit increase in year is assoc with sales prices that are 0.5% lower, all else equal. (not 0.005%). 
(I.e. Sales prices declined by 0.5% each year, on average, in this sample.)
1. Interpret $\alpha$ in Model 6
    - Alpha: the average log price in 2006 is 12.02. 
1. Interpret $\beta_1$ in Model 6
    - Beta1: The average price in 2007 is 3% higher than 2006. 
1. Why is the R2 of Model 6 higher than the R2 of Model 5?
    - Model 5 models the average price over time as a strict line with a slope. Model 6 *can* be a line, but it can also be any sequence of averages. Thus, model 6 is more flexible. 
1. What variables did you include in Model 7?
1. What is the R2 of your Model 7?    
1. Speculate (not graded): Could you use the specification of Model 6 in a predictive regression? 
    - Model 6: **Not well! What if your model has to be applied to a home sale in 2009? You can't estimate a beta on it because there is no 2009 observations in your sample! So year=2007 will be 0, and year=2008 will be 0. So the 2009 sales will get 2006 average prices as the predicted value!**
1. Speculate (not graded): Could you use the specification of Model 5 in a predictive regression? 
    - Model 5: Yes. (Predictive power TBD.) If the year is 2009, the predicted log price is 22-2009*(-0.01).

