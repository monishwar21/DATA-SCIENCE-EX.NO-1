#EX.NO:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

# Step 1: Import Required Libraries
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt

# Step 2: Read the Dataset
# Replace with your actual CSV file
df = pd.read_csv('Data_set.csv')
df.head()

# Step 3: Dataset Information
df.info()
df.describe()

# Step 4: Handling Missing Values
# Check Null Values
df.isnull()
df.isnull().sum()

# Fill Missing Values with 0
df1_fill_0 = df.fillna(0)
df1_fill_0

# Forward Fill
df1_ffill = df.ffill()
df1_ffill

# Backward Fill
df1_bfill = df.bfill()
df1_bfill

# Fill with Mean (Numerical Column Example)
df['rating']=df['rating'].fillna(df['rating'].mean())
df['watchers']=df['watchers'].fillna(df['watchers'].mean())
df

# Drop Missing Values
df1_dropna = df.dropna()
df1_dropna

# Step 5: Save Cleaned Data
df1_dropna.to_csv('Data_set1.csv', index=False)

# OUTLIER DETECTION
# Step 6: IQR Method (Using Dataset)
df1 = pd.read_csv('Data_set.csv')

# Boxplot for Outlier Detection
sns.boxplot(x=df1['watchers'])
plt.show()

# Calculate IQR
Q1 = df['watchers'].quantile(0.25)
Q3 = df['watchers'].quantile(0.75)
IQR = Q3-Q1
print("IQR:", IQR)

# Detect Outliers
outliers = df[
(df['watchers'] < (Q1-1.5 * IQR)) |
(df['watchers'] > (Q3 + 1.5 * IQR))
]
outliers

# Remove Outliers
df1_cleaned = df[
~((df['watchers'] < (Q1-1.5 * IQR)) |
(df['watchers'] > (Q3 + 1.5 * IQR)))
]
df1_cleaned

data = [1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,
54,57,60,63,66,69,72,75,78,81,84,87,90,93]
df_z = pd.DataFrame(data, columns=['values'])
df_z

# Calculate Z-Scores
z_scores = np.abs(stats.zscore(df_z))
z_scores

threshold=3
mask = np.zeros(len(df), dtype=bool)
mask[df['rating'].dropna().index] = z_score > threshold
outliers = df[mask]
print('outliers')
print(outliers)

df_z_cleaned = df_z[z_scores <= threshold]
df_z_cleaned

# output
<img width="1004" height="821" alt="Screenshot 2026-03-22 173007" src="https://github.com/user-attachments/assets/bd1ce1c1-7ad3-4f5b-b71e-0dc58e47def6" />

<img width="643" height="508" alt="Screenshot 2026-03-22 173030" src="https://github.com/user-attachments/assets/569cd16f-92ff-4e00-b17f-5d028ca1dd02" />
<img width="487" height="733" alt="Screenshot 2026-03-22 173045" src="https://github.com/user-attachments/assets/763c6302-5ec6-4cd1-bc39-2c07e55d1163" />

# Result
          <<include your Result here>>
 The given data has been cleaned.
