# Data-analysis-with-Python--more-advanced-data-visualizations
Data visualizations using the matplotlib and seaborn libraries:

Code demo of Data visualization:

Using the scipy library's stats module, various statistics such as the pearson correlation coefficient (r) can be calculate. To find the R^2
coefficient, one can merely take the square of this coefficient. 

The R^2 coefficient can then be displayed and applied to the regression plot:
Regression plot with line of best fit and R^2 coefficient (i.e., coefficient of determination), example from IPython Jupyter notebook, using Census 2017 ACS educational attainment data:
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
![Bachelor's attainment vs median earnings with R2 coefficient](https://user-images.githubusercontent.com/35751364/55039148-50e58b00-4fe0-11e9-8744-8d264b515aad.png)

Countplot of investment funding types, 1982-204 Crunchbase data:
```
#import pyplot so dimensions of the figure can be modified
from matplotlib import pyplot

#input dimensions into the figure
fig, ax = pyplot.subplots(figsize=(13, 10))

#resize font of the titles and tickmarkers
sns.set(font_scale = 1.5)

#set style to whitegrid for better visability
sns.set_style('whitegrid')

sns.countplot(x="funding_round_type", data =startup_data, ax = ax, palette = "Greens")

#set ticklabels to rotate the x-axis labels; this will make the labels display more cleanly
ax.set_xticklabels(ax.get_xticklabels(), rotation=40, ha="right")

#set main plot title
ax.set_title('Countplot of investment funding types')

```
![Countplot_Crunchbase_1982-2014_dataset](https://user-images.githubusercontent.com/35751364/55042644-b2612600-4fef-11e9-8ca0-ba0659d78703.png)
