# Fraud Detection Project

## Observations

1. **Data Quality:** The dataset contained no null values or duplicates.
2. **Fraud Detection Insights:** Transactions categorized as `cash_out` with zero amounts were flagged as fraudulent.
3. **Outlier Management:** Capping outliers (winsorization) enhanced model performance compared to outright removal.
4. **Feature Correlations:** High correlations were observed between `oldbalanceOrg`/`newbalanceOrg` and `oldbalanceDest`/`newbalanceDest`, as well as the `amount` feature. Addressing these issues through feature engineering improved model efficacy.
5. **Imbalance in Data:** The dataset was highly imbalanced. Decision Trees and Random Forests outperformed Logistic Regression, achieving higher precision and recall. High precision is critical for effective fraud detection.
6. **Non-Fraudulent Transactions:** Transactions where `nameDest` begins with "M" were consistently non-fraudulent.
7. **Impact of Techniques:** Feature engineering, exploratory data analysis, normalization, and model fine-tuning significantly enhanced fraud detection accuracy.
8. **Transaction Types:** Transactions labeled as `cash_out` and `transfer` showed higher fraud rates compared to other types.

## Challenges

1. **Data Visualization:** The wide range of transaction values (0 to \(10^8\)) complicated visualization efforts, resolved through log transformation.
2. **Model Fine-Tuning:** Limited RAM posed challenges for extensive model fine-tuning.
3. **Parameter Search Limitations:** Hardware constraints restricted the use of comprehensive grid or randomized searches, leading to a focus on fewer parameters.
4. **For Loop Fine-Tuning:** Although not optimized, fine-tuning using for loops was efficient and less time-consuming.
5. **Model Evaluation:** Multiple iterations were required to assess model performance and identify influential factors.
6. **Feature Selection:** Determining which features to drop and the rationale behind these choices was challenging, requiring time-intensive iterative testing with various models.

## Conclusion

This project demonstrated that **careful preprocessing** and **feature engineering** are critical for improving model performance in fraud detection. By capping outliers instead of removing them, we preserved valuable information, and substituting multicollinear features with balance change metrics enhanced model robustness.

Although complex models like XGBoost and Bagging offered high accuracy, they fell short in **precision** and **recall**—essential metrics for fraud detection. In contrast, simpler models like Decision Trees and Random Forests provided a better balance between precision, recall, and F1-scores. This underscores the importance of prioritizing high precision and recall over mere accuracy to minimize false positives and accurately identify fraudulent transactions.

The contributions of **feature engineering** and **normalization** were substantial in enhancing model performance. Challenges such as handling large transaction values and limited computational resources were addressed through log transformations and targeted parameter tuning. Overall, this project highlights that simpler models can often outperform more complex ones in specific tasks like fraud detection, where precision and recall are critical.

## Questions and Answers

### 1. Data Cleaning (Missing Values, Outliers, Multi-Collinearity)

**Answer:**
- **Missing Values:** The dataset had no missing values or duplicates. Transactions where `nameDest` starts with "M" lacked sufficient data and were categorized under a common label for analysis.
- **Outliers:** Used capping (winsorization) to limit the influence of extreme values while retaining critical information.
- **Multi-Collinearity:** Addressed by replacing highly correlated features with derived metrics like `balance_change_orig` and `balance_change_dest`, reducing redundancy and improving robustness.

### 2. Fraud Detection Model Overview

**Answer:** 
The fraud detection model employed **Random Forest** and **Decision Tree** classifiers, selected for their effective feature engineering and fine-tuning capabilities to maintain an optimal balance between precision, recall, and accuracy.

- **Random Forest:** An ensemble approach that enhances performance and generalization by combining multiple decision trees. Key fine-tuned parameters included:
  - `n_estimators`: The number of trees in the forest.
  - `class_weight`: Used to tackle class imbalance (e.g., 'balanced', 'None').

- **Decision Tree:** Known for high precision in detecting fraud and providing interpretability. Key fine-tuned parameters included:
  - `max_depth`: The maximum depth of the tree to control model complexity.
  - `criterion`: The function used to measure split quality (e.g., 'gini', 'entropy').

Model performance was evaluated using metrics like precision, recall, F1-score, and ROC-AUC, complemented by classification reports and confusion matrices for thorough assessment.

### 3. Variable Selection Process

**Answer:**
Variables were selected through a rigorous bi-variate analysis process:

- **Correlation Studies:** Identified relationships between features and the target variable, helping to pinpoint relevant predictors of fraud.
  
- **Box Plots:** Used to visualize the impact of features on fraud detection, comparing distributions across classes (fraudulent vs. non-fraudulent transactions). This approach assisted in addressing multicollinearity by highlighting redundant features.

### 4. Model Performance Demonstration

**Answer:**
Model performance was demonstrated through:

- **Classification Reports:** Detailed metrics including precision, recall, F1-score, and support for each class.
- **Confusion Matrices:** Showed true positives, true negatives, false positives, and false negatives.
- **ROC-AUC Scores:** Evaluated the model's ability to differentiate between classes.

These tools collectively provided a comprehensive view of model effectiveness in fraud detection.

### 5. Key Predictors of Fraudulent Transactions

**Answer:**
Key factors indicating fraudulent transactions included:

- **Transaction Amount:** Higher transaction values often suggested fraud.
- **Transaction Type:** `Cash_out` and `transfer` transactions were more frequently associated with fraud.
- **Balance Changes:** Significant shifts in `oldbalance` and `newbalance` were indicative of potential fraud.
- **Transaction History:** Patterns in transaction history, such as frequency and recent activity, were crucial for identifying fraud.
- **Source Security:** Transactions from less secure sources were more likely to be flagged as fraudulent.

### 6. Validation of Key Predictors

**Answer:**
These factors are logical because:
- **Transaction Amount:** Larger amounts tend to attract more scrutiny and are often flagged as fraudulent.
- **Transaction Type:** Certain transaction types are inherently more associated with fraud.
- **Balance Changes:** Drastic changes can indicate manipulative behavior.
- **Transaction History:** Frequent or unusual activities signal potential fraud.
- **Source Security:** Transactions from insecure sources have a higher likelihood of being fraudulent.

### 7. Recommended Prevention Measures During Infrastructure Updates

**Answer:**
To prevent fraud during infrastructure updates, consider the following best practices:

- **Utilize Verified Apps:** Ensure only trusted applications are used for transactions and sensitive operations.
- **Access Secured Websites:** Conduct transactions only on secured websites with HTTPS encryption.
- **Enhance Data Security:** Implement robust encryption and access controls to safeguard sensitive information.
- **Regular Model Updates:** Continuously retrain fraud detection models with new data to adapt to evolving fraud patterns.
- **Monitor High-Risk Transactions:** Keep a close watch on `cash_out` and `transfer` transactions and large transaction amounts for suspicious activities.

### 8. Evaluating the Effectiveness of Implemented Actions

**Answer:**
To assess the effectiveness of these preventive measures, one should:

- **Monitor Transaction Logs:** Regularly review logs for unusual or unauthorized activities.
- **Conduct Security Audits:** Perform periodic audits to evaluate the efficacy of the implemented measures.
- **Analyze Fraud Detection Metrics:** Track key metrics related to fraud detection, such as the rate of flagged transactions and false positives.
- **Solicit User Feedback:** Gather insights from users regarding their experiences and any security issues they encounter.
- **Evaluate Incident Response Protocols:** Assess the effectiveness of responses to any security breaches.
