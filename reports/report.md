# Data Aggregation

## Preliminary analysis/preparation of aggregation
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


## Aggregation of the Inspection Dataset
### Group Data by Key Identifiers
Organize the Inspection Dataset by grouping inspections using key identifiers. Use the `groupby` function to group data based on attributes that uniquely define each inspection. Consider factors such as Inspection Number, Elevator ID, and Inspection Date to distinguish between inspections and identify historical inspections effectively.

### Aggregate Previous Inspections
For each Inspection Number, calculate the count of different Inspection Types and Inspection Outcomes that occurred for the same elevator in the past. Ensure that the aggregation of the "Inspection Outcome" variable excludes the current inspection. This step will help uncover patterns and trends relevant to the current inspection outcome.

### Format Data for Current Inspection Outcome
Separate the current inspection outcome (Y variable) into its own column, ensuring it is formatted as text. Include the current "Inspection Type" alongside the aggregated historical data. Be cautious of potential data leakage during this process.

### Filter Data Based on Inspection Order Dataset
After completing the aggregation, filter the dataset to retain only rows where the Inspection Number exists in the Inspection Order Dataset. This ensures alignment between the two datasets for further analysis.
