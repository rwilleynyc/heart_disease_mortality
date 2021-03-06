# Predicting Heart Disease Mortality in the United States
According data from the National Center for Health Statistics (NCHS), which is overseen by the Center for Disease Control (CDC), the leading cause of death in the United States is heart disease. Reliable reporting of this data for all states goes back to 1999, and the most recent public data available is from 2016.

<img src='/images/CDC-logo-nchs.gif'>

Naturally, public health organizations stand to benefit from this data if they can use it to accurately predict heart disease mortality rates in various states. Such a model would allow them to plan and appropriate resources in future years. Given the lag time in public reporting, this project aims to build a model that predicts heart disease mortality rates 3 years into the future. 

The project will culminate in an analysis of risks deemed to be high-risk in 2019.

## Data Sources
### Target Variable
The primary source of data for this objective comes from the [NCHS](https://data.cdc.gov/NCHS/NCHS-Leading-Causes-of-Death-United-States/bi63-dtpu). This dataset contains information for the top 10 leading causes of death, and was used to identify heart disease as the leading cause.

<img src='/images/leading_causes.png'>

The trend in heart disease mortality can be reviewed in the infographic below. Green represents the lowest observed mortality rate for a state since 1999, and red represents the highest rate. As can be seen, the heart disease mortality rate has been dropping overall over the 17 year period.

<img src='/images/HD_Trend.gif'>

Hypothesis tests were performed to confirm that:

- Heart disease mortality is significantly greater than cancer mortality
- Heart disease mortality was significantly lower in 2016 than in 1999

    <tr>
    <td> <img src='/images/hd_vs_cancer.png' alt="Drawing" style="width: 400px;"/> </td>
    <td> <img src='/images/hd_1999_vs_2016.png' alt="Drawing" style="width: 400px;"/> </td>
    </tr>

In both instances, the p-values were found to be less than 0.01%.

### Independent Variables
Based on qualitative research, the following were considered viable as initial variables for this analysis:

- **[Age & Gender](https://wonder.cdc.gov/Bridged-Race-v2017.HTML)**
- **[Alcohol Consumption](https://pubs.niaaa.nih.gov/publications/surveillance110/tab4-1_16.htm)**
- **[Smoking Rate](https://www.americashealthrankings.org/explore/annual/measure/Smoking/state/ALL)**

It is important to note here that because age itself is a factor, the mortality rate was calculated as number of deaths per capita rather than using the age-adjusted rates provided by the CDC.

## Cross-Sectional Regression Analysis
To get a sense of which variables have the strongest relationship with heart disease, a simple linear regression analysis was run for each variable on its own with the target variable. As can be seen below, the behavior that seems to have the greatest negative impact on heart disease mortality is wine consumption, while smoking has the greatest positive impact. From a demographic standpoint, males are less likely to die from heart disease than females, and the 75-59 age group is most susceptible to death from heart disease.

<img src='/images/leading_factors.png'>

## Time-Series
If the objective is to predict heart disease rates three years into the future, we cannot use same-year data to make predictions. For example, we can't use 2016 alcohol consumption rates to predict 2016 heart disease rates. Instead, we need to use 2011-2013 data to make a proper prediction. Therefore, 3-5 year time lags were created for each predictor variable, while data from years 0-2 were dropped from consideration in the analysis.

## Creating a Classification Target
Rather than trying to simply predict a precise rate, we want to classify a state as high-risk, medium-risk, or low-risk. For simplicity, the lowest 33% of all observed mortality rates was considered low-risk, with the highest 33% as high-risk. Though there may be more appropriate ways to devise a proper classification model, this discrepancy should not affect the integrity of the results, and appropriate adjustments can be made to the model rather simply.

## Machine Learning Models
Over 1,400 variations of 6 machine learning architectures were trained and tested in an effort to find the best one. The results for the top performing model of each type on testing data are displayed below.

<img src='/images/top_models.png'>

As can be seen above, a Support Vector Machine classifier was the top performing model, achieving an accuracy rate of 91.7% on test data. The accuracy measure of choice was the F1-Score.

## Results
In total, seven states were predicted to see a change in risk profile from 2016 to 2019, as shown in the infographic below.

<img src='/images/risk_delta.gif'>

Results are a bit mixed, with some states going up in risk, and others going down. Of greatest note is Oklahoma, which is predicted to drop from high-risk to low-risk in a matter of 3 years. Further research on this topic revealed a concerted effort on the part of state government to drastically reduce smoking rates through the **Certified Healthy Oklahoma Program.** The overall map for 2019 predictions is below.

<img src='/images/2019_map.png'>

As we can see, the high-risk states are clustered together in the mid-west region.

## Recommendations
Based on the results of this analysis, a few recommendations would be made to national health organizations and states for 2019 and beyond:

1. Reallocate some resources from Illinois and Oklahoma to states in higher risk categories. It would also be a good idea to begin moving some of those resources to Tennessee since it went from low-risk to medium-risk.
2. Run smoking awareness ad campaigns. As showcased by Oklahoma, targeting this one factor alone can make a huge difference.
3. Run general awareness campaigns targeting women and retirees.

These are just a few initial directions states and organizations can go, however it would also be a good idea for this analysis to be furthered in more narrow directions based on specific needs. For example, high risk states might want to take a deeper dive on the factors that contribute most to their risk-levels. This would allow for the development of more targeted, regional strategies. 

In addition, for states at the medium- and low-risk levels, as well as other organizations, they may prefer to hold off on taking action, opting to add more behavioral and socioeconomic features in the model to see if accuracy can be improved. This could also provide additional insight to what’s going on in those mid-west states. 

Finally, some states may face greater risks related to cancer. Those states could switch gears and perform a similar analysis on cancer. Given that heart disease seems to be continuing its downward trajectory (for the most part), it may be worth focusing on other causes of death that are potentially on the rise, and get ahead of them.