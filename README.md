# Predicting Used Cars Prices using Machine Learning 

## Introduction

Nowadays, cars are one of the necessaities of life in UK. Therefore, buying and selling the used cars is a top business in United Kingdom. However, there is always a financial risk attached in this business for buyers and sellers to ensure the fair pricing of the car based on its market value which lessens the likelihood of overpaying or underselling. Consequently, assesing the vehicle's features to predict the fair price of the car is paramount to keep this market run reliably to support consumers and sellers through promoting the transparecy into the business.

### Objective

* Analyze the dataset of 100000 used cars open sourced on Kaggle.
* Clean and transform the data into the uniform format. 
* Build a machine learing model to predict the price of the cars based on their features.

## Data Description:

**There are 13 data files which present the data of 11 car companies.The 9 data files that are mentioned below have same columns i.e. _model_, _year_, _price_, _transmission_, _mileage_, _fuelType_, _tax_, _mpg_	,_engineSize_**.
* audi
* bmw
* ford
* hyundai
* mercedes 
* skoda
* toyota
* vauxhall
* volkswagen  

**However, following two data files contain 7 columns i.e. _model_, _year_, _price_, _transmission_,	_mileage_, _fuelType_, _engineSize_**.
* focus
* cclass

**There is also a couple of unclean data files of focus and cclass:**
* unclean focus
* unclean cclass

### Data manipulation and cleansing:

Following are the columns which are present in the cleaned data files:  
* **model:** It contains the model of the car.
* **year** : It represents the year when the certain model came out. 
* **price**: Represents price of the car based its mentioned features and also is the targeted variable.
* **transmission**: Contains the tramission type of the vehicle i.e. Manual or Automatic. 	
* **mileage**	: Contains the milleage of the car.
* **fuelType**	: It contains the fuel type for the car i.e. Patrol or Diesel.
* **tax**	: Gives information about the amount of tax imposed on the model.  
* **mpg**	: The miles per gallon (mpg )provides the fuel average of the model 
* **engineSize**: Shows the engine size of the vehicle in litres.

Following are the notables from the data exploration:

* However, **cclass** and **focus** have missing columns,i.e. tax and mpg.
* The **hyundai** has a 'tax £' column which is inconsistent with column name 'tax'.
* Add **''company'' column** for each of the data file which represents the models' company which diffentiate vehicles after merging the data files.
* Two of the data files i.e. **unclean cclass** and **unclean focus** are inconsistent as compared to the other data files and have missing data which needs to be cleaned and transformed. 

Now the 2 uncleaned data files i.e. _unclean focus_ and _unclean cclass_ have inconsistent and missing data which needs to be cleaned to make it consistent with the other data files. The uncleaned data files contain the following columns:

* **model:**  
* **year:**  
* **price:**  
* **transmission:**  
* **mileage:**  
* **fuel type:**  
*  **engine size:**  
* **mileage2:**  
* **fuel type2:**  
* **engine size2:**  
* **reference:**  

Following are the notables while exploring the uncleaned data files:

* Explore the unique values of each of the columns show that there are some incorrect values which needs to be sorted.  
* The prices in the price column are with the "_£_" sign and some spaces as well which need to be removed.  
* _fuelType_ contains incorrect values but _fuelType2_ has the correct values, therefore _fuelType_ column will be dropped.  
* The values in the _engine size_ column represents the prices and also the _tax_ column is missing in these files. Therefore, keeping in view the values, this column can be deemed as _tax_ column.  
* _engine size2_  column will be considered as _engineSize_. But the values in the _engine size2_ are in CC and to make it consistent with the other data files, it will be converted into litres.   
* Both the columns _mileage_ and and _mileage2_ seems to have correct values but to keep the single value,  the greater value from both columns will be reatained in a mileage column and the rest will be dropped.   
* There is'nt any mgp column, therefore a new column of _mpg_ will be created and filled with the nan values
* _Reference_ column will be dropped as it is not needed.  

**_Now the data is consistent with the other data files and all the files can be merged into the single dataframe._**

### Data Exploration:

#### Missing Data:    
The heatmap below shows the missing values indicated by the yellow bars. It represents that _mpg_ and _tax_ column has a significant amount of missing values which mark approximately 16% and 8% respectively and it also makes sense as these two columns were missing in the _cclass_ and _focus_ data files. However, there is a a very few missing values in the other columns as well.Therefore, the missing values in the numeric columns are imputed using mean and in the categorical column median is used to fill the missing data.  
![Null Value](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/null_values.png)



#### Outlier Handling:

Only two columns contain outliers. Almost 7% of the values from price and mileage columns are detected as outliers. Therefore, as 7% is not an insignificant value to be dropped. Therefore, capping through interquantile range will be applied to deal with outliers.  

![Identifying Outliers](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/outliers.png) 
![Outliers Handling](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/outlier_handling.png)

**_NOW THE DATA IS ALL SET FOR THE ANALYSIS_**

## Exploratory Data Analysis

After cleaning and transforming the data, all the files are combined into one data file for analysis. Following are the insights extracted from the data:

The plot below shows the correlation within the features. The target variable i.e. price is positively correlated with the engine size and tax, whereas it has negative correlation with mileage and mpg. 
!['Features Correlation'](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/features_correlation.png)

In the below plot of companies VS the number of cars, it can be seen that Ford has 17962 car which are the most in number as compared to the other companies followed by Volks Wagon with 15155 cars and Mercedez with 13117 as the second most and third most number of cars respectively. However, Hyundai has the least number of cars.

![Number of Cars by Companies](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/number_of_cars_by_companies.png)

The plot below shows the cars count per year with respect to their companies.Most of the cars are from 2013 to 2020.

![num of cars by campany per year](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/number_of_cars_by_companies_per_year.png)

The plot below shows the companies and their average mileage. BMW vehicles have are more used than the other its average milleage is greater than others. However, skoda vehicles have the least milleage.    
![company VS Mileage](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/companies_with_average_milleage.png)  

BWM has the most taxes followed by the slight difference in the Mercedez and Audi followed by the second most and the third most taxes respctively. As tax is directly correlated with the price so it can be said that these vehicles are largely expensive than the others with low taxes.  
![companies vs tax](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/companies_with_average_tax.png)

The plot below shows the number of cars per year from 2020 to 1991. Most of the cars are from the year 2019. However, approximately 90% of the vechicles are from 2013 to 2020 and 10% of the total cars are from 1991 to 2012.
![Number of cars per year](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/number_of_cars_by_years.png)

The count plot presents number of cars by the transmission type. Manual cars are the most in number count up to approximately 65000. However, the semi-auto and the automatic nearly sums up to 28000 and 25000 respectively. 
![cars by fuel type](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/cars_by_fuel_type.png)

In the figure below, it can be observed that the number of vahicles by each company by its transmission type where blue bar represents the manual cars, while orange as automatic, semi-auto cars are represented by green bars and red is used to represent the any other type except these mentioned. Therefore, Ford has the most number of manual cars, while Mercedez has the most number of automatic and semi-auto vehicles. However, any other transmission type has a negligiable number. 
![Companies and number of Transmission Type Rate](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/companies_and_transmission_type_rate.png)

Each of the company is represent below by its number of cars by the fuel type. Therefore, blue bar represents teh cars on petrol, while orange, green and red bars are for diesel, hybrid, and others respectively. The purple color is for the electric vehicles but are a very few in numbers. Ford has the most number of petrol cars, while Medcedez and Toyata have the most number diesel and hybrid cars repectively.

![Companies by Fuel Types](https://github.com/muhammadfhaider12/predicting-uk-used-cars-prices/blob/main/plots/Companies_and_fuel_type_rate.png)

## Data Preprocessing

Before fitting the machine learning models, the data needs to processed and tranformed into the numeric form. Therefore following are the sterps followed at this stage:
* New columns have been added which are the tranformation of categorical variables into binary or numeric form using one hot encoding.
* The categorical columns are then dropped as the encoded columns contain all the information of those categorical columns.
* The *company* feature that been added for data insights, has now been dropped as it won't be helpful in predicting the car prices.  


Now the entire data is in the numeric form and can now be feeded into machine learning algorithms. However, it is still one step away from modelling. One of the models whcih will be used for this project is the K-Nearest Neighbors(KNN). KNN is the distance based algorithm which calculates the distance between the data points to predict the results. Therefore, it is sensitive to the magnitude of the fatures. For such algorithms,  data needs to be scaled using feature scaling techniques so that all the features contribute equally while predicting the outcome. Hence, in this preprocessing phase, the data is scaled using **_StandardScaler()_** method.
























## Data Modelling

4 of the data machine learning algorithms have implemented for predicting the prices of the cars. However, the selection criterion of the model is based on the some performing matrices and selection parameters.  
### Measuring Parameters:  
* **Model Complexity:**  
Each model has its own trainning process. Some models are simpler and others are complex comparitively.Linear models are simpler than the ensemble methods and ensemble methods are less complex than the deep learning models as it goes into more depth in recognizing the patterns within the data. Therefore, it is also a parameter that is considered while recommending the final model.  
  
  
* **Trainning Time:**  
Trainning time is also a crucical factor while trainning the dataset. However, this dataset is not very large so trainning time would be a big factor because large and compex datasets take more time while trainning but it will still still be considered when selecting final the model.  

### Performing Matrices:   
  
**R2 Score:**  
One of the common and most used measures while evaluation the regression models' performance is R-squared or cofficient of determination. Its value ranges from 0 to 1, as0 being the least and 1 being the best fit.  

**Mean Squared Error(MSE):**  
It is the value of the average difference between the actual value and the predicted value. Lower the mean square error better will be the results.  

**Root Mean Squared Error(RMSE):**  
It is square root of MSE as it provides the more interpratable values by providing the results in the same unit as of the target variable.  
Now the models which are implemented are the following along with their results:  

| *Model*                 |*Validation Score*      |*Mean Absolute Error*      |*Mean Square Error*    |*Root Mean Squared Error*  
|-:                       |:-:                     |:-:                        |:-:                    |:-:  
|Decision Tree Regressor  |0.94                    |0.15                       |0.06                   |0.25  
|Random Forest Algorithm  |0.96                    |0.12                       |0.05                   |0.22  
|XG Boost Model           |0.94                    |0.15                       |0.05                   |0.22  
|K-Nearest Neighbor       |0.95                    |0.14                       |0.046                 |0.21
  
Based on the performing matrics, _Random Forest Algorithm_ is recommended as the most efficient and accurate model for this dataset with the accuracy of nearly 96% and RMSE value of less than 2%.  

**__THE END__**
