with processing elements in the pattern layer, and if they are associated to the same class then that category for output is developed. Based on the application, occasionally a fourth layer is added to normalize the input vector if the inputs are not already normalized before they enter the network.

![](bbox=[0.12, 0.246, 0.886, 0.528])

FIGURE 4.4: A Probabilistic Neural Network Example

The pattern layer constitutes a neural implementation of a Bayes classifier, where the class dependent Probability Density Functions (PDF) are approximated using a Parzen estimator. By using the Parzen estimator to determine the PDF the expected risk in classifying the training set incorrectly is minimized. Using the Parzen estimator, the classification gets closer to the true underlying class density functions as the number of training samples increases, so long as the training set is an adequate representation of the class distinctions.

The pattern layer consists of a processing element corresponding to each input vector in the training set. Each output class should consist of equal number of processing elements otherwise a few classes may be inclined falsely leading to poor classification results. Each processing element in the pattern layer is trained once. An element is trained to return a high output value when an input vector matches the training vector. In order to obtain more generalization a smoothing factor is included while training the network. In such a case, it is not necessary for