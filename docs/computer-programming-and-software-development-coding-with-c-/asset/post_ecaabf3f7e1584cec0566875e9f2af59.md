
![](img/0155736aec718cf18821e9f10a5d308d_230_0.png)

We obtain the dot product of two matrices, one of the coefficients in linear regression called beta. In neural networks, we call them weights and the other a features x. The difference between perceptron for classification and regression is that the former uses an activation function such as sigmoid or softmax in the output node to define the probabilities for each class. In regression, we remove this activation function in the last layer. Let's focus on regression for now. This network shows a simple perceptron. We have the circles that represent the matrix. Those are the area, years, rooms, has pool, and more. These are the features. Then in the middle we have a layer. This is a hidden layer where each node executes a dot product of x and the matrix of the coefficients. In the end, the output layer with a single node sums everything for the final output, which is a continuous value. Some important things to remember about perceptron regression are the following. First, it requires matrix multiplications instead of arrays like in simple linear regression. Perceptrons can be transformed into a classifier. Weights, w, in perceptrons are usually obtained with an optimization algorithm in contrast to linear regression, which uses least squares. In the output node, perceptron works exactly like linear regression. Calculations are done using the following formula. The hidden layer input calculations are here.

![](img/0155736aec718cf18821e9f10a5d308d_231_0.png)

Then you have the hidden layer output calculations. It uses sigmoid. And the final node prediction is similar to linear regression. For the last algorithm I have a perceptron with keras. It is still with the fish example.

![](img/0155736aec718cf18821e9f10a5d308d_232_0.png)

The process is very similar so far, and here's where I use keras. In this case, the network consists only of two layers, the input, output, and the connections between them.

## Train Predict and Plot

```
In [120]: model = keras.Sequential(
    [
        layers.Flatten(input_shape=(1,)),
        layers.Dense(1, activation="linear"),
    ]
)

optimizer = keras.optimizers.SGD(learning_rate=0.1)
model.compile(loss='mse', optimizer=optimizer, metrics=['accuracy'])
history = model.fit(x_width, y_weight, epochs=10, verbose=1, validation_split=0.1, shuffle=False)
y_pred = model.predict(x_width)
```

Epoch 1/10
5/5 [==============================] - 0s 26ms/step - loss: 0.1850 - accuracy: 0.0000e+00 - val_loss: 1.5773 - val_accuracy: 0.0000e+00
Epoch 2/10
5/5 [==============================] - 0s 6ms/step - loss: 0.1162 - accuracy: 0.0000e+00 - val_loss: 1.3276 - val_accuracy: 0.0000e+00
Epoch 3/10
5/5 [==============================] - 0s 7ms/step - loss: 0.1036 - accuracy: 0.0000e+00 - val_loss: 1.2179 - val_accuracy: 0.0000e+00
Epoch 4/10
5/5 [==============================] - 0s 6ms/step - loss: 0.1008 - accuracy: 0.0000e+00 - val_loss: 1.1671 - val_accuracy: 0.0000e+00

Those are the weights. I trained the network for 10 epochs and I am ready to start making predictions. Using neural network, requires a bit more sophisticated tuning. For example, you can try to add more hidden layers to the network in order to improve the predictions. One thing, neural networks are far superior in terms of accuracy to other more traditional algorithms, but they do require more work. In summary, we have learned what linear regression is and what type of problems it solves. Regression algorithms predict continuous values such as temperature, stock prices or battery life of an electric vehicle. Regression is prone to overfitting, so keep in mind that data transformation, normalization, and feature selection can help improve fit. Regularization is a great way to deal with overfitting. You might want to try L1 or L2 if simple linear regression seems not to be enough. Lasso L1 regularization will leave a small number of significant parameters. Ridge L2 will leave them all, but should be used when we need that all parameters must go into the linear equation, that is, all features are essential. This is a theoretical statement. My recommendation is to test both and see which one improves the fit of your model. Remove outliers. Some data points in a dataset might affect the regression model even if regularization is used. Plotting data helps understand data shape. Understanding if the relationship is linear or not can help determine the right algorithm. Next, I will cover the next type of algorithms, classification algorithms. If you're curious as to what is the difference, regression predicts numbers, while classification predicts labels such as good, bad or neutral.

## Chapter 5 Classification Algorithms & Logistic Regression

When we think about machine learning, there are two categories of problems that we might want to solve. First, the type of problems that predict a continuous value, such as temperature or stock price. And second, the type of problem where we predict categorical values such as high, mid, low; healthy or sick; bird, cat or dog. The second type of problems where we're looking to predict a category are solved using classification algorithms. When performing classification, we want to identify an algorithm that separates the data so that every entry, that is data sample, can be correctly categorized. Classification algorithms learn from a labeled dataset. This is what's called supervised learning. In the dataset, every entry has been tagged with the correct category. The algorithm learns from the data and can infer a new data that it's presented with. One thing worth noting is that correct labeling is essential. The more data, the merrier. If there are mistakes on the labels, then predictions will not be very good; garbage in, garbage out applies. Data shape is also an essential element while considering the algorithm for classification. For example, when performing image classification of chest to identify if a patient has a particular lung problem, not all algorithms can handle large images, high dimensional data. Choosing a suitable algorithm based on data shape is also a vital element of a good classifier. Let's look at some problems, and how they are solved using classification algorithms.

Logistic regression is one of my favorite classification algorithms. It is one of the most basic forms of a neural network, which will help us later down the road to understand this concept. Logistic regression is typically used for binary classification, that is a problem such as true or false, cancer or guilty or innocent. Logistic regression can also be used for classification, but in this case you need to use the softmax layer for classification. For now, let's focus on binary classification. Logistic regression is not a regression problem, but it uses the same linear regression formulas as part of its main algorithm. Logistic regression activates the linear regression function to create a probability. This probability lies within the 0 and 1 threshold, where 0.5 is used to determine whether a value belongs to the 1 class or the 0 class, kind of like this. Think of the 0.5 just as the middle ground, so when you have two options, then it is either one thing or the other. There's a saying where I live; it's either a chicken or a rooster. It may sound funny, but the whole point is that with binary classifiers, you only have two choices. For example, if we trained the logistic regression to identify if I'm subject to getting a loan based on my monthly income, the function used should predict a number between 0 and 1, with anything above 0.5 being approved and anything below means denied. If the prediction is .75, then I automatically get approved. In fact, there's a whole conversation about WMDs, or weapons of math destruction, but that's a whole subject of discussion. It's quite interesting, so if we ever happen to be in the same place, ask me about this and we can talk for hours. Without getting too much into the details, at a high level, the logistic regression algorithm works this way. First we estimate the linear function in the same way as it's done with linear regression. The value obtained will now be set as a parameter to the sigmoid activation function, which is the one that estimates the probability between 0 and 1. This combination of these two functions, one that
