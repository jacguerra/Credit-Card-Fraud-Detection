# Credit-Card-Fraud-Detection
1.	Executive Summary
   
The aim of this project was to precisely detect fraudulent credit card transactions with the purpose of reducing the financial risk associated with fraud and maximizing savings. To identify fraudulent transactions, a machine learning model was trained and tested on the dataset and assessed for accuracy based on previously identified frauds. The final model will eliminate 56.42% of fraud by rejecting only 3% of transactions, resulting in $21,000,000 in savings per year. Ultimately this model can be used to reject the fewest amount of credit card transactions possible while still optimizing for savings. 

3.	Description of Data
   
The data was composed of company credit card transactions from a US government organization. The dataset had 10 fields, 96,753 records and covered the year 2010. Of the fields, 2 were numerical and 8 were categorical.

4.	Variable Creation
   
During the variable creation step, a total of 1,383 variables were created. This included two Benford’s Law variables, which measured the unusualness of the first digit of the Merchnumber and Cardnumber fields. Amount variables calculated the average, max, median and total amount spent for each entity over a particular time period, and an Amount Bin variable was also created to group the transaction amounts into 5 bins to make the amount field more useful for analysis.

Two new variables were also created to test theories about credit card transaction fraud. A Gas Station variable indicated whether a transaction took place at a gas station, which is the most common location for credit card transaction fraud. A New Purchase Location variable was also created that indicated if the next purchase made on the same Cardnumber was in a different Zip Code or State, which could track stolen cards taken to a different location.

5.	Feature Selection
   
A univariate KS filter was first used to rank the variables by importance in predicting the y variable, Fraud, and reduce the number of variables to 300. Multiple wrappers were tested, including LGBM and Random Forest with both forward and backward selection methods. Ultimately, an LGBM wrapper utilizing forward selection had the most consistent performance and was chosen to generate a finalized list of 20 variables that achieved a peak performance of 0.69 FDR. The performance of the LGBM forward selection wrapper (Filter Number = 300, Wrapper Number = 30) and the list of the final 20 variables ranked in wrapper order are below.

6.	Preliminary Model Exploration
   
Using the finalized list of variables from the wrapper, many different models were run to identify the one with optimal performance. The chart below displays each type of model that was run and their output. All models were run separately on the training set, the test set and the OOT set. For each output, the model was run 5 times and the performance across each run was averaged to give a singular FDR score.
 
The simplest model, Logistic Regression, was run first to get a baseline performance to compare the nonlinear models to. For all models, the hyperparameters were tuned to optimize performance. A summary of the performance of each model can be found below as well as a visualization of the training, testing and OOT performance for each of the top performing models of each type.

![image](https://github.com/jacguerra/Credit-Card-Fraud-Detection/assets/113937618/c11ee3c8-c310-44ba-970b-b75ebaf3cdda)

7.	Final Model Performance
   
The final selected model was a Random Forest model with the following parameters: 10 Variables, 100 Estimators, Gini Criterion, No Max Depth, 1,000 Minimum Sample Split, 20 Minimum Sample Leaf and 8 Max Features. At 3% this model had the following FDRs for each set: 73.52% Training, 72.60% Testing, and 56.42% OOT. The 56.42% FDR for the OOT set was the highest achieved of all the models and indicates that rejecting only 3% of transactions will eliminate 56.42% of fraud.

9.	Financial Curve & Recommended Cutoff
    
The graph below represents the potential savings by score cutoff. A score cutoff of 3% has been chosen, represented by the black line in the graph below. This cutoff was chosen because it denies the fewest amount of credit card transactions possible while still leading to strong overall savings. It is far left enough to capture the peak savings and far right enough to capture the sharpest fraud increase. Overall, a 3% cutoff will lead to approximately $21,000,000 in savings per year.

![image](https://github.com/jacguerra/Credit-Card-Fraud-Detection/assets/113937618/b76a92d2-9580-46f4-bf1f-94758d34f660)


