# **Overview of the Water Quality Dataset**
The dataset contains measurements related to water quality and potability, with each row representing a water sample. The Potability column indicates whether the water is suitable for human consumption. The dataset includes various features such as pH, Hardness, Solids, Chloramines, Sulfate, Conductivity, Organic Carbon, Trihalomethanes, and Turbidity.

# **Role of Each Member**
1. Ochan Den-Mark Michael LOKIDORMOI - Data Loading and Preprocessing
2. Alhassan Alimamy Dumbuya - Vanilla Model Implementation
3. Sadick Mustapha Achuli - L1 regularization with/without earlystopping and comparison of RMSPOP and Adam and Error Analysis
4. Dimitri Kwihangana - L2 regularization with/without earlystopping and comaprison of RMSPOP and Adam and Dropout

# **Data Quality and Preprocessing**
In this project, we are using google colab where most of the data loading packages are being installed by default.
We will load the dataset using pandas library and perform initial exploratory data analysis to understand the dataset.

- The dataset contained missing values in several columns, notably in pH and Sulfate, which were addressed by
filling these gaps with the mean of their respective columns. This approach ensured that the dataset remained intact
without losing valuable information.
- Outliers were identified in the Solids feature through boxplots. However, they were retained to preserve data integrity,
  allowing the model to capture all potential patterns essential for accurate predictions.

# **Data Visualization**
In this section, we performed data visualization to understand the distribution of the features in the dataset.
We used `matplotlib` and `seaborn` libraries for data visualization as imported in the colab.

### **1. Correlation Heatmap:**
The heatmap generated using Seaborn provided a visual representation of the correlations between
various features in the dataset. 
Each feature's relationship with others was assessed, showing that no two or more variables were strongly correlated. 
This suggests that all features contribute unique information to the model, reducing the need for dimensionality reduction techniques.

![Screenshot 2024-10-04 170215](https://github.com/user-attachments/assets/8b6e9b9e-fb7c-4b52-bb1f-0e68023cf48e)

###**Feature Relationships**
The heatmap indicated moderate correlations among certain features, such as pH and Chloramines,
which can be important for understanding how these parameters interact in determining water potability.

### **2. Boxplot for Outlier Detection:**
Following the correlation analysis, boxplots were used to identify outliers in features like Solids.
The presence of outliers was acknowledged but retained to ensure the model captures all potential patterns that could influence predictions.

![Screenshot 2024-10-04 170239](https://github.com/user-attachments/assets/560049f1-5585-42ab-91a4-dd0816e1271f)

### **2. Scaling Features:**
Standardization was applied to the features to ensure they had a mean of 0 and a standard deviation of 1. 
This step is crucial for optimizing the performance 

