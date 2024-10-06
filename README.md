# **Overview of the Water Quality Dataset**
The dataset contains measurements related to water quality and potability, with each row representing a water sample. The Potability column indicates whether the water is suitable for human consumption. The dataset includes various features such as pH, Hardness, Solids, Chloramines, Sulfate, Conductivity, Organic Carbon, Trihalomethanes, and Turbidity.

### **Role of Each Member**
1. Ochan Den-Mark Michael LOKIDORMOI - Data Loading and Preprocessing
2. Alhassan Alimamy Dumbuya - Vanilla Model Implementation
3. Sadick Mustapha Achuli - L1 regularization with/without earlystopping and comparison of RMSPOP and Adam and Error Analysis and Model Evaluation
4. Dimitri Kwihangana - L2 regularization with/without earlystopping and comaprison of RMSPOP and Adam and Dropout

### **Link to presentation** 
https://www.canva.com/design/DAGSzbkqbQo/fIetJvLpyBLdbglpMISeFA/edit?utm_content=DAGSzbkqbQo&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton

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

### **Feature Relationships**
The heatmap indicated moderate correlations among certain features, such as pH and Chloramines,
which can be important for understanding how these parameters interact in determining water potability.

### **2. Boxplot for Outlier Detection:**
Following the correlation analysis, boxplots were used to identify outliers in features like Solids.
The presence of outliers was acknowledged but retained to ensure the model captures all potential patterns that could influence predictions.

![Screenshot 2024-10-04 170239](https://github.com/user-attachments/assets/560049f1-5585-42ab-91a4-dd0816e1271f)

### **Scaling Features:**
Standardization was applied to the features to ensure they had a mean of 0 and a standard deviation of 1. 
This step is crucial for optimizing the performance 

###  **First Model: Vanilla Model Implementation**
The model trained on water potability predictions is increasing smoothly in accuracy over the epochs, while it is overfitting at the same time after a certain point in the process.

Key Highlights of the Training:

### **Model Architecture:**
Input Layer: A dense input layer with 64 units and ReLU activation, since the number of features in the data is that much.
Hidden Layer: Comprise one dense layer of 32 units with ReLU activation.
Output Layer: One unit, Sigmoid activation, the task is to provide binary predictions about water potability.
### **Training Progress:**
A decent start where initial accuracies lie in the range of 0.59 and quickly get into the range of 0.70-0.80.

**Overall Best Performance:** Somewhere in epoch 30-35, where training accuracy goes up towards 77-80%, the validation accuracy stays around 69-70%.

**Overfitting Signs:** After the 35th epoch, the validation loss starts to be stuck, or even slightly increase, while the accuracy of training continuously improves-this is a surefire sign of overfitting.

![first](https://github.com/user-attachments/assets/ae47a6f2-344e-41b5-bdc0-4871610596c8)

### **Validation Performance:**
The validation accuracy was hovering between 66 and 70%, and hence proved moderate generalization on unseen data but could not show further consistent improvement.
The graph for validation loss did not keep on falling and showed a slight increase toward the later epochs, thus cementing the overfitting signs.

### **Possible Improvements:**
**Early Stopping:** It would be beneficial to avoid overfitting by early stopping, when the validation loss stops improving.
**Regularization:** Overfitting could be prevented by the addition of L2 regularization or dropout.

### **Second model with L1 regularisation with early stopping and Adam optimiser**
For the second model, L1 regualrisation was implemented together with early stopping and Adam optimiser. I kept tunning the L1 hyperparameters like kernel_regularizer size, and the Adam hyperparameter (learning rate). I realized these while tuning the learning rate:

**i) Higher learning rate**: Model used fewer epochs since the model can make larger weight updates, but it risks overshooting the optimal point or causing large oscillations, triggering early stopping prematurely.

**ii) Lower learning rate**: Model used more since weight updates are smaller, but the model could more smoothly converge to a minimum, potentially leading to more effective training and fewer early stops.

However it had a very little impact on the validation accuracy and significantly reduced the training accuracy.

**Confusion Matrix for model explained above:**

![download](https://github.com/user-attachments/assets/3a4ed90b-2c52-497e-a882-d3f99ff166ff)

This confusion matrix implies that the model cannot accurately predict class 1 (positive class) and is heavily skewed toward class 0 (negative class). This is troublesome since there are a lot of false negatives resulting from the model's zero accuracy in detecting the positive class (1). This could be due to class imbalance which is most probably the case. 

### **3. Using L1 with RMSPOP Optimiser**

Changing the optimiser for L1 only improved the model performance by 2%. which is not significant enough but it goes to show that sometimes changing the optimiser can help.

**Confusion Matrix for model above:**

![download](https://github.com/user-attachments/assets/3a4ed90b-2c52-497e-a882-d3f99ff166ff)

As we can see, the confusion matrix did not change compared to the previous one.

### **Model with L2 Regularization, Adam Optimizer**

In this model, L2 regularization was applied to combat overfitting, using the Adam optimizer for efficient weight updates. Key findings while tuning the learning rate were:

i) Higher Learning Rate: The model trained faster with fewer epochs, but larger weight updates risked overshooting the optimal point, leading to premature early stopping.

ii) Lower Learning Rate: The model trained slower, requiring more epochs but resulted in smoother convergence and more stable training.
The overall overview is that the model results and accuracy did not differ from the previous model as the confusion matrices are almost identical. 

**Confusion Matrix for the model above:**

![tfdownload](https://github.com/user-attachments/assets/4c394239-f9ef-42f0-bdeb-69f51fa66763)
### Model with L2 Regularization,
 RMSprop Optimizer, and Early Stopping
This model employs L2 regularization in both layers to reduce overfitting. The RMSprop optimizer, set with a learning rate of 0.0001, is used for adaptive weight updates.

Key Observations:
i) Higher Learning Rate: Using a higher learning rate (e.g., 0.001) led to faster convergence but risked overshooting and premature early stopping.

ii) Lower Learning Rate: A lower learning rate (0.0001) allowed for smoother convergence over more epochs, though it extended training time.

Result:
Despite implementing L2 regularization and RMSprop, the model's performance showed no significant improvement, with validation accuracy and confusion matrix similar to earlier models.

**Confusion Matrix for the model above:**


![download](https://github.com/user-attachments/assets/b57902cd-5dd2-4ea5-ab4b-8005205d0331)

### Model with L2 Regularization, Dropout and Adam Optimizer

This model employs L2 regularization and Dropout to mitigate overfitting, utilizing the Adam optimizer with a learning rate of 0.001. The ReduceLROnPlateau callback adjusts the learning rate if the validation loss does not improve for 10 epochs.

Key Observations:
i) Dropout: The use of Dropout (40% in the first layer and 30% in the second) effectively reduces overfitting by randomly deactivating neurons during training.

ii) Learning Rate Adjustment: The ReduceLROnPlateau strategy enables the model to dynamically lower the learning rate, allowing for finer adjustments in weight updates.

### Result:
This model performed better than previous versions up to 70 percent of accuracy, with improved validation accuracy and class predictions.

**Confusion Matrix for the model above:**

![nload (1)](https://github.com/user-attachments/assets/38a0b478-ac90-4bd2-9a04-a839d6d793e9)



### <u>Authors and Contributors</u>

- Achuli Mustapha Sadick - m.achuli@alustudent.com
- Ochan Den-Mark Michael LOKIDORMOI - o.lokidormo@alustudent.com
- Dimitri Kwihangana - k.dimitri@alustudent.com
- Alhassan Alimamy Dumbuya - a.dumbuya@alustudent.com

