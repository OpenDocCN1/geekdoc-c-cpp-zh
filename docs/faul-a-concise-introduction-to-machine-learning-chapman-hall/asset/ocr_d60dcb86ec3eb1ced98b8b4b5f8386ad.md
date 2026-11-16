![](bbox=[0.132, 0.102, 0.868, 0.238])

Figure 5.18: Two layer neural network with two input neurons, ten hidden neurons using the heaviside step function, and 3 output neurons using the softmax function.

exp (-c_i C(v_i)) will contribute very little to the total error, since the exponent is a large negative number. If C predicts the class label of v_i incorrectly with great confidence, then exp (-c_i C(v_i)) will contribute a lot to the total error, since c_i and C(v_i) will have opposite sign and the exponent will be a large positive number. We consider C a strong classifier if it predicts correctly with great confidence, and has little confidence in the prediction when making errors.

AdaBoost, short for Adaptive Boosting iteratively generates a series of classifiers C_m. Each iteration improves the current classifier by concentrating on the misclassified elements. Each classifier is stronger than its predecessor. It is generated as a linear combination of simple, weak classifiers k_j which only return ±1. The perceptron could be one of these classifiers. The coefficients in this linear combination are positive. Each coefficient gives the confidence in the weak classifier.

First, C_1 is initialized to the weak classifier k_1(v) which misclassifies the least number of training examples. Its coefficient alpha_1 is chosen to minimize

```
E(C_1) = \sum_{i=1}^N exp (-c_i \alpha_1 k_1(v_i))
= \sum_{c_i \neq k_1(v_i)} exp (\alpha_1) + \sum_{c_i = k_1(v_i)} exp (-\alpha_1),
```

where we used the fact that both c_i and k_1(v_i) only have the values +1 or -1. Differentiating with respect to alpha_1 gives

```
\frac{dE(C_1)}{d\alpha_1} = \sum_{c_i \neq k_1(v_i)} exp (\alpha_1) - \sum_{c_i = k_1(v_i)} exp (-\alpha_1).
```

Let N be the number of samples and N_C be the number of correctly classified samples. We then have

```
\frac{dE}{d\alpha_1} = (N - N_C) exp (\alpha_1) - N_C exp (-\alpha_1).
```