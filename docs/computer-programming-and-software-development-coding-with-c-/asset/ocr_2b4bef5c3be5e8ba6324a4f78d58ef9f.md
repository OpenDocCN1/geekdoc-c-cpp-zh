from o to 10. Can this neural network classifier outperform wine experts?

# Normalization

```
In [5]: from sklearn.preprocessing import PowerTransformer
cols = [
    'fixed acidity', 'residual sugar', 'chlorides', 'free sulfur dioxide', 'total sulfur dioxid
]
pt = PowerTransformer()
wine[cols] = pt.fit_transform(wine[cols])
```

Due to the nature of the algorithm, neural networks require the data to be normalized and scaled, preferably between o and 1.

# 3. Algorithm

```
In [9]: model = keras.Sequential(
    [
        keras.Input(shape=X.shape[1]),
        layers.Flatten(),
        layers.Dense(64, activation="relu"),
        layers.Dense(256, activation="relu"),
        layers.Dense(1024, activation="relu"),
        layers.Dense(num_classes, activation="softmax"),
    ]
)
```

To ensure both conditions, we're going to use the power transformer. I then create my model, compile, and let it run. It is set to 100 epochs, which might take some time if you do not have a GPU. An alternative would be to use Google Colab or Kaggle for training. Once it finishes, I can check the predictions.