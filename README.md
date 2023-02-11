# Fraud_detection

# Objective:
* *Predicting fraudulent transactions for a  financial company and use insights from the model to develop an actionable plan.*

# Data description:
* *Thae data set is having 6362620 rows and 10 columns.*

* *The description of the columns is as follows*

     **step** : *maps a unit of time in the real world. In this case 1 step is 1 hour of time. Total steps 744 (30 days simulation).*

     **type** : *CASH-IN, CASH-OUT, DEBIT, PAYMENT and TRANSFER.*

     **amount** : *amount of the transaction in local currency.*

     **nameOrig** : *customer who started the transaction*

     **oldbalanceOrg** : *initial balance before the transaction*

     **newbalanceOrig** : *new balance after the transaction*

     **nameDest** : *customer who is the recipient of the transaction*

     **oldbalanceDest** : *initial balance recipient before the transaction. Note that there is not information for customers that start with M (Merchants).*

     **newbalanceDest** : *new balance recipient after the transaction. Note that there is not information for customers that start with M (Merchants).*

     **isFraud** : *This is the transactions made by the fraudulent agents inside the simulation. In this specific dataset the fraudulent behavior of the agents aims to profit by taking control or customers accounts and try to empty the funds by transferring to another account and then cashing out of the system.*

     **isFlaggedFraud** : *The business model aims to control massive transfers from one account to another and flags illegal attempts. An illegal attempt in this dataset is an attempt to transfer more than 200.000 in a single transaction.*
     
# Exploratory Data Analysis:     
* *The given data set is loaded to data frame and data analysis is carried out.*
* *From the visualizations it is observed that only 0.13% of the transactions made are fraud.*

![image](https://user-images.githubusercontent.com/121590533/218256465-2d85ca7e-b1c0-472f-a46c-b18ab073bf9a.png)

* *In the data set there are many outliers are present*

![image](https://user-images.githubusercontent.com/121590533/218256768-7ddc7048-5ae1-4258-a2b0-e00f653f6efe.png)

* *Now we know even though outliers are present, some columns contribute or effect the desired output in a good way. To determine the influence of the variables to the ouput we can **VARIANCE INFLATION FACTOR, CORRELATION MAP.***

* *The VARIANCE INFLATIONS FACTORS are listed below*
* 
![image](https://user-images.githubusercontent.com/121590533/218257020-fb733eee-744b-47b9-8f78-33a77546e6b7.png)

* *We can see that oldbalanceOrg and newbalanceOrig have too high VIF thus they are highly correlated.*
* *Similarly oldbalanceDest and newbalanceDest. Also nameDest is connected to nameOrig.*
* *Thus combine these pairs of collinear attributes and drop the individual ones.*

* *After performing the above operations the VARIANCE INFLUENCE FACTORS are listed below*

![image](https://user-images.githubusercontent.com/121590533/218258031-9a554847-1b24-4d10-b0e8-befe26e4945d.png)

# Model training:
* *The object data type columns are converted in to integer data type using label encoder and the amount column is scaled.*
* *After scaling the data is splitted to train and test data for model building.*
* *Since the target variable contains descrete values classification algorithms are used for model building.*
* *For model building Decision Tree, RandomForest Classifier and AdaBoost classifier is used.*
# Evaluation:
* The model is teined using Decision Tree, RandomForest Classifier and AdaBoost classifier. The accuracy score is measued.
* TP,FP,TN,FN are computed for the models
* TP,FP,TN,FN - **Decision Tree**

  True Positives: 1718
  
  False Positives: 748
  
  True Negatives: 1905603
  
  False Negatives: 717
  
  **============================**
  
* TP,FP,TN,FN - **Random Forest**

  True Positives: 1713
  
  False Positives: 67
  
  True Negatives: 1906284
  
  False Negatives: 722
  
  **============================**
  
* TP,FP,TN,FN - **AdaBoostClassifier**

  True Positives: 1218
  
  False Positives: 164
  
  True Negatives: 1906187
  
  False Negatives: 1217
 
  **=============================**
* TP(AdaboostClassifier)<TP(Decision Tree) ~ TP(Random Forest) so no competetion here.
* FP(AdaBoostClassifier)<FP(Decision Tree) >> FP(Random Forest) - Random Forest has an edge TN(Decision
* Tree) < TN(AdaBoostClassifier) < TN(Random Forest) - Random Forest is better here too FN(Decision Tree) ~
* FN(Random Forest) < FN(AdaBoostClassifier)
* Here Random Forest looks good

* *Accuracy of the models are*

![image](https://user-images.githubusercontent.com/121590533/218259748-e9162c79-229e-4d0a-b660-6bf5e43f4298.png)

# Conclusion:
* We have seen that Accuracy of Random Forest, Decision Tree and AdaBoostClassifier is pretty close, although the precision of Random Forest is more. In a fraud detection model, Precision is highly important because rather than predicting normal transactions correctly we want Fraud transactions to be predicted correctly and Legit to be left off.If either of the 2 reasons are not fulfiiled we may catch the innocent and leave the culprit.
* Also the reason I have chosen this model is because of highly unbalanced dataset (Legit: Fraud :: 99.87:0.13). Random forest makes multiple decision trees which makes it easier (although time taking) for model to understand the data in a simpler way since Decision Tree and AdaBoostClassifier makes decisions in a boolean way.
