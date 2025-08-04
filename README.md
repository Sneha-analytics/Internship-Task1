# Internship-Task1 Desription
## Task 1 - Data Cleaning Steps
This project involves cleaning and preprocessing the **Medical Appointment No-Shows** dataset using both **Excel** and **Python (Pandas)**.


### In Excel:
- **Renamed Columns**: Cleaned and simplified column headers
- **Deleted Unnamed Columns**: Removed unnecessary blank columns
- **Saved Cleaned Excel File**
  
---
### In Python (Pandas):

```python
import pandas as pd

# Load data
df = pd.read_csv('medical_data.csv')

# Rename columns to clean format
df.columns = df.columns.str.strip().str.lower().str.replace('-', '_').str.replace(' ', '_')

# Standardize text columns
df['gender'] = df['gender'].str.upper()
df['no_show'] = df['no_show'].str.upper()
df['neighbourhood'] = df['neighbourhood'].str.upper()

# Convert date columns to datetime
df['scheduled_day'] = pd.to_datetime(df['scheduled_day']).dt.date
df['appointment_day'] = pd.to_datetime(df['appointment_day']).dt.date

# Remove rows with invalid age
df = df[df['age'] >= 0]
df['age']=df['age'].apply(lambda x: np.nan if x<=0 else x)

# Drop duplicate rows
df.drop_duplicates(inplace=True)

# Save cleaned data
df.to_csv('cleaned_medical_data.csv', index=False)
