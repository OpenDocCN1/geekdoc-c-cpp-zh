
One part processes the parameter X and calculates the theta parameters, and the other activates the function, in this case the sigmoid function, to calculate the probability. This is the same thing that every node of a neural network does. The only difference is that in logistic regression we are doing a neural network with one single node. Then we activate h_θ(X) with the following function:

\[
h_\theta(X) = w_0 + \sum_{j=1}^{m} X_{ij} w_j
\]

\[
\hat{y}_i = \sigma(h_\theta(X)) = \frac{1}{1 + e^{-h_\theta(X)}}
\]

And now we can get some predictions. The problem now is that we don't know how good these predictions are. To find the best parameters θ for our logistic functions, we need to use another formula that calculates the cost of the function, that is the error between the predicted and the actual outcomes. Therefore, it becomes evident that the best parameters for the sigmoid function minimize the cost function. The cost function for the logistic regression algorithm looks like this:

\[
J(\theta) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y^{(i)} \log(h_\theta(x^{(i)})) + (1 - y^{(i)}) \log(1 - h_\theta(x^{(i)})) \right]
\]

This cost function is looking for the average difference, that's the error between the true outcomes, the labeled data, and the predicted values. The logistic regression algorithm and many other parametric algorithms require optimization algorithms to help find the best theta parameters that reduce the cost function. These optimization algorithms are creative processes that defy using brute force to find the best parameters based on the outcome of the cost function. We can use some really lovely optimization algorithms to help logistic regression find those theta parameters, such as SGD or Adam. The good news is that all major machine learning frameworks such as Keras, TensorFlow, Caffe, and PyTorch contain all of them ready to use, so it's a matter of testing to see which framework performs best.

Here are some of the most important points for you to remember when using logistic regression:

- We use logistic regression for binary classification, for example, approved or denied, good or bad, sick or healthy.
- You can use logistic regression for classification; however, it will be a classifier. Other algorithms can perform better for classification.
- Remember, as with many other ML algorithms, the input data must be numerical, so using encoding to encode labels and categorical data is needed.
- For best performance, that's classification accuracy, the input features must have a normal or Gaussian distribution as much as possible.
- Logistic regression assumes all variables, that are the features, are independent, so check for covariates and eliminate them if possible.

I'm going to show you the steps I usually take to solve a problem using a particular ML algorithm. Perhaps something of what I am about to show you may help you solve one of your problems.

```python
import pandas as pd
import numpy as np

stroke = pd.read_csv("healthcare-dataset-stroke-data.csv")
stroke.dropna(inplace=True)
stroke.head()
```

|   | id | gender | age | hypertension | heart_disease | ever_married | work_type | Residence_type | avg_glucose_level | bmi | smoking_status |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 9046 | Male | 67.0 | 0 | 1 | Yes | Private | Urban | 228.69 | 36.6 | formerly smoked |
| 1 | 31112 | Male | 80.0 | 0 | 1 | Yes | Private | Rural | 105.92 | 32.5 | never smoked |
| 2 | 60182 | Male | 49.0 | 0 | 0 | Yes | Private | Urban | 171.23 | 34.4 | never smoked |
| 3 | 1665 | Female | 79.0 | 1 | 0 | Yes | Self-employed | Rural | 174.12 | 24.0 | never smoked |
| 4 | 56669 | Male | 81.0 | 0 | 0 | Yes | Private | Urban | 186.21 | 29.0 | formerly smoked |

For the first classification example, I am going to check if a logistic regression algorithm could predict whether a patient is likely to have a stroke based on features like gender, age, various diseases, and smoking status.

![](img/0155736aec718cf18821e9f10a5d308d_239_0.png)

Just as a good practice, it is always important to check our input data for outliers, nulls or dirty data. The simplest way is by describing the dataset. Once I understand the dataset, I perform a bit of feature engineering by dropping columns that are not relevant and then encode each categorical feature.

![](img/0155736aec718cf18821e9f10a5d308d_239_1.png)

One thing that you need to remember is that logistic regression assumes all variables are independent, so it's important to check the correlation between the features. This algorithm in particular works better, that's execution time and convergence, when the data follows a normal distribution. Thus, I verify the distribution of the features using histograms.

### Normalization

```python
In [7]: from sklearn.preprocessing import StandardScaler

age_scaler = StandardScaler()
stroke['age'] = age_scaler.fit_transform(stroke[['age']])

avg_glucose_level_scaler = StandardScaler()
stroke['avg_glucose_level'] = avg_glucose_level_scaler.fit_transform(stroke[['avg_glucose_level']])

bmi_scaler = StandardScaler()
stroke['bmi'] = bmi_scaler.fit_transform(stroke[['bmi']])
```

```python
In [8]: from sklearn.preprocessing import PowerTransformer
#pt = PowerTransformer()
#pt_data['body_mass_power_trans'] = pt.fit_transform(pt_data[['body_mass_g']])
```

The last step before fitting the model is normalizing features, making all the features have similar ranges. I now prepare X and y.

### 2. Feature Selection

```python
In [9]: X = stroke.drop(['stroke'], axis=1)
y = stroke['stroke']
```

```python
In [10]: from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=42)
```

### 3. Algorithm

```python
In [12]: from sklearn.linear_model import LogisticRegression

model = LogisticRegression(class_weight='balanced', penalty='l2', solver='liblinear', max_iter=1000)
model.fit(X_train, y_train)
Out[12]: LogisticRegression(class_weight='balanced', max_iter=1000, solver='liblinear')
```

![](img/0155736aec718cf18821e9f10a5d308d_242_0.png)

In this case, the scatter represents the real target or class to which a given sample belongs. The contour represents model predictions. The color of each marker represents the actual class and the symbol represents the correctness of the prediction. A dot means the sample was predicted correctly and an x if the sample was predicted incorrectly.

## Chapter 6 Naive Bayes & Support Vector Machines

One good thing about machine learning algorithms is that they are the perfect example of how you can solve a problem using multiple different approaches. In this case, let's talk about Naive Bayes classifiers, which are a family of simple probabilistic classifiers that are based on applying the Bayes' theorem with strong, that's naive, independence assumptions between the features. Let me use a quick example to explain. What if I ask you, how often does the Ace of Spades appear in a deck of cards if you pull one card? Well, this is a straight answer. The probability of getting the Ace of Spades is known because there's only 1 in every deck of 52 cards. This assumes all 52 cards are in the deck. But, what is the probability of getting the Ace of Spades after we drew the Ace of Hearts from the deck? Well, this is a typical example of a conditional probability. It's the probability of getting the Ace of Spades given that we already drew the Ace of Hearts. We solve this conditional probability using the Bayes' theorem. The Bayes' theorem states the probability that an event A will happen if an event B occurs first. We write the formula like this.
