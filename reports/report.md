# Data Aggregation

### Matching Inspection Numbers Across Datasets
To improve the consistency of predictions, this step focuses on obtaining a better representation of the elevator data from the two datasets. This includes addressing potential missing data. Additionally, inspections without associated orders may indicate data entry errors or import issues.

### Chronological Sorting of Datasets
This step enables the processing and creation of time-dependent features, enhancing the model's predictive accuracy and preventing leakage.

### Combining Text Columns in Inspection Orders Dataset
Simplifying text processing with LPN would reduce redundancy.

### Addressing Missing "RISK SCORE" Values
Missing values were imputed using the median, and subsequently, a scaler was applied for normalization. This process ensures that all data is measured on a consistent scale.

### Grouping Rare Categories in Inspection Outcome
Improved readability and model efficiency can be achieved by grouping smaller categories. While individually these categories might not significantly impact the overall analysis, their combined effect will provide a more comprehensive understanding.

### Standardizing the Inspection Type Variable
Standardize and clean the 'Inspection Type' variable within the Inspection Dataset.


## Aggregation of the Inspection Dataset
### Group Data by Key Identifiers & Aggregate Previous Inspections
On this step the data is grouped by Elevator Id, then the Inpection Number is grouped as a list (because can have many), then also regrouped dates: The earliest as the min and the latest as the max. 

### Format Data for Current Inspection Outcome
As we want to assure that the Elevator Id is associated with an Inspection we can't arbitrarily keep an unique id. Thus, we can keep the id and create a list with the Inspection Numbers to do the validation. Like this we guarantee that: only contains rows with valid (matched inspections), rows from final_df where the "Inspection_Number" exists in the Inspection Orders dataset (sorted_inspections_order).

### Filter Data Based on Inspection Order Dataset
To improve data quality for prediction, it's crucial to eliminate duplicate entries and retain only the elevator data present in existing orders. Other elevator data is not required for this purpose.


# Machine Learning / Modeling
##  Modeling Part 1

### Determine the Baseline Score
Calculate the baseline score using a simple model or heuristic. For classification tasks, this could be the accuracy of always predicting the majority class. For regression tasks, use the mean or median of the target variable as the prediction and calculate the baseline metric (e.g., RMSE or MAE).

### Set Up a Machine Learning Pipeline
1. **Column Removal and Preprocessing**: Create a pipeline that removes unused columns and preprocesses the data as needed (e.g., encoding categorical variables, scaling numerical features).
2. **Train-Test Split**: Split the data into training and testing sets using `train_test_split` from `sklearn`.
3. **Model Testing**: Test several models, such as Logistic Regression, Random Forest, Gradient Boosting, and Support Vector Machines. Use cross-validation to evaluate model performance and compare results.

### Include a Feature Selection Step
1. **Add All Features**: 
Start by including all features in the model.
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
