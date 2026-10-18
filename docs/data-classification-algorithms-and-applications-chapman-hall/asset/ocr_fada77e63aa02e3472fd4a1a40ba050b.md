2. Backpropagation Phase: In the backward phase, the errors are propagated backwards through the neural network layers. This leads to the updating of the weights in the neurons of the different layers. The gradients at the previous layers are learned as a function of the errors and weights in the layer ahead of it. The learning rate λ plays an important role in regulating the rate of learning.

In practice, any arbitrary function can be approximated well by a neural network. The price of this generality is that neural networks are often quite slow in practice. They are also sensitive to noise, and can sometimes overfit the training data.

The previous discussion assumed only binary labels. It is possible to create a k-label neural network, by either using a multiclass “one-versus-all” meta-algorithm, or by creating a neural network architecture in which the number of output nodes is equal to the number of class labels. Each output represents prediction to a particular label value. A number of implementations of neural network methods have been studied in [35,57,66,77,88], and many of these implementations are designed in the context of text data. It should be pointed out that both neural networks and SVM classifiers use a linear model that is quite similar. The main difference between the two is in how the optimal linear hyperplane is determined. Rather than using a direct optimization methodology, neural networks use a mistake-driven approach to data classification [35]. Neural networks are described in detail in [19,51]. This topic is addressed in detail in Chapter 8.

# 1.3 Handing Different Data Types

Different data types require the use of different techniques for data classification. This is because the choice of data type often qualifies the kind of problem that is solved by the classification approach. In this section, we will discuss the different data types commonly studied in classification problems, which may require a certain level of special handling.

# 1.3.1 Large Scale Data: Big Data and Data Streams

With the increasing ability to collect different types of large scale data, the problems of scale have become a challenge to the classification process. Clearly, larger data sets allow the creation of more accurate and sophisticated models. However, this is not necessarily helpful, if one is computationally constrained by problems of scale. Data streams and big data analysis have different challenges. In the former case, real time processing creates challenges, whereas in the latter case, the problem is created by the fact that computation and data access over extremely large amounts of data is inefficient. It is often difficult to compute summary statistics from large volumes, because the access needs to be done in a distributed way, and it is too expensive to shuffle large amounts of data around. Each of these challenges will be discussed in this subsection.

# 1.3.1.1 Data Streams

The ability to continuously collect and process large volumes of data has lead to the popularity of data streams [4]. In the streaming scenario, two primary problems arise in the construction of training models.

+   - One-pass Constraint: Since data streams have very large volume, all processing algorithms need to perform their computations in a single pass over the data. This is a significant challenge, because it excludes the use of many iterative algorithms that work robustly over static data sets. Therefore, it is crucial to design the training models in an efficient way.