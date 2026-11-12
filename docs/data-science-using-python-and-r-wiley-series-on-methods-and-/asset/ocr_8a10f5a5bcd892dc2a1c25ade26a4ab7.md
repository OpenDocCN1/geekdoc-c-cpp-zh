The output from plot(C5) is shown in Figure 6.2.

To obtain classifications for each record in the data set, create the X data frame as in the previous R section and run the predict() command.

```
predict(object = C5, newdata = X)
```

Set object = C5 to use the C5.0 tree you built in this section. Retain the newdata = X input, as in the previous R section. The result is a classification of the Income variable for each record in the training data set.

# 6.4 RANDOM FORESTS

CART and C5.0 both produce a single decision tree based on all of the records, and the specified variables, in the training data set. There is, however, a method that uses multiple trees, where the output of each tree is considered when determining the final classification of each record.

Random forests build a series of decision trees and combine the trees disparate classifications of each record into one final classification. Random forests are an example of an ensemble method. Ensemble methods are a category of modeling techniques that take multiple models' output into account in order to arrive at a single answer. Different ensemble methods take the models' output into consideration in different ways. For more about ensemble models, please see our earlier text.

The random forests algorithm begins building each decision tree by taking a random sample, with replacement, from the original training data set. In this way, each tree will have a different data set on which to be built. For each node of the decision tree, a subset of the predictor variables is selected for consideration. It is possible, in this way, that the variable which would have given the "best" split (according to, for example, the Gini criterion) will not be available for consideration. The decision tree is completed in this way, with no restrictions on how large the tree may get.

Once the different trees are built, they are used to classify the records in the original training data set. Every record in the data set is given a classification by every tree. Since these classifications are highly unlikely to be unanimous for all records, each classification is considered a "vote" for that particular target variable value. The value with the largest number of votes is deemed the final classification of the record.