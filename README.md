# LAB

*MICHELA PIROZZI - 732531
FERIOLI SARA - 733105*

## LAB1 

You can find here the links of the datasets we used. We couldn't upload them in the Github repository as they are too big (even the zip file was too big).
https://www.dati.lombardia.it/Attivit-Produttive/Rapporti-di-lavoro-attivati/qbau-cyuc
https://www.dati.lombardia.it/Attivit-Produttive/Rapporti-di-lavoro-prorogati/chng-cman
https://www.dati.lombardia.it/Attivit-Produttive/Rapporti-di-lavoro-cessati/nwz3-p6vm

The datasets we used are on the various types of contracts for people living in Lombardy. In particular, we focused on the pre and post covid years (2018, 2019, 2020, 2021). 

1. Analysis with “Rapporti_di_lavoro_di_attivati.csv”

1.1 How has covid affected the types of activated contracts?
At this point, we analyzed the numbers of contracts activated in the various years, checking the trend of the main types of contract (extracted according to frequency).  
We noted that in the years 2018, 2019, 2020 and 2021, “Lavoro Domestico” has increased, while contracts for “Tirocinio” decreased. 

1.2 Which sectors have been most affected by covid? 
We have extracted the sectors most affected in the covid years, in terms of contracts activated in this period. Also in this case, we preferred to select some of the most present sectors within the dataset (to avoid visual problems in our graphs), always according to their occurrence.
What is noticeable is that the hotel (“Alberghi”) and catering (“Ristorazione con somministrazione”)  sector has decreased, while the “Attività di famiglie e convivenze come datori di lavoro per personale domestico”.
												
1.3 How are changed the work opportunities before and after covid? 
We only considered 2019 and 2021, in order to make a comparison between the values of the pre and post covid years.  
At this point, we have analyzed the different values of the types of contracts activated over the years, depending on the city. These values are shown in the first (map) and second graph.
Furthermore, in the third graph, we have considered the sectors (and not the provinces as in the previous graphs) in the years considered, noting a decrease in the numbers of active contracts in 2021, post covid. 

1.4 How covid has affected the active contract according to age and gender?
In this case, we split the covid years, into before and after, putting the values into two different DataFrames (datibefore and datiafter), then creating other DataFrames depending on the genre. These new 4 DataFrames were then used for the graphical representation. 
It is noticeable that male contracts are always greater than those of females, but that however in proportion to pre covid data, both gender categories have decreased. 

2. Analysis with “Rapporti_di_lavoro_di_prorogati.csv” + “Rapporti_di_lavoro_di_cessati.csv”

2.1 Comparison between extended and terminated contracts during covid.
We only considered the date and province of the company, for both the extended and terminated contracts datasets, and considered the post covid 2020 and 2021 years. 
After having created two datasets specifically for the two types of contracts ("selectedprorogati", "selectedcessati"), we have created a new DataFrame (“union”), which is the union of the two. 
This has been done in order to represent the data in the pie chart, where we can see the number of contracts extended is greater than those terminated, despite the end of covid and the removal of “Blocco dei licenziamenti”. For each of the categories of contract, one can also see the relationship between the various provinces.
In the second graph, considering 2018-2019-2020-2021, you can see that during the lockdown period, the number of both contract categories decreased dramatically. But as soon as the period ended (between the green lines), they increased again. 

3. Analysis with all 3 dataset

3.1 Which sectors have more or less active, extended or terminated contracts, during covid?
At this point, all three datasets were considered, to assess which sectors were most affected during the covid. To find our result, we used the max() and min() operators, applied on DataFrames divided by category (activated, extended, and terminated) and divided by year (activated20, activated21, extended20, etc.).

3.2 For the sectors of the previous point, what is the average age?
This point is related to the previous one, because we take the sectors with the highest values, and calculate the average age. We see that the average age for activated and extended contracts decreased in 2021, compared to 2020, but the average age for terminated contracts remained the same. 

Conclusion
In this project, we have analyzed how covid has influenced the employment relationships activated, extended and terminated in Lombardy, analyzing the number of contracts and sectors, employment opportunities according to age and province of the company. In various sectors there is a drastic decrease in the number of contracts, while in others there is growth, albeit minimal. 
In the lockdown period, the rule of layoffs was respected, which caused a decrease in terminated contracts. But this was only a delay, because then the curve rose again. 

## LAB2

In Lab21.ipynb.zip you can find the notebook zipped. 

In this lab, we analyzed and prepared the data, to be used in future methods. 
After extracting the macro categories for the economic sectors, we proceeded to Label Econcoding, using principally two methodologies:
  1. Label Encoder used on 'TITOLOSTUDIO', 'MODALITALAVORO', 'PROVINCIAIMPRESA', 'ITALIANO'. 
  2. Encoding Manually Ordinal Categorical Features used only on GENERE, because the column has two distinct values (M and F, transformed into 0 and 1).

To verify the normal distribution of the data (Gaussian Distribution), we have applied the Shapiro-Wilk Test, which makes the data non-Gaussian. For this reason, non-parametric stastical methods should be used in the future. 

Before starting with the PCA, we check the original feature correlation. As we can see from the matrix, the highest correlation is between the Codice_ateco (which is the category of the economy sector) and the gender (male or female): it means that the sector in which a person can work, depend if you are a man or woman. 

To reduce the number of columns, we found component1 and component2 via PCA and saw the correlation they have with all of our columns. Here, we can see some correlations:
  - component1 with 'ANNO' and 'modalitalavoro_transformed'
  - component2 with 'ETA' and 'nazionalita_transformed'

We found outliers, such as a contract activated in 2201 and an age of 221. 
In addition, we also removed all those contracts entered into with people younger than 15 years old, because this is not allowed in Italy. 

For the seasonality, we can observe that in the month of August (in all years), the count of activated contracts drops drastically, while in the months of September and October, with the resumption of all work, contracts increase.

We check the stationarity and we notice that the mean is increasing, so the series is not stationary. Test Statistic is higher than the Critical Values.

Verify Forecastability of a Time Serie: Approximated Entropy and Sample Entropy are calculated. 
For the Approximated Entropy, if the value is close to 0, then the data is more predictable and therefore observable. This is the case for years.
Otherwise, for the age, which has a value more distant from 0, we can say that it is not regular and predictable.

Descriptive analysis: In this section, we consider only indeterminate contracts and analyze how this type is distributed across industries. 

Group by features given: The idea is to consider non-modifiable features for each person (gender, age, and nationality) and to target an indeterminated contract. The result will be to get the best combination of all output features to get the contract.
The combination of age, gender and nationality which have the higest number of activated contract is a 30 years old man from Italy. 

## LAB3

### Creazione dataframe.ipynb 
This file is used to create the DataFrame 'transformed.csv' needed to be able to run 'LAB3.ipynb'. 
(Some parts refer to the second lab.)

We extract the macro categories for the economic sectors and also we decided to set only two macro categories for the type of contract, 
i.e., INDETERMINATO or NON-INDETERMINATO. Then we proceed to Label Econcoding, using principally two methodologies:
  * Label Encoder;
  * Encoding Manually Ordinal Categorical Features. 

We remove the outliers, for the features ETA and ANNO. 

We transformed the features we want to get as output, into a single new feature, called 'output'. 

*This notebook creates a new DataFrame, which will be downloaded with the name 'transformed.csv', and then loaded into the 'LAB3.ipynb' notebook.
We provide this new DataFrame by email, to speed up the execution of the 'LAB3.ipynb' notebook.*

### LAB3.ipynb

#### Goal

1. Given the features in the dataset, what is the best combination to have a new contract? Was the feature combination the same even before covid?

2. Predict number of contracts. Is the number of contracts predicted for the future in 2019 the same or similar to the actual data given the occurrence of COVID?

#### The code

As a first point, it is evaluated whether the DataFrame is balanced, according to the contract type. 
We note that it is not and therefore proceed with balancing by 'Random Undersampling'. We use undersampling instead of oversampling because we care more about the INDETERMINATO's contracts which have less occurencies, even if there are the possibilities to lose some informations.

We used the *'train_test_split'* method to split the dataset into train set (70%) and test set (30%). 

In order to solve the first goal, we needed a classification model, so we chose to use the Decision Tree and the K-Nearest Neighbors Classifiers. 

As for the Decision Tree, we implemented two different methods to identify the best parameters: 
 * Find the best max_depth
 * Best Depth Tree \n
The complexity of the Decision Tree is very high, so we implemented tree pruning to reduce or avoid overfitting.
This last part we were not able to execute because they took too long (we never got an output).

Regarding the second goal, we used several models, to determine which one is best for our dataset, through a section of Compare. 
The used models are:
 * ARIMA/SARIMAX
 * Holt winter
     * Simple exponential smoothing - ses
     * Double exponential smoothing - des
     * Triple exponential smoothing - tes
 * Extra trees regressor
 * Linear regression
 * Support Vector Regressor - svm
 
To compare the models, we use:
* MAE: Mean Absolute Error is the average over the verification sample of the absolute values of the differences between forecast and the corresponding observation.
* RMSE: Root Mean Squared Error is the square root of the mean of the square of all of the error.
* MAPE: Mean Absolute Percentage Error is a measure of prediction accuracy of a forecasting method in statistics.

As a last step, we selected only pre-COVID years (before 2019) and made the predictions on them, without the influence of the test set, then compared the result with what actually happened. 

As we can see in the graph, the COVID situation led to decrease in the number of contracts, compared to the prediction based on data through 2019.

## LAB4

Creazione presentazione jupyter slides
