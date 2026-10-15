# Neural Network

When and How to use a Neural Network

# 1. Data

```
In [1]: import pandas as pd
import numpy as np
from tensorflow import keras
from tensorflow.keras import layers
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

wine = pd.read_csv("winequality-red.csv")
wine.dropna(inplace=True)
wine['quality'] = wine['quality'] - 3
wine.head()
```

Another type of algorithm that we can use is a neural network classifier.

+   1. What variable do we want to predict?
+   
+   Wine quality
+   
+   2. What type of data is?
+   
+   Categorical, quantitative, ordinal. From 0 to 10.
+   
+   3. Which data are we going to use to predict it?
+   
+   All the other features are Numerical, continuous.

In this particular case, I am going to use a simple neural network to predict wine quality based on some features like alcohol, pH, acidity, and others. This type of data is categorical, quantitative, ordinal, and