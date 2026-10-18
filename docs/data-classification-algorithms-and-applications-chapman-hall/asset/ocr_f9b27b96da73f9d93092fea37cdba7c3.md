base classifiers, our new x_i' has two dimensions: x_i' = (x_i^1, x_i^2), where x_i^1 is x_i’s predicted label from the first classifier, and x_i^2 is the predicted label from the second classifier. The new data set is shown in Table 19.14.

# TABLE 19.14: Stacking Step 2 on the Toy Example

| x | (1,-1) | (1,-1) | (1,-1) | (-1,-1) | (-1,-1) |
| y | +1 | +1 | +1 | -1 | -1 |
| x | (-1,-1) | (-1,-1) | (-1,1) | (-1,1) | (-1,1) |
| y | -1 | -1 | +1 | +1 | +1 |

Note that in the illustrations of various ensemble algorithms on this toy example shown in the previous sections, we always use one-dimensional data on which we simply apply a threshold-based classifier. In this Stacking example, we can easily extend the threshold-based classifier to two dimensions:

h(x) = { -1, if x^1 = -1 and x^2 = -1
        +1, otherwise. } (19.4)

The final results on the toy example obtained by this second-level classifier are shown in Table 19.15. We can see that the ensemble classifier classifies all the points correctly.

# TABLE 19.15: Stacking Final Result on the Toy Example

| x | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| y | +1 | +1 | +1 | -1 | -1 | -1 | -1 | +1 | +1 | +1 |

# 19.5.2 Stacking and Cross-Validation

In Algorithm 19.7, we use the same data set D to train first-level classifiers and prepare training data for second-level classifiers, which may lead to over-fitting. To solve this problem, we can incorporate the idea of cross validation [49] in stacking. K-fold cross validation is the most commonly used technique to evaluate classification performance. To evaluate the prediction ability of a learning algorithm, we conduct the following K-fold cross validation procedure: We partition training data into K disjoint subsets and run the learning algorithm K times. Each time we learn a classifier from K − 1 subsets and use the learnt model to predict on the remaining one subset and obtain the learning accuracy. The final prediction accuracy is obtained by averaging among the K runs.

As shown in Algorithm 19.8, the idea of cross validation can be combined with Stacking to avoid using the same training set for building both first and second level classifiers. Instead of using all the training examples to get first-level classifiers, we now partition data in D into K subsets and get K classifiers, each of which is trained only on K − 1 subsets. Each classifier is applied to the remaining one subset and the output of all the first-level classifiers constitute the input feature space for the second-level classifier. Note that over-fitting is avoided because the data to train first-level classifiers and the data to receive predicted labels from first-level classifiers are different. After we build the second-level classifier based on the first-level classifiers’ predicted labels, we can re-train first-level classifiers on the whole training set D so that all the training examples are used. Applying the second-level classifier on the updated first-level classifier output will give us the final ensemble output.