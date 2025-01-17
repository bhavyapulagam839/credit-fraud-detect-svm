# Fraud Detection Using PCA and Hyperplane Classification

Overview

This project focuses on detecting fraudulent transactions using Principal Component Analysis (PCA) for dimensionality reduction and different hyperplane-based classification approaches to balance false positives (FP) and false negatives (FN).

Data Preprocessing

We used PCA to reduce the dimensionality of the input dataset. Out of 28 features, we selected the first 10 principal components, as they retained 96.6% of the total variance. The remaining features were dropped due to their insignificant contribution to the dataset.

Approach

We implemented three different classification approaches to handle the imbalance between fraud and non-fraud transactions effectively.

Approach 1: Equal Weighting (Undersampling)

We undersampled the non-fraud data and balanced it with fraud transactions.

The training dataset consists of 293 fraud transactions and 300 non-fraud transactions randomly sampled from the full dataset.

The model was trained with equal weighting for both classes.

Approach 2: Unequal Weighting

The fraud and non-fraud classes were assigned different weights, determined as the reciprocal of the ratio of their occurrences in the dataset.

The penalty constant C was adjusted per class, giving higher importance to the fraud class to reduce FN cases.

With weights set to fraud = 0.6 and non-fraud = 0.4, the confusion matrix showed a decrease in FN cases (from 22 to 20) but an increase in FP cases (from 4541 to 6229).

Approach 3: Hyperplane Shifting

This approach builds on Approach 2 by shifting the hyperplane towards the non-fraud class using a buffer value buffer / ||w||2.

This shift ensures more transactions are classified as fraud to align with a "Better Safe Than Sorry" policy.

The trade-off: While FN cases decrease, FP cases increase, requiring banks to inspect more flagged transactions.

Effect of buffer changes:

Buffer = 0.3: FN = 17, FP = 7760

Buffer = 0.5: FN = 14, FP = 12650

Buffer = 0.7: FN = 11, FP = 17402

Increasing the buffer reduces FN but significantly increases FP, making buffer selection crucial based on available resources.

Evaluation

We evaluated model performance using confusion matrices:

Confusion matrix insights:

False negatives (FN): Fraud transactions misclassified as non-fraud.

False positives (FP): Non-fraud transactions flagged as fraud.

Banks need to choose a buffer balancing resource allocation and fraud detection efficiency.

Conclusion

PCA effectively reduced dimensionality while preserving relevant information.

Weighted classification helped in improving fraud detection rates.

Hyperplane shifting allowed for better fraud detection but increased FP cases.

Banks should experiment with different buffers to find an optimal trade-off between FN and FP based on financial resources and risk tolerance.



