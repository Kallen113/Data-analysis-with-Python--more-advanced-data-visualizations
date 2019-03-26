# Data-analysis-with-Python--more-advanced-data-visualizations
Data visualizations using the matplotlib and seaborn libraries:

Code demo of Data visualization:

Using the scipy library's stats module, various statistics such as the pearson correlation coefficient (r) can be calculate. To find the R^2
coefficient, one can merely take the square of this coefficient. 

The R^2 coefficient can then be displayed and applied to the regression plot:
Regression plot with line of best fit and R^2 coefficient (i.e., coefficient of determination), example from IPython Jupyter notebook:
```
import seaborn as sns
import matplotlib.pyplot as plt

#import scipy to perform the R^2 calculation
from scipy import stats

#specify the variable for the x axis
xa = edu_attain["Bachelor's_degree_%"]

#specify the y-axis variable
ya = edu_attain["Median_earnings_2017"]

#calculate R^2, and implement a jointplot with the R^2 displayed
def R_2(x, y):
    '''calculate the R^2 coefficient by taking the square of the pearsonr calculation
    by the scipy library, and have this appear in the plot'''
    return stats.pearsonr(xa, ya)[0] **2   #calculate the R^2 coefficient by taking the square of the pearson correlation coefficient
sns.jointplot(xa, ya, kind = 'reg', stat_func=R_2)

```
![Bachelor's attainment and median earnings with R2 coefficient](/Bachelor's attainment vs median earnings with R2 coefficient.png)
