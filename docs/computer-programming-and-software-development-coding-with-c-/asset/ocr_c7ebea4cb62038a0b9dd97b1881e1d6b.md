```
```python
import pandas as pd
import numpy as np
import os
```
```

```
```python
sentiment_tweets3 = pd.read_csv("sentiment_tweets3.csv")

sentiment_tweets3.dropna(inplace=True)

sentiment_tweets3.columns = ['Index', 'Message', 'Label']

sentiment_tweets3.head()
```
```

| Index | Message | Label |
|---:|---|---:|
| 106 | just had a real good moment. i missssssssss hi... | 0 |
| 217 | is reading manga http://plurk.com/p/mzp1e | 0 |

Now, I'm going to preprocess some tweets using NLP methods, which gives me a huge amount of features from a bag of words.

```
```python
from sklearn.feature_extraction.text import CountVectorizer
from nltk.tokenize import RegexpTokenizer

# tokenizer para eliminar elementos no deseados de los datos como símbolos y números
token = RegexpTokenizer(r'[a-zA-Z]+')

cv = CountVectorizer(
    lowercase=True,
    stop_words='english',
    ngram_range = (1,1),
    tokenizer = token.tokenize,
    max_features=2000
)

text_counts = cv.fit_transform(sentiment_tweets3['Message'])
```
```

The objective is to determine if a person has or does not have depression based on the tweets. This is called sentiment analysis. I'm going to reduce this enormous amount of words to only three components, and this is how I do it.