![](bbox=[0.27, 0.1, 0.73, 0.24])

Figure 4.8: Perceptron.

weights were implemented as potentiometers which were updated by electric motors. Specifically, the Perceptron initializes \(\hat{\mathbf{w}}_0 = 0\), and updates the vector \(\hat{\mathbf{w}}_{i-1}\) with each new training sample \(\mathbf{v}_i\) by

\(\hat{\mathbf{w}}_i = \hat{\mathbf{w}}_{i-1} + \frac{\alpha}{2} (c_i - \text{sgn}(\hat{\mathbf{w}}_{i-1}^T \hat{\mathbf{v}}_i)) \hat{\mathbf{v}}_i,\)

where \(c_t\) is the class label of \(\mathbf{v}_t\), that is \(c_i = -1\) if \(\mathbf{v}_i \in C_0\) and \(c_i = 1\) if \(\mathbf{v}_i \in C_1\). The parameter \(0 < \alpha \le 1\) is the *learning rate* and is set by the user. If the learning rate is chosen too big, any changes are too radical and oscillations occur. Note that \(\hat{\mathbf{w}}_i\) is the same as \(\hat{\mathbf{w}}_{i-1}\) if the class label was determined correctly. If the class label was determined incorrectly, the separation line is pulled in the direction such that it is more likely that the sample is labeled correctly in future. The sign of \(c_i - \text{sgn}(\hat{\mathbf{w}}_{i-1}^T \hat{\mathbf{v}}_i)\) determines in which direction the separation line is pulled. At any stage, the vector of weights, \(\hat{\mathbf{w}}_i\), is a linear combination of all samples which caused a change of the separation line so far.

The perceptron is implemented as a single layer neural network within the neural network framework in MATLAB (Figure 4.8 and Listing 4.2). We take a closer look at neural networks, when considering non-linear classification.

The perceptron needs to see enough examples for the separation line to settle. An epoch is one complete presentation of the data to the algorithm. Figure 4.9 shows the different separation lines after a certain amount of data has been seen by the perceptron. The unseen data are marked with \(\times\). The learning rate is set to 1. Because of this large value, the separation line changes position quite dramatically between seeing 90% and the complete data set. After 100 epochs the perceptron classifies all samples correctly apart from one outlier. It takes several hundred more epochs for the perceptron to also classify this sample correctly. Given a different seed for the random number generator and thus changing the order in which the data is presented leads to different separation lines.