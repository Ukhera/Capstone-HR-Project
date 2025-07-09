# Capstone-HR-Project using Python

## Overview
This project involves a comprehensive analysis of key factors influencing employee attrition using data-driven techniques and provide actionable insights that help organizations improve employee retention, enhance satisfaction, and optimize HR decision-making using Python.
## Objectives

- To explore and analyze employee data using Python 
- Identify the key factors contributing to employee attrition—such as satisfaction level, workload, and salary
- Find a co relation between salary and employee satisfaction
- Analyze if employees are overutilized leading to burnout
- To develop actionable recommendations that can help HR teams improve retention
- Recommendations to optimize staffing, and enhance employee satisfaction through data-driven decision-making.

 ## Dataset
The data for this project is sourced from the institute helping in getting certified for Data Science

## Schema
## Q1 : Load the dataset and display the first 10 rows. What are the key attributes of the dataset, and what do they represent?

## 🧠 Answer 1

## 🧠 Answer 1 – Load the Dataset

```python
# Import pandas
import pandas as pd

# Read the CSV file into a DataFrame
df = pd.read_csv("./data/HR_capstone_dataset.csv")

# To view the complete table

df.head()

##To Extract particular columns and row use iloc

df.iloc[9:20,0:3]
```
## 📊 Insights

This dataset provides a view from the perspective of Human Resources (HR). Key insights include:

- **Attrition Behavior Analysis**:
  - The attributes `satisfaction_level`, `last_evaluation`, and `left` can be useful in studying employee attrition.
  - For example, employees with lower satisfaction levels or high evaluation scores may show a higher tendency to leave.

- **Workload Correlation**:
  - Variables like `number_project`, `average_monthly_hours`, and `left` can help in understanding if increased workload is directly influencing employee exits.
  - An interrelationship between work pressure and attrition may become evident if a higher number of projects or long working hours correlate with the `left` column.

These insights can guide HR in making informed decisions about workload distribution and employee engagement to reduce attrition.

## 📌 Q2: Provide a summary of the dataset's structure

### 🔹 Code:

## 📌 Q2: Provide a summary of the dataset's structure

### 🔹 Code:

```python
# Get the number of rows and columns
df.shape

# Get a concise summary of the DataFrame
df.info()

# Get summary statistics for numerical columns
df.describe()
```

## 📌 Q3: List the unique values in the `Department` and `Salary` columns

### 🔹 Code:

```python
# Get unique values in the 'salary' and 'Department' columns
df['salary'].unique()
df['Department'].unique()

# Get number of unique entries in each column
df['salary'].nunique()
df['Department'].nunique()
```

## 📌 Q4: Are there any missing values in the dataset? If yes, how would you handle them?

### 🔹 Code:

```python
# Check for missing values in each column
df.isnull().sum()

How to Handle Missing Values (General Strategies):

df.dropna()
```
## 📌 Q5: Detect outliers in the `average_monthly_hours` column. What techniques would you use to handle these outliers?

### 🔹 Code (Boxplot Visualization):

```python
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris

plt.boxplot(df['average_montly_hours'], showmeans=True)
## To detect outliers in 'average_monthly_hours'
plt.title("Boxplot of Average Monthly Hours")
plt.xlabel("Average Monthly Hours")
plt.show()

## 📌 Q5 (continued): Visualize Outliers in All Numerical Columns

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Store column names
col = list(df.columns)
print(col)

# Loop through columns and plot boxplots for numerical ones
for i in df.columns:
    print(i)
    if df[i].dtype in ['float64', 'int64']:
        plt.figure(figsize=(6, 4))
        sns.boxplot(y=df[i])
        plt.title(f'Boxplot of {i}')
        plt.ylabel(i)
        plt.show()
    else:
        continue

## 📌 Boxplot to Detect Outliers in `average_monthly_hours`

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Plotting boxplot for 'average_monthly_hours'
plt.figure(figsize=(6, 4))
plt.boxplot(df['average_monthly_hours'], showmeans=True)
plt.title("Boxplot of Average Monthly Hours")
plt.xlabel("Average Monthly Hours")
plt.show()

```

## 📌 Q6: Convert non-numerical columns (e.g., `salary`) into numerical format using encoding

### 🔹 Code:

```python
import pandas as pd
from sklearn.preprocessing import LabelEncoder

# Strip any leading/trailing spaces in 'salary' column
df['salary'] = df['salary'].str.strip()

# Initialize the encoder
label_encoder = LabelEncoder()

# Apply Label Encoding to the 'salary' column
df['salary_encoded'] = label_encoder.fit_transform(df['salary'])

# Display unique categories before encoding
print(f"Unique salary levels before encoding: {df['salary'].unique()}")

# Display the data types
print(df.dtypes)

# Summary of the DataFrame after encoding
df.info()

```

## 📌 Q7: What is the proportion of employees who left the company versus those who stayed? Visualize the distribution.

### 🔹 Code (Bar Chart using Countplot):

```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(6, 4))
sns.countplot(x='left', data=df, palette='Set2')
plt.title("Distribution of Employees Who Left vs Stayed")
plt.xlabel("Employee Status")
plt.ylabel("Count")
plt.xticks([0, 1], ['Stayed', 'Left'])
plt.show()

# Count values of 'left' column
left_counts = df['left'].value_counts()

plt.figure(figsize=(6, 6))
left_counts.plot.pie(autopct='%1.1f%%', startangle=90, colors=['green', 'red'])
plt.title("Proportion of Employees Who Left vs Stayed")
plt.ylabel('')
plt.show()

🧠 Explanation:
The left column typically contains binary values:
0 = Employee stayed
1 = Employee left
sns.countplot() gives a quick bar chart showing the number of employees in each category.
plot.pie() provides a percentage view to better understand the proportion.
📊 Interpretation:

76% of employees stayed
24% of employees left
This analysis helps identify whether attrition is a significant issue and if further analysis is needed on causes (e.g., satisfaction, workload).

```

## 📌 Q8: How does employee satisfaction differ for employees who stayed versus those who left the company?

### 🔹 Code:

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Grouping data (optional, for inspection)
grouped_df = df.groupby('left')['satisfaction_level'].mean()
print(grouped_df)

# Boxplot for visual comparison
plt.figure(figsize=(8, 6))
sns.boxplot(x='left', y='satisfaction_level', data=df)

# Customize the plot
plt.title("Employee Satisfaction Level: Stayed vs Left")
plt.xlabel("Employee Status (0 = Stayed, 1 = Left)")
plt.ylabel("Satisfaction Level")
plt.xticks([0, 1], ['Stayed', 'Left'])
plt.show()

📊 Interpretation:
From the plot and group means:

Employees who left tend to have lower satisfaction levels
Those who stayed generally show a higher median satisfaction
This insight is critical for HR decision-making around employee engagement and retention strategies.

```

## 📌 Q9: Which department has the highest number of employees leaving the company?

### 🔹 Code:

```python
# Group by department and sum the 'left' column to count number of leavers
department_leave_counts = df.groupby('Department')['left'].sum()

# Department with the most leavers
most_leavers_department = department_leave_counts.idxmax()
max_leavers = department_leave_counts.max()

print(f"Department with highest attrition: {most_leavers_department} ({max_leavers} employees)")

📊 Interpretation:
Department with highest attrition: sales (1014 employees)

This insight helps identify which functional area is most affected by attrition, so HR teams can prioritize interventions there.

```

## 📌 Q10: Analyze the relationship between salary levels and employee attrition. What trends do you observe?

### 🔹 Code:

```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(8, 6))
sns.countplot(x='salary', hue='left', data=df, palette='Set2')

# Customize the plot
plt.title("Employee Attrition by Salary Level")
plt.xlabel("Salary Level")
plt.ylabel("Number of Employees")
plt.legend(title="Attrition", labels=['Stayed', 'Left'])
plt.show()

📊 Trends / Observations (Example):
From this plot, you might observe:

Low salary: Highest attrition — a large number of employees left.
Medium salary: Balanced — some stayed, some left.
High salary: Lowest attrition — most employees stayed.
These trends suggest that lower salary levels are correlated with higher attrition, which HR teams can address by reviewing compensation structures.

```

## 📌 Q11: Compute the correlation matrix for numerical columns and identify the strongest positive and negative correlations.

### 🔹 Code:

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Select only numerical columns
df_corr = df.select_dtypes(include=["number"])

# Compute correlation matrix
correlation_matrix = df_corr.corr()

# Plot heatmap
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".2f")
plt.title("Correlation Matrix")
plt.show()

🔍 Key Insights:
Strongest Positive Correlation:
Example: promotion_last_5years and satisfaction_level
→ Indicates that employees who were promoted tend to be more satisfied.
Strongest Negative Correlations:
number_project and satisfaction_level
→ Suggests that more projects may be associated with lower satisfaction.
average_monthly_hours and left
→ Employees working very high hours are more likely to leave.
```

## 📌 Q12: Based on your analysis, which features do you think are most important in predicting employee attrition? Justify your selection.

### 🔹 Answer:

Based on the exploratory analysis and correlation matrix, the most important features in predicting employee attrition are:

- **`satisfaction_level`**  
  - One of the strongest indicators — lower satisfaction levels are clearly linked with a higher probability of employees leaving.
  
- **`number_project`**  
  - Overburdened employees (too many projects) tend to show higher attrition, especially when not balanced with recognition or support.
  
- **`average_monthly_hours`**  
  - Higher average monthly working hours are associated with burnout and a greater likelihood of resignation.

### 🧠 Justification:

If an employee has:

- **High average monthly hours**
- **Low satisfaction level**
- **Low salary**

## 📌 Q13: Normalize or standardize numerical features such as `satisfaction_level` and `average_monthly_hours`. Explain why this step is important.

### 🔹 Code:

```python
import pandas as pd
from sklearn.preprocessing import StandardScaler

# Initialize the scaler
scaler = StandardScaler()

# Apply standardization to selected columns
scaled_features = scaler.fit_transform(df[['satisfaction_level', 'average_montly_hours']])

StandardScaler() standardizes features by removing the mean and scaling to unit variance.

```

## 📌 Q14: Create a flag for overutilized employees and analyze satisfaction & attrition

### 🔹 Code:

```python
# Create a flag: True if employee is working more than the 75th percentile
df['overutilized'] = df['average_montly_hours'] > df['average_montly_hours'].quantile(0.75)

# Compare satisfaction and attrition between overutilized and not
print(df.groupby('overutilized')[['satisfaction_level', 'left']].mean())

# Visualization
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(6, 4))
sns.boxplot(x='overutilized', y='satisfaction_level', data=df)
plt.title('Satisfaction vs Workload Level')
plt.xlabel('Overutilized (True = > 75th percentile)')
plt.ylabel('Satisfaction Level')
plt.show()

📊 Insight:
Employees who are overutilized (i.e., working more than the 75th percentile of monthly hours):

Have ~12% lower satisfaction
Show ~18% higher attrition rate
✅ This clearly shows a link between burnout and employee turnover.
✅ Employees with lower satisfaction are more likely to leave, emphasizing the need for workload balance.

```

---

### ✅ Q15: Final Recommendations Based on Insights

```markdown
## 📌 Q15: Based on your analysis, provide two recommendations to reduce employee attrition

### 🧠 Recommendation 1: Boost Employee Satisfaction Through Regular Engagement

- Our analysis found **satisfaction_level** to be one of the most critical predictors of attrition.
- Employees who left had significantly **lower satisfaction scores**.
- 🔁 **Action**: Conduct regular **feedback surveys**, initiate **one-on-one check-ins**, and ensure project roles are:
  - Aligned to employee strengths
  - Free from chronic overutilization and burnout

### 💰 Recommendation 2: Address Compensation Gaps

- Attrition was notably **higher among employees with lower salaries**.
- 🔁 **Action**: The company should:
  - Conduct **market research** to benchmark competitive salary levels
  - Perform **regular compensation reviews**
  - Ensure fair and transparent pay aligned with **industry standards**

These proactive steps can help **retain top talent**, reduce attrition, and improve overall organizational performance.

