# **Overview of the Water Quality Dataset**
The dataset contains measurements related to water quality and potability, with each row representing a water sample. The Potability column indicates whether the water is suitable for human consumption. The dataset includes various features such as pH, Hardness, Solids, Chloramines, Sulfate, Conductivity, Organic Carbon, Trihalomethanes, and Turbidity.

# **Data Loading and Initial Exploration**
In this project, we are using google colab where most of the data loading packages are being installed by default.
We will load the dataset using pandas library and perform initial exploratory data analysis to understand the dataset.

### **1. Loading the data**
The data is loaded using `pandas` and the dataset is mounted from the drive as shown in the code below
```python
import pandas as pd
data = '/content/drive/MyDrive/water_potability.csv'
df = pd.read_csv(data)
```
### **2. Exploring the Data:**
In data exploration, we first need to know our data by checking the content in it.
So, the first few rows of the dataset can be viewed using:
```python
df.head()
```
### **3. Checking Data Shape and Info:**
In order to fully understand our data, we check the `shape` and `info` of the DataFrame to understand its structure using the the print commands below:
```python
print(df.shape)  **# Output: (3276, 10) as in the notebook**
print(df.info())
```
### **4. Handling Missing Values:**
We check for missing values in the dataset using the `isnull()` function and then drop any rows or fill it depending on the data size.
In this case, we filled the Missing values in the dataset with the mean of their respective columns using the command below:
```python
df.fillna(df.mean(), inplace=True)
```
### **5. Checking for Missing Values:**
After filling missing values, it's good practice to verify that there are no remaining NaN values in your data.
We can do this by using the `isnull().sum()` function as shown below:
```python
print(df.isnull().sum())
```
# **Data Visualization**
In this section, we will perform data visualization to understand the distribution of the features in the dataset.
We will use `matplotlib` and `seaborn` libraries for data visualization as imported in the colab.

### **1. Correlation Heatmap:**
A heatmap is used to check for correlations between variables. 
No strong correlations were found, so no dimensionality reduction techniques to be applied.

![Screenshot 2024-10-04 170215](https://github.com/user-attachments/assets/8b6e9b9e-fb7c-4b52-bb1f-0e68023cf48e)

### **2. Boxplot for Outlier Detection:**
We use boxplot to detect outliers in the dataset. The boxplot is used to visualize the distribution.
Despite the outliers being found int the `**"Solid columns"**`, standardization is applied to scale the features.

![Screenshot 2024-10-04 170239](https://github.com/user-attachments/assets/560049f1-5585-42ab-91a4-dd0816e1271f)

# **Data Preparation for Modeling**
### **1. Separating Features and Target Variable:**
We separate the `features(X)` from the target `variable(y)` using the following commands:
```python
 X = df.drop('Potability', axis=1)
 y = df['Potability']
```
### **2. Scaling Features:**
The StandardScaler from sklearn is used to scale the features, ensuring that all variables have a mean of `0` and standard deviation of `1`. The scaled features are stored in a new DataFrame as shown below:
```python
 scaler = StandardScaler()
 X_scaled = scaler.fit_transform(X)
```
## Create a new DataFrame with scaled features
```python
X_scaled_df = pd.DataFrame(X_scaled, columns=X.columns)
print(X_scaled_df.head())
```
