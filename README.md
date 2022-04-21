# Credit Line Increase Model Card

### Basic Information

* **Person or organization developing model**: Zeeshan Raza, "zraza10@gwu.edu", MohammadEbrahim Zamani Mazdeh, "ebrahim_zamani@gwu.edu", Mariam Kurasbediani "mariamkuras@gwu.edu", Abid Shafiullah, "abidshafi@gwu.edu", 
* **Model date**: August, 2021
* **Model version**: 1.0
* **License**: MIT
* **Model implementation code**: [Fina-Decision-Model.ipynb](Fina-Decision-Model.ipynb)

### Intended Use
* **Primary intended uses**: This model is an *example* probability of default classifier, with an *example* use case for determining eligibility for a credit line increase.
* **Primary intended users**: Students in GWU DNSC 6301 bootcamp.
* **Out-of-scope use cases**: Any use beyond an educational example is out-of-scope.

### Training Data

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

* **Source of training data**: GWU Blackboard, email "jphall@gwu.edu" for more information
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data
* **Source of test data**: GWU Blackboard, email "jphall@gwu.edu" for more information
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None


### Model Details
* **Columns used as inputs in the final model**: 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1',
       'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6',
       'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'
* **Column(s) used as target(s) in the final model**: 'DELINQ_NEXT'
* **Type of model**:Decision Tree Classification Model
* **Software used to implement the model**: Google Colab 
* **Version of the modeling software**:Google Colab with Python Ver: 3.6.9
* **Hyperparameters or other settings of your model**: test size, tree depth, AIR ratio and cutoff which we changed it to 18% were hyperparameters of our model.

### Quantitative Analysis
* **Metrics used to evaluate your final model**: Training AUC, Validation AUC, Test AUC, Asian-to-White AIR, Black-to-White AIR, Hispanic-to-White AIR, Female-to-Male AIR, mean_squared_error, roc_auc_score, cross_val_score, accuracy_score.
* **State the final values of the metrics for all data: training, validation, and test data**: 
   * Trainng AUC: 0.78 ,
   * Validation AUC: 0.75 , 
   * Test AUC: 0.74
   * Asian-to-White AIR: 1.02
   * Black-to-White AIR: 0.87
   * Hispanic-to-White AIR: 0.84
   * Female-to-Male AIR: 1.04
* **Provide any plots related to your data or final model -- be sure to label the plots!**:
 ![image](https://user-images.githubusercontent.com/89197698/130970062-d6d5418c-f176-4534-8243-cbfc3c50aa3a.png)
### Ethical Considerations
* **Describe potential negative impacts of using your model**:
  * Math or software problems:
    * A small change in the data can cause a large change in the structure of the decision tree causing instability. 
    * Single Decision tree is often a weak learner so we require a bunch of decision tree called random forest for better prediction.
  * Real-world risks: 
    * As the AIR for Hispanic to White is 83 percent and it could result in racial profiling. 
* **Describe potential uncertainties relating to the impacts of using your model**:
  * Math or software problems:
    * All the nodes of a specific level in a decision tree depend on the nodes in their previous levels. In other words, how you define the nodes on level ‘n +1’ depends entirely on your definition for the nodes on the level ‘n.’ If your definition at level ‘n’ is wrong, all the subsequent levels and the nodes present in those levels would also be wrong and this could be manipulated by hacker.
  * Real-world risks: who, what, when or how?
    * Decision-tree analysis can help identify or uncover the potential impacts of alternatives so that a decision maker can select the option that is most consistent with her ethical and moral beliefs by adding backdoors into model scoring and exploiting backdoors with watermarked data.
* **Describe any unexpected or results**: 
    * package dependecies is also another risk of using python packages that could result in security problems.
 
