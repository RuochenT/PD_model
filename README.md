# The probability of default model 
## Variable selection 
1. Relevance: should relate to the default risk.
2. Data quality and availability: complete and reliable.
3. Independence between variables: avoid multicollinearity.  
4.Interpretability: variables should have a clear economic and financial interpretation.
5. Predictive power: should have significant association with default variable. Assess by using chi-square, pearson coefficient, information value.

## Example of Varaibles 
**General client information**: Sector/industry, years in business, ownership type.

**Credit history**: credit utilization, outstanding debt, length of credit history, past defaults.
Financial health, Debt Service Coverage Ratio (DSCR), Capital Gearing Ratio, debt-to-asset ratio, quick ratio.
Credit product

**Loan characteristics**: loan amount, type of loan, collateral type, repayment terms, the interest rate, Loan-to-Value (LTV) ratio.
External data, GDP growth rate, Credit ratings (S&P Global Ratings, Moody’s, DBRS Ratings Limited).

## Target Variable: default variable
Encode categorical variable by using label encoding as 1 for default and 0 for not default. 

## Variable Transformation
1. Fine classing: applied to continuous and discrete with high cardinality.
2. Coarse classing: we optimize number of the bins based on Weight of Evidence (WoE)  and number of observation for each category.
3. Dummy coding: A technique used to represent categorical variables in a binary format. We create dummy variables for all coarse classes except the reference class.

## Important Model Features (why logistic regression?)
1. Interpretable: not a black box model and being able to explain the relationship.
2. Compliance with regulatory requirements: Basel III IRB approach, IFRS 9, the Committee of European Banking Supervisors (CEBS).
3. Probability models: should provide probability  of default directly. 
4. Accurate and stable results: high predictive accuracy and stable predictions.
5. Scalability and efficiency: handle large volumes & able to do real-time predictions.

## Model Validation 
Discrimination: ability to separate defaulters and non-defaulters.
1. Gini curve (Gini coefficient) 
2. Receiver Operating Characteristic (ROC curve)
3. Brier score 

Calibration: ability to make unbiased estimates of the outcome ( the accuracy of the estimated PD).
1. Binomial test
2. Chi-square statistics 

## Challenges of the Probability of Default Model
1. Model monitoring: The data should be representative as required by the Basel III accord. However, the values change over time (e.g., income). We can use the population stability index (PSI) to check if the previous data still represents the new data. If not, retrain the model with the new data.
2. Data imbalance: The number of defaults is much smaller and can pose a bias to the model, especially in the false negative class (predicted as non-default but actually default). Use SMOTE to oversample minority class.


## References 
				
Basel Committee on Banking Supervision (2005, February). Working paper no. 14: Studies on the validation of internal ratings systems. 
Basel Committee on Banking Supervision (2020, March). IRB approach: minimum requirements to use IRB approach 
Medema, L., Koning, R.H., & Lensink, R. (2009). A Practical Approach to Validating a PD Model. Journal of Banking and Finance, 33, 701-708.






