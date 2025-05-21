# Data Aggregation

## Preliminary analysis/preparation of aggregation
### Matching Inspection Numbers Across Datasets
This step is important to get a better representation of the elevator data that is on the two data sets, so we assure that the predictions will be consitent. There might be missing data. Also, inspections without orders may represent errors in data entry or bad imports.

### Chronological Sorting of Datasets
This step will allow to process and create new features that depend on time. In this case the model will have ease to predict with more accurancy and prevent lekeage. 

### Combining Text Columns in Inspection Orders Dataset
This would simplify to process the text processing with LPN. Also reduces redundancy. 

### Addressing Missing "RISK SCORE" Values
Replaced missing values with median and then used scaler to normalize. This assures that the data is messured on the same scale. 

### Grouping Rare Categories in Inspection Outcome
Group all categories with fewer than 500 observations in the Inspection Outcome variable into an "Other" category.

### Standardizing the Inspection Type Variable
Clean and standardize the Inspection Type variable in the Inspection Dataset.

### Generating Dummy Variables for Inspection Dataset
Create binary/dummy variables for the Inspection Outcome and Inspection Type columns while retaining the original text information.


## Aggregation of the Inspection Dataset
### Group Data by Key Identifiers
Organize the Inspection Dataset by grouping inspections using key identifiers. Use the `groupby` function to group data based on attributes that uniquely define each inspection. Consider factors such as Inspection Number, Elevator ID, and Inspection Date to distinguish between inspections and identify historical inspections effectively.

### Aggregate Previous Inspections
For each Inspection Number, calculate the count of different Inspection Types and Inspection Outcomes that occurred for the same elevator in the past. Ensure that the aggregation of the "Inspection Outcome" variable excludes the current inspection. This step will help uncover patterns and trends relevant to the current inspection outcome.

### Format Data for Current Inspection Outcome
Separate the current inspection outcome (Y variable) into its own column, ensuring it is formatted as text. Include the current "Inspection Type" alongside the aggregated historical data. Be cautious of potential data leakage during this process.

### Filter Data Based on Inspection Order Dataset
After completing the aggregation, filter the dataset to retain only rows where the Inspection Number exists in the Inspection Order Dataset. This ensures alignment between the two datasets for further analysis.


# Machine Learning / Modeling
##  Modeling Part 1

### Determine the Baseline Score
Calculate the baseline score using a simple model or heuristic. For classification tasks, this could be the accuracy of always predicting the majority class. For regression tasks, use the mean or median of the target variable as the prediction and calculate the baseline metric (e.g., RMSE or MAE).

### Set Up a Machine Learning Pipeline
1. **Column Removal and Preprocessing**: Create a pipeline that removes unused columns and preprocesses the data as needed (e.g., encoding categorical variables, scaling numerical features).
2. **Train-Test Split**: Split the data into training and testing sets using `train_test_split` from `sklearn`.
3. **Model Testing**: Test several models, such as Logistic Regression, Random Forest, Gradient Boosting, and Support Vector Machines. Use cross-validation to evaluate model performance and compare results.

### Include a Feature Selection Step
1. **Add All Features**: Start by including all features in the model.
2. **Feature Selection**: Add a feature selection step to the pipeline using methods like Recursive Feature Elimination (RFE) or feature importance from tree-based models.
3. **Performance Comparison**: Compare the model's performance on the validation set before and after feature selection. Document the impact of feature selection on metrics such as accuracy, precision, recall, or RMSE.


## Feature Engineering

### Adding Historical Features to the Dataset
1. **Create Variables for Previous Months**:  
    Generate features that summarize inspection data from the previous 1, 3, and 6 months. For example:
    - Count of inspections conducted in the last X months.
    - Average "RISK SCORE" from inspections in the last X months.
    - Most frequent "Inspection Outcome" in the last X months.

2. **Develop Variables Based on the Last X Observations**:  
    Instead of aggregating all historical data, create features based on the last 3 or 5 inspections for each elevator. Examples include:
    - Count of specific "Inspection Types" in the last X inspections.
    - Proportion of "Pass" outcomes in the last X inspections.
    - Time gap between the current inspection and the most recent inspection.

3. **Document Performance Impact**:  
    Evaluate the impact of these new features on model performance:
    - Compare metrics such as accuracy, precision, recall, or RMSE on the validation set before and after adding these features.
    - Highlight any improvements or trade-offs observed in the model's predictive power.

4. **Feature Selection and Refinement**:  
    Use feature selection techniques to identify the most impactful historical features. Document how the inclusion of these features affects the final model's performance.
