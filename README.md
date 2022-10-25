# Credit-Card-Fraud-Detection
### Overview
As far as identity theft goes, credit card fraud is the most prevalent. It's hardly surprising that millions of people become victims each year given that there are an estimated 1.5 billion credit cards in the United States alone. $24.26 Billion was lost in 2018 due to payment card fraud worldwide. 

The best approach to defend yourself against credit card fraud is to take precautions whenever possible. Technology innovation, data analytics tools, and machine learning make it feasible to create models that can accurately forecast credit card frauds and contribute to its reduction. Machine learning algorithms can identify fraud and atypical credit card transactions.

Using algorithms like logistic regression, random forests, support vector machines (SVMs), deep neural networks combined with autoencoders, long short-term memory (LSTM) networks, and convolutional neural networks (CNNs), it is possible to classify credit card transactions as genuine or fraudulent. 
Another way is through credit card profiling where it can be determined if someone is using a credit card legitimately or fraudulently
Also, by using techniques for outlier identification to spot transactions that are noticeably different from typical credit card transactions (or "outliers") can help uncover credit card fraud.

#### What are the benefits of using machine learning for credit card fraud detection
- ##### Performance
One major advantage of applying machine learning to the detection of credit card fraud is that ML models outperform traditional fraud detection models by a wide margin. From vast databases, they can recognize thousands of patterns. By studying consumers' app usage, payments, and transaction methods, ML provides insight into how they behave. 

- ##### A quicker detection
A machine learning model is able to swiftly spot any deviations from normal user behavior and transactional patterns. ML algorithms can reduce the risk of fraud and enable more secure transactions by identifying anomalies, such as a sudden spike in transactional amount or geographical change.

- ##### Greater precision
Traditional fraud detection methods result in errors at the payment gateways, which may lead to the blocking of real clients. The accuracy and precision of ML models can be increased with enough training data and insights, which also cuts down on errors and the time needed for manual analysis.

- ##### Increased effectiveness with more data
An algorithm can effectively work with enormous datasets to distinguish between legitimate payments and fraudulent ones after it learns various transactional patterns and behaviors. The models can quickly analyze enormous volumes of data and provide real-time insights for better decision-making.

### Data
- The credit card fraud data set was downloaded from Kaggle. The data set has 284807 observations with 31 columns. However, according to the data source, most of the features are numerical input variables and are the result of a PCA transformation with features V1 to V28 being the principal components obtained with PCA, while the only features which have not been transformed with PCA are 'Time' and 'Amount'. The Feature 'Time' contains the seconds elapsed between each transaction and the first transaction in the dataset. The feature 'Amount' is the transaction Amount. The Feature 'Class' is the target or response variable and it takes value 1 in case of fraud and 0 in case of no fraud. The target 'Class' is highly imbalanced with 492 frauds out of 284,807 transactions


### Results and Findings
- Histograms revealed that most of the variables were either positively or negatively skewed distributions
- Box plots showed the presence of numerous outliers which were treated using the interquartile range method with the 25th and 75th percentile representing the lower and upper bundaries respectively.
- After treating outliers, the distribution of the variables were more symmetrical.
- correlation matrix and heat map showed that  a strong positive correlation exists between the features 'V21' and 'V22'. All other variables are weakly correlated with each other either positively or negatively.
- Without feature selection and balancing of the imbalanced class in the response variable, the logistic regression algorithm did not perform well as it was overfit and was only able to predict the 'no fraud' which was the predominant class.
- Using featurewiz for feature selection, 16 out of 30 variables were selected.
- 
