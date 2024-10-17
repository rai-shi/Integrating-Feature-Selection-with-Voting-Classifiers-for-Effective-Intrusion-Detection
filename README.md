
# Integrating Feature Selection with Voting Classifiers for Effective Intrusion Detection

This project is developed under the Network Security lecture in Karadeniz Technical University. The aim of the project was to study and develop various IDS projects.  

In this project, various studies related to IDS (Intrusion Detection Systems) were thoroughly reviewed. These reviews aimed to examine different methodologies in detail and analyze the results obtained by combining these methodologies. Additionally, the integration of new methods into existing algorithms was also considered. This study focuses on developing innovative approaches in the field of IDS and improving the performance of existing systems.

The overall content of the project is as follows: Features were extracted for DoS, Probe, U2R, and R2L attacks. These features were combined with machine learning algorithms to examine how accurately the attacks could be detected. Finally, the prediction results of all the machine learning algorithms used were combined using a Voting Decision Mechanism. Through this decision mechanism, the contributions of all models were evaluated, and a final prediction result was obtained.

The methods taken from the reviewed articles are as follows: In the article "[Evaluating Shallow and Deep Neural Networks for Network Intrusion Detection Systems in Cyber Security](https://github.com/rahulvigneswaran/Intrusion-Detection-Systems)", the success rates of machine learning algorithms and deep learning models in IDS systems were compared. In this project, machine learning algorithms such as Logistic Regression, Gaussian, Decision Tree, AdaBoost, and Random Forest, mentioned in the article, were used. Additionally, in the article "[A Subset Feature Elimination Mechanism for Intrusion Detection System](https://github.com/CynthiaKoopman/Network-Intrusion-Detection)", the impact of feature selection on the accuracy of attack detection was examined. Although several feature extraction methods were discussed in that paper, in our project, the ANOVA-F statistical test was used for feature extraction.

## Methodologies

In our project, we used various machine learning algorithms to detect network security threats. Each algorithm has its own unique advantages, and the reasons for choosing these algorithms in our project are as follows:

• Logistic Regression (LR)
Logistic regression was used as a basic classification method in our project. It provides a good starting point for identifying fundamental threats in network security and allows us to compare it with more complex models. It is a highly interpretable model, as the outputs can be understood as probabilities. The training process is fast and can work efficiently even with large datasets. Additionally, due to its simple structure, it has a low risk of overfitting.

• Naive Bayes (NB)
Naive Bayes is an effective classifier, especially in cases where the variables in the dataset are assumed to be independent. It can be trained quickly, even on large datasets. It performs well on both large and small datasets. The simplicity and speed of the algorithm make it easy to apply. It can be used for the quick and effective detection of network security threats.

• Decision Trees (DT)
Decision trees were preferred for detecting network security threats because the decision rules are easily understandable. This makes it clear how and why threats are detected. Decision trees are easily interpretable thanks to the decision rules and visualization. They help in identifying important features by selecting variables relevant to the target. They also have low preprocessing and normalization requirements.

• AdaBoost (Adaptive Boosting)
AdaBoost provides high performance in detecting network security threats. By combining different weak learners, it allows us to obtain more accurate and reliable results. It creates a strong learner by combining weak learners, usually resulting in high accuracy. It reduces the risk of overfitting. Its flexibility is high, meaning it can be used with various weak learners.

• Random Forest (RF)
Random Forest provides high accuracy even on complex datasets. It allows us to obtain reliable and generalizable results in detecting network security threats. Predictions obtained by combining multiple decision trees generally result in high accuracy. It reduces the risk of overfitting and enhances generalization ability. It also helps in identifying which features are more important.

The main reason for choosing these methods in our project is that each offers different advantages in detecting network security threats. The simplicity and interpretability of logistic regression, the speed and efficiency of Naive Bayes, the interpretability of decision trees, the high performance of AdaBoost, and the accuracy and generalization ability of Random Forest expanded the scope of our project and improved detection accuracy. The combination of these methods helped us effectively detect network security threats and ensured the success of our project.

In our project, the ANOVA (Analysis of Variance) method plays an important role, particularly in the feature selection process. The advantages of ANOVA and the reasons for using it in this project are as follows:

- Determining the Importance of Features: ANOVA measures the effect of independent variables on the dependent variable to determine which features are more important for the model. This is useful for improving model accuracy and eliminating unnecessary features. 
- Simple and Fast: It is computationally simple and fast. It can be easily applied even on large datasets. 
- Statistical Significance: ANOVA determines whether each feature's effect on the dependent variable is statistically significant. This increases the reliability of the model. 
- Dimensionality Reduction: By selecting features, it reduces the size of the data, allowing for simpler and faster models. This positively impacts the training time and performance of the model, especially on high-dimensional datasets.

The main reason for choosing ANOVA in our project is to determine whether the features used in detecting network security threats are important and to improve the model's performance. ANOVA helps select important features and eliminate unnecessary ones, especially in large and complex datasets. This helps the model produce more accurate and reliable results.

#### Comparison of ANOVA and RFE: 
• ANOVA: ANOVA evaluates the impact of each feature on the dependent variable independently and performs a statistical significance test. It is effective, especially when the correlation between independent variables is low. 

• RFE (Recursive Feature Elimination): RFE iteratively eliminates features and determines the best feature set based on the model's performance. This method is more complex and computationally intensive but provides more precise and detailed feature selection.

The reason for preferring ANOVA in this project is its ability to provide fast and effective feature selection for detecting network security threats. ANOVA delivers quick and reliable results, especially on high-dimensional datasets. Additionally, by determining the statistical significance of each feature, it improves the model's accuracy. Therefore, ANOVA is an ideal choice for effectively detecting network security threats in our project.


In the project, we used Voting classification as the decision mechanism. The reason for using this method is that it is one of the ensemble learning techniques and provides the ability to make stronger and more balanced predictions by combining multiple classification or regression models. There are two sub-methods: Hard Voting and Soft Voting. Hard Voting is the simplest ensemble learning method. Each classifier makes a prediction, and the majority's prediction becomes the ensemble's decision. For example, if three classifiers identify an image as a cat and one classifier identifies it as a deer, the ensemble’s prediction would be "cat." Soft Voting, on the other hand, considers the reliability of the classifiers' predictions. Each classifier assigns a probability to each class, and the class with the highest total probability becomes the ensemble's prediction. For example, if one classifier predicts with 90% probability that an image is a cat and another predicts with 10% probability that it is a deer, the ensemble’s decision would be "cat." In our application, we chose the Soft Voting method.

This method benefits from the diversity provided by combining different features or algorithms, allowing each model to compensate for its own errors. As a result, it offers advantages such as better generalization ability, higher precision, and less overfitting.

## Operational Flow of the Code

- Applying Preprocessing Steps to the Datasets
In our project, we used the NSL-KDD dataset. The first step of the project is to preprocess the dataset. The dataset contains some columns with categorical data. These categorical columns are identified, and appropriate preprocessing steps are applied. The categorical columns are "protocol_type," "service," "flag," and "label." For all columns except the "label" column, each category in the respective column is identified, and these categories are added to the dataset as separate columns using dummy columns. The categorical data in these columns are first label-encoded. Based on the output of this process, One-Hot Encoding is then applied to the newly created dummy columns.

The "label" column contains information on which type of attack the row belongs to. Each attack category in the "label" column is identified. These attack types are divided into four main categories: DoS, Probe, R2L, and U2R attacks. The dataset is then split based on these four main attack categories, using the updated "label" column. For example, the rows that belong to DoS attacks are added to the DoS dataset. In the final step of this phase, the datasets split according to the attacks are scaled and prepared for the ANOVA F-Test.

- ANOVA F-test
Next, the ANOVA F-test is applied to each attack dataset, and the most significant columns (features) within each dataset are obtained.

- Model Training
At this stage, the datasets are rearranged for the models that will perform attack detection. From each dataset, the columns containing the selected features are separated, and new attack datasets are prepared with only the most significant features. Each dataset is normalized.

Then, for each dataset, classification models are created using the selected machine learning algorithms.
Finally, for the decision-making model, we used the ensemble method known as Voting Classifier, which included the same Logistic Regression, Gaussian Naive Bayes, Decision Tree Classifier, AdaBoost Classifier, and Random Forest Classifier algorithms. By combining multiple algorithms through this voting classification technique, a decision-making model was created that can make more accurate predictions.

The Voting Classifier models were trained using the selected features from each of the attack datasets, and a total of four models were created, one for each type of attack.

In the Probe attack classification models, the labels were originally 0 and 2. Since the binary method could not be used in this case, the labels were initially updated to 0 and 1, and all models were run. 

Afterward, in the R2L classification the label distribution in the dataset was examined, and considering the imbalance, the average values were changed to **weighted**. It was observed that the models performed better under these conditions. 

To try again, the attack label values were left as 0 and 2 in the Probe attack classification section, and the model score average continued to use the weighted parameter. Here too, an increase in the scores was observed. Then, the weighted approach was tested for the DoS and U2R datasets as well, and again, an improvement in model performance was noted.

**As a result because of the imbalanced of the datasets the average values were continued with the weighted**. ```average="weighted"```

Here the imbalance of the datasets
```
DoS_df["label"].value_counts()

label
0    67343
1    45927
Name: count, dtype: int64
```

```
Probe_df["label"].value_counts()

label
0    67343
2    11656
Name: count, dtype: int64
```

```
R2L_df["label"].value_counts()

label
0    67343
3      995
Name: count, dtype: int64
```
```
U2R_df["label"].value_counts()

label
0    67343
4       52
Name: count, dtype: int64
```

At the end of the project file you can find a section of experiment through the dataset. This section prepared for testing the models with their test datasets. Each time a random row will be selected for each model's test datasets and models will predict their label. 

## Results

The F1 score provides a good balance between precision and recall. In the DoS and Probe datasets, the distribution between labels is reasonable, making it important to consider both metrics. The F1 score better reflects the overall performance of the model. Therefore, the F1 score has been taken into account for these attacks in an overall perspective.

In the R2L and U2R datasets, recall is critically important to ensure that attacks are not missed due to the high level of class imbalance. Recall indicates how well the model detects actual attacks. Therefore, the recall value has also been considered for these attacks from an overall perspective.

F1 score was showed for DoS and probe. Recall for R2L and U2R.


|                         | DoS   | Probe | R2L   | U2R   |
|-------------------------|-------|-------|-------|-------|
| Logistic Regression      | 0.811 | 0.868 | 0.723 | 0.960 |
| Gaussian NB              | 0.811 | 0.875 | 0.850 | 0.992 |
| Decision Tree Classifier | 0.841 | 0.873 | 0.805 | 0.991 |
| Adaboost                 | 0.832 | 0.883 | 0.774 | 0.994 |
| Random Forest Classifier | 0.824 | 0.878 | 0.777 | 0.994 |
| Voting Classifier        | 0.822 | 0.879 | 0.808 | 0.993 |

If we examine the model performance values of each attack one by one,

#### DoS
|                         | Accuracy | Precision | Recall | F1 Score |
|-------------------------|----------|-----------|--------|----------|
| Logistic Regression      | 0.816    | 0.824     | 0.816  | 0.811    |
| Gaussian NB              | 0.813    | 0.814     | 0.813  | 0.811    |
| Decision Tree Classifier | 0.845    | 0.853     | 0.845  | 0.841    |
| Adaboost                 | 0.836    | 0.847     | 0.836  | 0.832    |
| Random Forest Classifier | 0.829    | 0.841     | 0.829  | 0.824    |
| Voting Classifier        | 0.826    | 0.836     | 0.826  | 0.822    |

#### Probe
|                         | Accuracy | Precision | Recall | F1 Score |
|-------------------------|----------|-----------|--------|----------|
| Logistic Regression      | 0.880    | 0.876     | 0.880  | 0.868    |
| Gaussian NB              | 0.886    | 0.883     | 0.886  | 0.875    |
| Decision Tree Classifier | 0.884    | 0.881     | 0.884  | 0.873    |
| Adaboost                 | 0.892    | 0.889     | 0.892  | 0.883    |
| Random Forest Classifier | 0.888    | 0.885     | 0.888  | 0.878    |
| Voting Classifier        | 0.889    | 0.885     | 0.889  | 0.879    |


#### R2L
|                         | Accuracy | Precision | Recall | F1 Score |
|-------------------------|----------|-----------|--------|----------|
| Logistic Regression      | 0.723    | 0.665     | 0.723  | 0.685    |
| Gaussian NB              | 0.850    | 0.851     | 0.850  | 0.828    |
| Decision Tree Classifier | 0.805    | 0.843     | 0.805  | 0.743    |
| Adaboost                 | 0.774    | 0.820     | 0.774  | 0.679    |
| Random Forest Classifier | 0.777    | 0.824     | 0.777  | 0.686    |
| Voting Classifier        | 0.808    | 0.839     | 0.808  | 0.750    |

#### U2R
|                         | Accuracy | Precision | Recall | F1 Score |
|-------------------------|----------|-----------|--------|----------|
| Logistic Regression      | 0.960    | 0.991     | 0.960  | 0.974    |
| Gaussian NB              | 0.992    | 0.992     | 0.992  | 0.992    |
| Decision Tree Classifier | 0.991    | 0.989     | 0.991  | 0.990    |
| Adaboost                 | 0.994    | 0.994     | 0.994  | 0.991    |
| Random Forest Classifier | 0.994    | 0.994     | 0.994  | 0.991    |
| Voting Classifier        | 0.993    | 0.992     | 0.993  | 0.992    |


The performance of the models for each dataset appears to be at a sufficient level. The Voting Classifier has performed above average for each attack. As a result, we can say that feature selection in the attack datasets has increased the performance of the models.




# 
For any inquiries or feedback, please contact. And also project is open if you want to contribute to it.

Special thanks to contributors,

[Zeynep İlkay Şahin](https://github.com/ZeynepIlkay)

[Sevgi Yılmaz](https://github.com/sevgiyilmaz)

[Süveyda Can](https://github.com/suveydacan)

[Ayşenur Tak](https://github.com/rai-shi)
