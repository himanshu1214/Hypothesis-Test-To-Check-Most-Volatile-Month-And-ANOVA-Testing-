#### Check Hypothesis Test to check the most volatile month is by chance or it is statistically significant.

#### ONE WAY ANOVA TESTING to compare the stock returns from Year 2014, 2015, 2016, 2017, 2018.

# Data:
	We will be using S&P500 stocks index from 2014 to 2018 data.

# Our Goal:
#### Construct Hypothesis Testing
####	Simulation over 1000 resampling to perform Hypothesis
####	Hypothesis Test to check the most volatile month is by chance or it is statistically significant and also check any other month having the similar extreme value as the one found by the analysis

# Wrangle Data:
#### Volatility of the stock returns is derived based on Annualised Monthly Volatility Rankings. (AMVR)

# Quick Look At the Data:
#### We are investing the S&P500 dataset from 2014-2017 i.e. 4 years. We extracted this data from Kaggle.com. We manipulated the date to satisfy our goals. We have 7 columns and 497472 rows in the dataset after manipulation. S&P 500 index consist of 505 company stocks. Below shows the quick glance of dataset.

# Cleaning:
#### We dropped the NaN’s values from the dataset.  


# Further:
#### We grouped the data by dates and aggregated the close as mean and created year, month column. Convert the raw unadjusted closing prices into daily % returns of S&P500 using .pct_change() method which basically takes (previous_close price – present_close_price)/previous_close_price.


## Final Annualised-Monthly Volatility Return (AMVR) values:

#### Finally rank all the months average are aggregated for all the years. Below data shows the final stock volatility over 12 months.


# Testing Hypothesis 1:
#### H0: S&P500 stock returns are highly volatile in January month
#### H1: S&P500 stocks returns are not volatile in January

# Testing Hypothesis 2:
#### H0: S&P stock returns volatility extreme as January month can occur in any other month
#### H1: S&P stocks returns volatility extreme as January month cannot occur in any other month.

# Below are the steps taken to conduct Hypothesis:
#### 1. Creating 1000 AMVR samples to test the Hypothesis
#### 2. Simulation using Resampling
#### Sampling the data and make the observed effect equally likely amongst all the labels and thus giving us a desired null set.
#### 3. For constructing null dataset i.e. with no seasonality, we removed the labels from dataset and create the random sample of 1007 using .sample method.
#### 4. Next we added an index using pd.bdate_range of equal length to the original data.
#### 5. Next we generated the same operations as we performed earlier on the original dataset.
#### 6. Further we appended the ‘new_df_sim’ dataframe by concatenating with empty dataset. We stored 1000 of such dataframes as columns.
#### 7. ‘Maxi_month’ takes the highest values from the ‘new_df_sim’ dataframe and append in ‘highest’ list.
#### 8. Absolute AMVR values are derived by subtracting the mean values after flattening the dataframe into one big array.
#### 9. Similar operation is performed on ‘highest’ list and absolute ‘abs_highest’ (AMVR) is derived.
#### 10. We did 1000 samples of 12 AMVR, permuting the data labels each time we build the samples.
#### 11. Test is like t-test or ANOVA as we are in the most extreme value, either above or below the mean.

# RESULTS:
#### We calculated p-value by counting how many values out of (12X1000 trials) are greater than January value. The p-value is 0.1105 which is more than 0.05 hence is not significant. Hence, we can reject Null Hypothesis.

# ANOVA TESTING:
#### After satisfying the assumptions required before using ANOVA, we applied ANOVA testing.



# Interpretation of Results:

#### Hence with high p-value we fail to reject Null Hypothesis that yearly return from 2014, 2016, 2017, 2018 are same. Hence group mean may be same.
#### Hence p > 0.05, we state that we have a main interaction effect. This simply identifies that between the group comparison identifies statistically significant differences.
#### Hence, we can also apply Tukey's Test to further validate our results.


# TUKEY’S TEST:

#### From the Tukey’s Test we validate our results from ANOVA that we reject that mean values from the group 2014, group 2015, group 2016 and group 2017 are not same.
