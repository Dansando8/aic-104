# Data Aggregation

## 
### Matching Inspection Numbers Across Datasets
Verify whether each Inspection Number in the Inspection Dataset is also present in the Inspection Order Dataset to ensure every inspection has associated orders.

### Chronological Sorting of Datasets
Sort both datasets chronologically using Earliest_INSPECTION_Date for the Inspection Dataset and DateofIssue for the Inspection Order Dataset.

### Combining Text Columns in Inspection Orders Dataset
Create a new column by combining the text from the "DIRECTIVE" and "Inspections additional information" columns.

### Addressing Missing "RISK SCORE" Values
Identify missing "RISK SCORE" values in the Inspection Orders dataset and propose a solution based on quantitative analysis with justification.

### Grouping Rare Categories in Inspection Outcome
Group all categories with fewer than 500 observations in the Inspection Outcome variable into an "Other" category.

### Standardizing the Inspection Type Variable
Clean and standardize the Inspection Type variable in the Inspection Dataset.

### Generating Dummy Variables for Inspection Dataset
Create binary/dummy variables for the Inspection Outcome and Inspection Type columns while retaining the original text information.