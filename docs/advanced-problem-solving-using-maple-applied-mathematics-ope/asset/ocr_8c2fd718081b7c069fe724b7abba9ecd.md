# ## Deep Learning

Deep learning is a subset of machine learning that uses neural networks with many layers to model complex patterns in data. It has driven breakthroughs in computer vision, natural language processing, and speech recognition.

+   - Convolutional Neural Networks (CNNs) for image data
+   - Recurrent Neural Networks (RNNs) for sequence data
+   - Transformers for attention-based modeling

![](bbox=[0.6, 0.32, 0.92, 0.5])

| Model | Accuracy |
|-------|----------|
| CNN   | 98.2%    |
| RNN   | 95.7%    |
| Transformer | 99.1% |

```
```python
import torch
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(784, 256),
    nn.ReLU(),
    nn.Linear(256, 10)
)
```
```

> > "Deep learning is the electricity of the 21st century." — Andrew Ng

The field continues to evolve rapidly, enabling new applications in generative AI, autonomous driving, and personalized medicine.