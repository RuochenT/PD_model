# The probability of default model 
## Data 
the data includes all loans issued from 2007 - 2015. The file is a matrix of 890,000 observations and 75 variables which I cannot include the file in here. 
please follow this link for data set https://www.dropbox.com/s/tq3xz0piqitnc59/loan_data_2007_2014.csv?dl=0 

## Variable selection 
1. Relevance: should relate to the default risk.
2. Data quality and availability: complete and reliable.
3. Independence between variables: avoid multicollinearity.  
4. Interpretability: variables should have a clear economic and financial interpretation.
5. Predictive power: should have significant association with default variable. Assess by using chi-square, pearson coefficient, information value.



## Variable Transformation
1. Fine classing: applied to continuous and discrete with high cardinality.
2. Coarse classing: we optimize number of the bins based on Weight of Evidence (WoE)  and number of observation for each category.
3. Dummy coding: A technique used to represent categorical variables in a binary format. We create dummy variables for all coarse classes except the reference class.

## Data preparation summary 
1. Encode dependent variable as 1 and 0 (Charged Off', 'Default', 'Does not meet the credit policy. Status:Charged Off’, 'Late (31-120 days)'.
2. Split the data train-test get input and target for both data frame.
3. Discrete <20: Coarse classing on discrete variables which have few distinct values based on WoE and number of observations in each group. (if WoE high > there is bad more than good, relate to default more).
4. We make a reference category the category with lowest weight of evidence.
5. Continuous (month since issue,income) or discrete> 20:
- Fine classing by roughly grouping the values into categories/intervals (pd.cut), 2.) Coarse classing by combining some initial fine classing categories into bigger ones based on woe and number of obs for each category (similar woe, varies woe but small obs, high obs).
6. When we plot woe and see if there is no pattern between variable and woe, then there is no relation between them. We drop the variable.
7. If there are missing values, we can create one dummy variable for missing value. 

## Important Model Features (why logistic regression?)
1. Interpretable: not a black box model and being able to explain the relationship.
2. Compliance with regulatory requirements: Basel III IRB approach, IFRS 9, the Committee of European Banking Supervisors (CEBS).
3. Probability models: should provide probability  of default directly. 
4. Accurate and stable results: high predictive accuracy and stable predictions.
5. Scalability and efficiency: handle large volumes & able to do real-time predictions.

## Model Validation 
In a statistical framework we face two possible kinds of errors: A Type I error, which indicates low default risk when in fact the risk is high, and a Type II error, which conversely indicates high default risk when in fact risk is low. From a supervisory viewpoint, Type I error is more problematic, as it produces higher costs. (The model predicted no default and the borrower defaulted — False Negative).

Discrimination: determine the power of discrimination that a model exhibits in warning of default risk over a given horizon.
1. Gini curve (Gini coefficient) 
2. Receiver Operating Characteristic (ROC curve)
3. Brier score

Calibration: ability to make unbiased estimates of the outcome ( the accuracy of the estimated PD).
1. Binomial test
2. Chi-square statistics 

## Gini coefficient 

- we focus on Gini coefficient which is used to measure the inequality between non defaulted and defaulted in a population.
- It is a plot of cumulative percentage of all borrowers on the X axis and the cumulative percentage of bad borrowers on the Y axis.
- The Gini coefficient is a ratio that represents how close our model to be a “perfect model” and how far it is from being a “random model.” Thus, a
“perfect model” would get a Gini coefficient of 1, and a “random model” would get a Gini coefficient of 0.
- Our gini coefficient is 40.32% (AUROC * 2 - 1). It suggests that, on average, the default rates are relatively evenly distributed across two groups of borrowers.

## Challenges of the Probability of Default Model
1. Model monitoring: The data should be representative as required by the Basel III accord. However, the values change over time (e.g., income). We can use the population stability index (PSI) to check if the previous data still represents the new data. If not, retrain the model with the new data.
2. Data imbalance: The number of defaults is much smaller and can pose a bias to the model, especially in the false negative class (predicted as non-default but actually default). Use SMOTE to oversample minority class.

## Apply the model to decision making
- Scorecard: The PD model must be easy to understand and interpret since it will trasform into a scorecard tool. The scorecard is used to process an individual credit worthiness assessment that direactly corresponds to a specific probability of default. In order to turn it into a tool, we need to turn the coefficient from the model into simple scores. In this case, we turn specify the minimum 300 and the maximum 850. Then, we rescale the credit worthiness from our model into desired scores. You can read more about the detail here https://altair.com/newsroom/articles/credit-scoring-series-part-five-credit-scorecard-development

- Setting cutoffs: The cutoff rate is being used for taking a decision on whether to approve a loan application or not.If we set a given probability of default as a cutoff, all borrowers with a lower probability of default than the cutoff will be granted a loan. Naturally, there is a trade off between the two. If we want to grant more loans, we will be inevitably accepting lower quality borrowers. The other side of the coin is that if we only approve the most creditworthy borrowers, we will end up with very few loans. The cutoff point is decided based on those two factors how many borrowers would be accepted and rejected, and what would the credit worthiness of the accepted borrowers be? If a bank wants more business, it will set a lower cutoff in terms of credit worthiness or probability of non default. And if the bank wants to lend to fewer borrowers with higher credit worthiness, it will set a higher cutoff point in terms of probability of non default.

## References 
				
Basel Committee on Banking Supervision (2005, February). Working paper no. 14: Studies on the validation of internal ratings systems.

Basel Committee on Banking Supervision (2020, March). IRB approach: minimum requirements to use IRB approach. 

Medema, L., Koning, R.H., & Lensink, R. (2009). A Practical Approach to Validating a PD Model. Journal of Banking and Finance, 33, 701-708.






