# Increase sales by selling the right item at the right locations
## An exploration of the relationship between item types and outlet sales

Author: Aisling Gilder 

### Business problem:

Using space efficient is essential to maximising profits. Do larger outlets sell more meat or household goods? Do smaller locations sell more soft drinks or vegatables? This data exploration and the model derived from it will allow you to increase sales by detecting the higher selling categories per location type.


### Data:
The data used for this model is from the Big Mart Sales Prediciton set, hosted here: https://datahack.analyticsvidhya.com/contest/practice-problem-big-mart-sales-iii/. It is a data set of 8523 rows, with 12 different columns, contain pricing and type desctiptions for items as well as many different categorical metrics for the outlet locations. The full description is posted below:

| Variable Name | Description | 
| ------------- |:-------------:|
| Item_Identifier | Whether the product is low fat or regular |
| Item_Weight | Weight of product    |
| Item_Fat_Content | Whether the product is low fat or regular     |
| Item_Visibility | The percentage of total display area of all products in a store allocated to the particular product      |
| Item_Type | The category to which the product belongs |
| Item_MRP | Maximum Retail Price (list price) of the product |
| Outlet_Identifier | Unique store ID |
| Outlet_Establishment_Year| The year in which store was established |
| Outlet_Size	| The size of the store in terms of ground area covered |
| Outlet_Location_Type | The type of area in which the store is located |
| Outlet_Type	| Whether the outlet is a grocery store or some sort of supermarket |
| Item_Outlet_Sales |	Sales of the product in the particular store. This is the target variable to be predicted. |

## Methods
- The data went through the stanarad cleanign procedures if removing dupilcates and handeling missing data. Two columns, Item_Wight and Outlet_Size we missing ~18% and 29% of data, respectivally. Given the large number of values that would have to be filled it, it would most certainly warp the data trends too much to be useful. As such, both columns were dropped.
- Special note on outliers. There are some high outliers in the Item_Outlet_Sales column. However, as these reprent items that generate extremtly high sales, the outliers were included in this data model

## Data Visualizations

#### Oulet Sales by Item Type
![itemsales](https://user-images.githubusercontent.com/101794920/171062749-5ede6b3f-575b-4a5f-b301-886c68c15633.png)

> Diary & Starchy foods have the highest maximum. They are also biased low, indecating higher prices overall and looks like a good item category to focus on. Baked goods, for the additional cost in labor, generate relatily lower mean sales vs the other categories

#### Distribution of Sales by Outlet Type
![Dist of Sales](https://user-images.githubusercontent.com/101794920/171062872-f1c0bfd4-a552-4c62-8501-3a5fc401c6f1.png)

> Supermarket Type 2 form the bulk of the sales volume. Any increases to sales for this category would have a larger inpact on total sales. Grocery Store has the lowest overall sales, so implenting model-based strageties here would shift the sales distrubion curve to the right.

### Correlation Heatmap
![corrmap](https://user-images.githubusercontent.com/101794920/171062928-39920dbb-c68f-4696-bd0e-a381f24f0db1.png)

>From the numeric data alone, there is only a moderate correclation between Item_MRP and Item_Outlet_Sales. This is intuitive, as selling items for a higher price should lead to increase sales. 

## Results

Two models, a Linear Regression Tree and a Random Forest Rergression model. were generated, optimized, and tested on the data. The were measured and compared via the following metrics:
|Metric |Despciption|
| ------------- |:-------------:|
|MAE - Mean Absolute Error | Mean absolute error measures the average of the absolute values of all of the errors our model makes. |
|MSE - Mean Squared Error | Mean squared error is similar to mean absolute error, but it penalizes large errors more. |
|RMSE - Root Mean Squared Error | Root mean squared error is the square root of the mean squared error. Penalizes large errors and is in same unit as target|
|R2 or R^2 - R-Squared Score | The R2 score is also called the coefficient of determination, and it describes the percentage of the variation in the target variable that a model can explain by using all the features together. |

The results are as follows:
| Model Name | MAE($) | MSE($^2) | RMSE Score($) | R2 Score |
| ---------- |:---:|:---:|:----:|:--:|
|Tree Training | 762.58 | 1,172,164.97 | 1,082.67 | 0.60 |
|Tree Testing | 738.34 | 1,118,083.68 | 1,057.39 | 0.59 | 
|Forest Training | 755.42 | 1,152,608.49 | 1,073.60 | 0.61 |
|Forest Testing | 728.45 | 1,096.095.77 | 1,046.95 | 0.60 |

We can see that both models give similar results, but I have chosen the Random Forest model for the higher R2 score and lower Mean Average Error.

## Model

The Random Tree model was first ran and generate an R2 score of 0.56. This was quite a bit higher than the inital Tree model score of 0.21.
The mean squared error is a resonable 728.45, given that over half the sales totals are 1794 and higher. This could be reduced by using a tighter data range or increase the size of the data pool. The RMSE score over 1,000 does indicate the influence the included outliers is having on our model. Removing them from the data set would also increase the model's accuracy. 

As is, the model can modestly predict the best item's to target with increase sales and marketing support in order to increase overall sales. It will work well for the vast majority of items, with those of a luxary price will be more prone to error.


## Recommendations

Volume, volume, volume! This is the key factor for increasing sales. 
If there was only one item type to increase sales on, it would be dairy. It has the largest range of sales prices within the error bars, as well as a signifcant population of outliers. Given the perishable nature of dairy products, this ensures that customers will be back to buy again within a week or to. As opposed to dried and canned foods that can be stored in the pantry for months.



## Limitations & Next Steps

The large outliers in Item_Outlet_Sales would be removed for a second iteration of the model. This would narrow down the error values and give more actionable information for the vast majority of items. Additional metrics, but the population or average household income on the city or town the outlet is in would be usefull to the model. As they can show trends based on income, family size, and any urban/suburban/rural factors. 
Similarly, fruits & vegetables is another good category, being even more parishable than dairy. With access to global supply chains, even locally out of season goods than be brought and had sales & marketing attetion brought to them.
Seafood is a solid category to increase sales. Owed to is larger volume of 2nd and 3rd quartile sales. Though, due to the nature of the product, the higher average cost may not do well in all markets.
Lastly, snack foods are great choice for increased sales. We will live in a go go go society, though that has been dampened in recent years. Though that doesn't seem to be affected it too much. Afterall, who doesn't like candy. 
These changes would be most effect when applied to the Supermarket Type 1 locations, as they make up the bulk of the sales volume. Grocery stores, being the lowest selling location class, but benefit greatly from the increase in diary and snack foods due to there usual proximity to residencial areas and foot traffic. Send Billy or Mandy down to the store for some milk before dinner, and they might grab a candy bar for the walk home.

### For further information
More in depth disccusion of the data can be seen in the Food_Sales_Prediction_v1_0 notebook included in this repsotory

For any additional questions, please contact me via LinkdIn, www.linkedin.com/in/aisling-gilder-data-science-student
