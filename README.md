# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT
```
     

import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

Step 2 : Load the Dataset

data = pd.read_csv("titanic_dataset.csv")
print("\nDataset Loaded Successfully\n")
print(data.head())
print("\nDataset Info:\n")
print(data.info())
print(data.describe())

Step 3 : Data cleansing - Handling missing values

for column in data.columns:
    if pd.api.types.is_numeric_dtype(data[column]):
        data[column] = data[column].fillna(data[column].median())
    else:
        data[column] = data[column].fillna(data[column].mode()[0])
print("\nMissing values handled successfully.\n")

Step 4 : Box plot to analyse outliers (Age & Fare)

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Age"])
plt.title("Boxplot - Age")
plt.show()

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Fare"])
plt.title("Boxplot - Fare")
plt.show()

Step 5 : Remove outliers using IQR method

def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

data = remove_outliers_iqr(data, "Age")
data = remove_outliers_iqr(data, "Fare")

print("Outliers removed using IQR method.\n")

Step 6 : Countplot for categorical data

plt.figure(figsize=(6,4))
sns.countplot(x="Survived", data=data)
plt.title("Countplot - Survival Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="Sex", data=data)
plt.title("Countplot - Gender Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="Pclass", data=data)
plt.title("Countplot - Passenger Class Distribution")
plt.show()

Step 7 : Displot for univariate 

sns.displot(data["Age"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Age Distribution")
plt.show()

sns.displot(data["Fare"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Fare Distribution")
plt.show()

Step 8 : Cross tabulation

print("\nCross Tabulation: Sex vs Survived\n")
print(pd.crosstab(data["Sex"], data["Survived"]))

print("\nCross Tabulation: Pclass vs Survived\n")
print(pd.crosstab(data["Pclass"], data["Survived"]))

Step 9 : Heatmap for Correlation analysis

plt.figure(figsize=(8,6))
correlation_matrix = data.select_dtypes(include=np.number).corr()
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap - Titanic Dataset")
plt.show()

```
# Output
<img width="1037" height="361" alt="554075588-d68ab579-1360-4ea8-ac67-7c35330d43f7" src="https://github.com/user-attachments/assets/d5222ab6-87f5-467b-87fa-7ba32609e7ea" />
<img width="949" height="831" alt="554075670-8e805d2a-fa8c-4933-9600-821c3775ee9b" src="https://github.com/user-attachments/assets/9341f82c-eeb9-4050-b35e-087bd60d69f8" />
<img width="802" height="210" alt="554075808-a005cc04-ba54-49a1-91c3-1fd516940601" src="https://github.com/user-attachments/assets/01b189ec-c8a0-4652-a2f5-c60bcd6ab17f" />
<img width="903" height="348" alt="554076020-7436abd2-3121-4912-a1bb-1ee8c1562923" src="https://github.com/user-attachments/assets/bcb9bdc1-66c6-4504-abf2-700d158244f1" />
<img width="800" height="852" alt="554076118-3ef021b6-eb10-4dfc-ba5e-f25286f38b9f" src="https://github.com/user-attachments/assets/318a9fd9-6eb4-4f55-8a67-db94d24d1442" />
<img width="644" height="535" alt="554076216-233b0691-8247-4279-ba43-93cf59664015" src="https://github.com/user-attachments/assets/cb2431b5-4865-4c59-9200-3967d2f5a3bf" />
<img width="644" height="535" alt="554076341-b91aac68-f838-4742-839c-41047808819e" src="https://github.com/user-attachments/assets/f97742e8-fe1a-4ab6-a5ac-9836122841a8" />
<img width="803" height="459" alt="554076429-25eba6c1-b23e-41df-815b-a36c5002682a" src="https://github.com/user-attachments/assets/6fb017b8-66fe-4861-99fe-25a33e957dac" />
<img width="723" height="525" alt="554076533-7ad03409-f4b7-47de-a879-1569b45ac727" src="https://github.com/user-attachments/assets/e3b6e4e7-651b-4a40-9599-35b1fb2a18bf" />
<img width="699" height="517" alt="554076600-a4132a90-0e71-4015-9ce1-db15fb14aee5" src="https://github.com/user-attachments/assets/7cde7a69-ab0b-485d-ab38-0d105b59272a" />
<img width="718" height="524" alt="554076692-bf507710-28d4-4b7d-a95b-602481e422ae" src="https://github.com/user-attachments/assets/3909d85d-e83f-4fd8-a4db-ff529baef109" />
<img width="876" height="841" alt="554076765-09066b41-2aa1-4c92-a757-7a7b233b9e4f" src="https://github.com/user-attachments/assets/f9645527-1efd-4e7f-b3d0-865062ae5d19" />
<img width="773" height="554" alt="554076829-d26bb775-11a0-4461-bc9c-127b7c555e26" src="https://github.com/user-attachments/assets/11cfa439-e4bc-40ef-a2dc-e14178c54339" />
<img width="571" height="631" alt="554076885-f1bb3ead-cccb-461b-8f2e-705d9d5a747b" src="https://github.com/user-attachments/assets/408e1eac-fe8c-4862-9199-17f99557a6c7" />
<img width="571" height="631" alt="554076939-f266ef40-b5c6-470b-a69c-bb151d9bd4bc" src="https://github.com/user-attachments/assets/8a7c5501-1763-4a5e-8b82-211e85a3f489" />
<img width="918" height="771" alt="554076987-cc60ed80-2cf3-4ce8-a82a-adfbb4089a1c" src="https://github.com/user-attachments/assets/d666efc2-efe4-4cbf-b5d0-502536619bc6" />



# RESULT
    Thus , the EDA Analysis using Python is completed successfully
