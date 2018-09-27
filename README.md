# Arif_Test
                                               	Quartic.ai Data Scientist - Challenge Documentation
1.	Details of the codes:

a.	“Data_Scientist_Challenge_V6_23092018.py”: To measure the model’s performance
b.	“Data_Scientist_Challenge_Final_25092018.py”: To create the final model (models are saved and uploaded, no need to play this code)
c.	“Test_Data_Testing_Final_25092018.py”: To predict the test data using the saved models
Note: Two created models and two respective CSV files of the test data performances are uploaded. For regenerating the CSV files, please give the proper path address of the uploaded models in the code “Test_Data_Testing_Final_25092018.py”.  

2.	Questions and answers:

a.	Briefly describe the conceptual approach you chose! What are the trade-offs?

Ans: The block diagram of the experiment is displayed in Fig. 1. After observing the training data, I found a lot of missing values. Hence, first of all, the missing values are imputed with the individual column’s median value. Next, I have used the min-max normalization procedure to keep each feature in the range of 0 to 1. In the training database, there is a huge imbalance between target “0” and “1”. Hence, I have used a popular combined resampling technique (combination of SMOTE: Synthetic Minority Oversampling Technique and Tomek under sampling technique) for balancing the imbalance. Next, the features are fed to Support Vector Machine (SVM) (Radial Basis Function (RBF) kernel and with default setup) and Artificial Neural Network (ANN) classifier (with default setup) for classification purpose. 

















Trade-offs are (i) representation of missing values with the median value and (ii) application of combined resampling technique with the cost of high computation time.

b.	What's the model performance? What is the complexity? Where are the bottlenecks?

Ans: Initially, the training data is split into 70% training and 30% validation. The confusion matrices of SVM and ANN classifiers are shown in Table 1 and 2 for the validation data. Four metrics are used to measure the classification performance on validation data as given in Table 3.

Table 1: Confusion matrix of SVM classifier      Table 2: Confusion matrix of ANN classifier
	Predicted
	0	1
Target	0	142955	29325
	1	5173	1347
	Predicted
	0	1
Target	0	150440	21840
	1	5411	1109

      Table 3: Classification performances in two different classifiers for validation data
Metrics	SVM	ANN
Accuracy (%)	80.700	84.700
Sensitivity (%)	20.659	17.009
Specificity (%)	82.978	87.322
F1 Score	0.072	0.075

The time complexity of the model is high due to the usage of the resampling method; even though, the sensitivity (detection rate of being class 1) is inferior. Consequently, the overall performance of the model is poor. I have also tried 5-fold cross-validation, and the performance in such case is also nearly equal to the performance above. 

The principal bottleneck of this study is the resampling method which takes huge time to generate new samples. However, the application of the resampling method is imperative to balance the number of samples in training data otherwise it will work very poorly on the unseen data.
		
c.	If you had more time, what improvements would you make, and in what order of priority?

Ans: The improvements could be made by applying a few techniques, such as:
(i)	Application of feature selection method (first priority): I observed the distribution of each feature separately for class “0” and class “1” and I am quite optimistic that removing of redundant (or insignificant) features might increase the classification performance.
(ii)	Tuning of classifier’s settings (second priority): I have used default setup of both the classifiers as defined in scikit-learn, python; hence, optimization of the hyperparameters or change in classifier’s configuration (e.g., grid search in SVM, number of hidden neurons, activation functions, and learning algorithm in ANN, etc.) could provide us better classification performance.
(iii)	Application of other imputation techniques (third priority): Other imputation technique such as replacement of missing value with the most frequent value or by applying other predictive models could be found beneficial .
