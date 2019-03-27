# Data-analysis-with-Python--more-advanced-data-visualizations
Data visualizations using the matplotlib and seaborn libraries:

#  I.) Summary of Data visualizations:

## A.) Visualizations using the Ames, IA housing dataset:

## 1.) Barplot of covariates ranked by correlation with housing sale prices: 
Source of data: Ames, IA housing dataset (2006-2010 house price data)- (Note: for more detailed analysis of this dataset also see this repo: https://github.com/Kallen113/Python_data_analysis_Ames-IA_Housing_dataset.git).

Source code:
```
#imports
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline

#import the data:
# since the first column is unnamed and does not actually contain data, specify a range to avoid importing this column
range_1 = [i for i in range(1,118)]

#input the specified range as the argument for the pd.read_csv's usecols parameter
usecols = range_1

df_housing = pd.read_csv('Amex_IA_dataset_cleaned.csv', usecols=usecols)

# for purposes of finding correlations with SalePrice, create a new Index object and convert to list with all numeric columns from the  dataframe
numeric = df_housing.select_dtypes(include=['int64','float64']).columns

#drop the SalePrice column (since we don't want to see the correlation with itself) and ID (since it does not have any actual data for examining correlations) from the numeric Series
numeric = numeric.drop(['Id','SalePrice']) 

#convert to list
numeric  = list(numeric)

#calculate the correlations of each variable to SalePrice
corr = df_housing[['SalePrice'] + numeric].corr()

#sort the correlations by ascending: i.e., negative to highest positive
corr2 = corr.sort_values('SalePrice', ascending=False)

#initialize the figure and dimensions of the correlations with SalePrice
plt.figure(figsize=(15,17))

#use a barplot via Seaborn, and show the correlations with SalePrice
#Also, set the title for the plot
sns.barplot(corr2.SalePrice[1:], corr2.index[1:]).set_title('Ranked correlations with SalePrice')
                   
plt.show()
```
## Barplot of ranked correlations with respect to Ames, IA house sale prices for 2006-2010:
![Ames_IA_ranked_correlations_wrt_SalePrice](https://user-images.githubusercontent.com/35751364/55116926-41c91080-50a6-11e9-876f-a2886d7b007c.png)

## 2.) Countplot of homes by month and year sold:
```
#barplot of year and month sold
df_housing.groupby(['YrSold', 'MoSold']).Id.count().plot(kind='bar',figsize=(14,6))

#set title
plt.title('Years and months when Ames, IA Homes were sold')

plt.show()

```
## Countplot of Ames, IA homes by month and year sold, Jan 2006-July 2010:
![Ames_IA_countplot_of_home_year_sold](https://user-images.githubusercontent.com/35751364/55117293-899c6780-50a7-11e9-9ca7-f666c6a64e2e.png)



## B.) Visualiations using county-level Census/ACS 2017 data on educational attainment and median annual earnings:

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
## Regression and histogram jointplot showing correlation between bachelor's degree attainment and median earnings, using county-level 2017 5-year Census/ACS data:
![Bachelor's attainment vs median earnings with R2 coefficient](https://user-images.githubusercontent.com/35751364/55039148-50e58b00-4fe0-11e9-8744-8d264b515aad.png)

## C.) Visualizations using 1982-2014 Crunchbase data on startup investment funding:
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
## Countplot of invesment funding types for startups, 1982-2014 Crunchbase data:
![Countplot_Crunchbase_1982-2014_dataset](https://user-images.githubusercontent.com/35751364/55042644-b2612600-4fef-11e9-8ca0-ba0659d78703.png)
