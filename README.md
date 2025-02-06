CREDIT CARD FRAUD DETECTION

PROBLEM Statement:
Credit card fraud occurs when someone makes an unauthorized purchase using a stolen or misappropriated credit card or card number.
Since establishing the National Cyber Crime Reporting portal in August 2019, approximately 1.3 million scam complaints have been documented as of November 2023. These complaints encompass roughly 126 crores associated with fraudulent activities between 2022 and 2023. 

Goal: To create a machine learning model to identify fraudulent credit card transactions.
      To minimize the use of unauothorized transactions.
      To help strengthen user security.

Data Source:
https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud/data
The dataset contains transactions made by credit cards in September 2013 by European cardholders.

LET'S UNDERSTAND THE DATASET:
There are totat 31 columns in the dataset. Feature V1 to V28 are renamed and unknown originally due to confidentiality issues. The remaining rows are "Time" , "Amount" and "Class".
Features V1, V2, … V28 are the principal components obtained with PCA, so they are scaled already. The only features which have not been transformed with PCA are 'Time' and 'Amount'. Feature 'Time' contains the seconds elapsed between each transaction and the first transaction in the dataset. The feature 'Amount' is the transaction Amount, this feature can be used for example-dependant cost-sensitive learning.
Feature 'Class' is the response variable and it takes value 1 in case of fraud and 0 otherwise.

SO ACCORDING TO THE DATASET WE CAN APPLY ANY SUPERVISED LEARNING MODEL TO THIS DATASET. SO LETS JUMP INTO STATISTICL MODELLING.

1. Data Cleaning
   We will check for nulls. There are no nulls in our dataset.
   We also remove feature 'Time' as it does not help in data modelling as 'Time' contains the second elapsed between each transaction and the first transaction in the dataset.

2. Exploratory Data Analysis
    We observe a class imbalance in our dataset. 99.83% data is non-fraudulent case and only 0.17% data is fraud cases.
    Now , the only known feature to us is 'amount'. So let's explore about it more. So performed Quantatitive Analysis on Feature Amount to know more about dispersion of data for both 
    Classes. Plotted histograms with kde's for Feature Amount of Class Fraud and Non-fraud seperately to understand data dispersion for each classes.  We can observe that the transaction 
    amount for Class Fraud has more counts for smaller amount transactions and the max transaction amount is only 2125.870000

3. Data Pre-Processing
   
   Scaling the Feature 'Amount' as we observe a vast range of distribution. Here, the outliers (extremely high amounts) likely belong to the non-fraudulent class, so identifying and 
   eliminating outliers alone won't help distinguish fraud from non-fraud. By scaling the data robustly, we normalize the range without letting outliers (legitimate but large 
   transactions) dominate the scaling. Hence, used robust scaler for scaling 'Amount'. Methods like RobustScaler use robust statistics (e.g., median, IQR), which are not significantly 
   influenced by outliers. These methods ensure that the central data points are scaled properly, while outliers remain extreme.
  
   The train-test splitting process is done before data manipulation ( in our case class balancing ). In this way, the test set will be highly imbalanced, but we use this because we want 
   to test our model on a real scenario data. We have balanced the data just for the training process.
   We have prepared two different Train-Test sets , first where we have original Amount column with all other columns while dropping scaled_amount column and the second with 
   scaled_amount column and not using original Amount column.

   
   HANDLING CLASS IMBALANCE- (DATA AUGMENTATION)
   The next biggest issue which we are facing is a very huge class imbalance to deal with and we need to apply proper data pre-processing to minimize the model from overfitting and 
   learning only about the majority class which is Non-Fraud class.
   So we have applied resampling technique to handle data imbalance. I have chosen to go along with SMOTE, ADASYN and NearMiss resampling techniques.
    *SMOTE- Imbalance Challenge: Imbalanced datasets lead to biased accuracy metrics; SMOTE mitigates this by focusing on the minority class. SMOTE creates synthetic samples for the 
   minority class. Here , we get equal samples of minority class as the samples of majority class.
    *ADASYN- Adaptive Synthetic Sampling is another oversampling technique similar to SMOTE, but it focuses on generating synthetic data samples adaptively based on the density of the 
   minority class. It creates more synthetic data points for minority samples that are harder to classify (i.e., near the decision boundary).
    *Near Miss- Near Miss is an undersampling technique that selects examples from the majority class based on their distance to instances from the minority class. It works by keeping 
   only those majority class samples that are closest to the minority class samples, essentially creating "near misses".
   
   So now we are prepared with our new balanced datasets. And we will now apply ML model on our training dataset.


   4. Data Modelling
      In this case we can apply any supervised machine learning algorithms or deep neural networks of our choice. Due to the complexities of the neural networks and also beacause of 
      higher interpretability of classical machine learning algorithms we have selected the following ML models to train on the dataset and will evaluate the best model using Test set.
      In credit card fraud detection model's interpretability is an important parameter as one needs to know the reasons behind the result/descision provided by the model. Also, Feature 
      importance is easier to extract, which is crucial in fraud detection. So, we will apply different classical mahcine learning models such as Random Forest, One-Class-SVM, Logistic 
      Regression, Decision Tree, K-NN and AdaBoost.

      *RANDOM FOREST
       An extension of the Decision Tree algorithm, this algorithm just consists of several different decision trees working as an ensemble — each of them evaluates the input and 
       produces some output. All outputs are then consolidated and the class with the most votes is chosen as the model’s prediction. RF is an extension of the bagging method, which 
       involves selecting a random sample of data in a training set.
      * One-Class-SVM
        
        

      

      

      
   
   


   

