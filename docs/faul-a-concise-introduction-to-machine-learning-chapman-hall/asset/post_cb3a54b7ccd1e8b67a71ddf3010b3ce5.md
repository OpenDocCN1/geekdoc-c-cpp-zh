
Using the inversion formula for a block matrix in Appendix A.1.1, the precision matrix of the joint distribution is

\(\left( \begin{array}{cc} C^{-1} + C^{-1}k(\mathbf{x}_*)k(\mathbf{x}_*)^T C^{-1} & -C^{-1}k(\mathbf{x}_*) \\ c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*) & \frac{-C^{-1}k(\mathbf{x}_*)}{c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*)} \\ \frac{c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*)}{1} & \frac{c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*)}{c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*)} \end{array} \right).\)

We can deduce that the conditional probability of \(t_*\) given \(\mathbf{t}\) is normal and has variance and mean

\(\sigma^2(\mathbf{x}_*) = c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*) = \sigma^2 + k(\mathbf{x}_*, \mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*),\)
\(m(\mathbf{x}_*) = k(\mathbf{x}_*)^T C^{-1} \mathbf{t}.\)
(8.11)

Since \(\mathbf{x}_*\) is chosen arbitrarily (excluding \(\mathbf{x}_1, \dots, \mathbf{x}_N\)), this specifies a distribution over functions.

Let \(\mathbf{x}_1^*, \dots, \mathbf{x}_{N^*}^*\) be \(N^*\) points where predictions \(\mathbf{t}^* = (t_1^*, \dots, t_{N^*}^*)^T\) are to be made. The joint distribution of \((\mathbf{t}, \mathbf{t}^*)\) has covariance matrix

\(\left( \begin{array}{cc} \mathbf{C} & \mathbf{K} \\ \mathbf{K}^T & \mathbf{C}^* \end{array} \right),\)

where \(\mathbf{C}\) is as before, \(\mathbf{K}\) is a \(N \times N^*\) matrix given by \(k(\mathbf{x}_n, \mathbf{x}_m^*)\) and the \((i, j)\) entry of \(\mathbf{C}^*\) is \(k(\mathbf{x}_i^*, \mathbf{x}_j^*) + \sigma^2 \delta_{ij}\). The conditional probability distribution of \(\mathbf{t}^*\) given \(\mathbf{t}\) has mean and variance

\(\mathbf{m}^* = \mathbf{K}^T \mathbf{C}^{-1} \mathbf{t},\)
\(\mathbf{\Sigma}^* = \mathbf{C}^* - \mathbf{K}^T \mathbf{C}^{-1} \mathbf{K}.\)

As before, we can draw point values from this distribution and plot as functions to illustrate draws from the posterior Gaussian process. Figure 8.13 illustrates four draws using various kernels along with four training data points from the function \(1 + x + \sin x\), which is drawn in red. The mean of the conditional distribution is drawn in blue along with a band of two standard deviations in gray. The parameters were kept at \(\theta_1 = \theta_2 = 1\). The noise variance was set to 0.00001. The distribution is tightened near the training data, while the uncertainty increases away from the training data points. In the range between two training points the uncertainty is largest in the middle. As can be seen to the right, away from the training data the distribution becomes the prior distribution of the Gaussian process (as for example in Figure 8.12d for the Gaussian kernel) with added noise, since the entries of \(\mathbf{K}\) are getting close to zero, because the Gaussian kernel decreases as the distance between points increases.

Comparing (8.11) to (8.10), we see that the results agree when the kernel is chosen to be \(k(\mathbf{x}, \mathbf{y}) = \mathbf{d}(\mathbf{x})^T \mathbf{A}^{-1} \mathbf{d}(\mathbf{y})\). In the previous section, however, the entries of \(\mathbf{A}\) were determined by maximizing the log evidence. Similarly,

![](img/d3c00252180686426c9e63ab889b535b_279_0.png)

(a) Gaussian kernel, \(\theta_1 = \theta_2 = 1\)

![](img/d3c00252180686426c9e63ab889b535b_279_1.png)

(b) Exponential kernel, \(\theta_1 = \theta_2 = 1\)

![](img/d3c00252180686426c9e63ab889b535b_279_2.png)

(c) Inverse multiquadric kernel, \(\theta_1 = \theta_2 = 1\)

Figure 8.13: Draws from the posterior Gaussian process for different kernels.

\(\theta_1\) and \(\theta_2\) can be chosen by maximizing the log likelihood of the training data, which is given by

\(\mathcal{L} = -\frac{1}{2} \left[ \log |\mathbf{C}| + \mathbf{t}^T \mathbf{C}^{-1} \mathbf{t} + N \log(2\pi) \right].\)

Using the formulae in Appendices A.2.4 and A.2.7 for the derivatives of the determinant and inverse of a matrix, when the entries of the matrix depend on a variable, we arrive at

\(\frac{\partial}{\partial \theta_i} \mathcal{L} = -\frac{1}{2} \left[ \text{tr} \left( \mathbf{C}^{-1} \frac{\partial \mathbf{C}}{\partial \theta_i} \right) - \mathbf{t}^T \mathbf{C}^{-1} \frac{\partial \mathbf{C}}{\partial \theta_i} \mathbf{C}^{-1} \mathbf{t} \right].\)

The \((m,n)\) entry of the derivative of \(\mathbf{C}\) with respect to \(\theta_i\) is

\(\frac{\partial}{\partial \theta_i} (k(\mathbf{x}_m, \mathbf{x}_n) + \sigma^2 \delta_{mn}) = \frac{\partial}{\partial \theta_i} k(\mathbf{x}_m, \mathbf{x}_n).\)

![](img/d3c00252180686426c9e63ab889b535b_280_0.png)

(a) Gaussian kernel, \(\theta_1 \approx 2.81, \theta_2 \approx 2.85\)

![](img/d3c00252180686426c9e63ab889b535b_280_1.png)

(b) Exponential kernel, \(\theta_1 \approx 1.75, \theta_2 \approx 1.66\)

![](img/d3c00252180686426c9e63ab889b535b_280_2.png)

(c) Inverse multiquadric kernel, \(\theta_1 \approx 3.21, \theta_2 \approx 4.74\)

Figure 8.14: Draws from the posterior Gaussian process for different kernels.

Thus the derivative of the kernel with regards to its parameters is needed. For the Gaussian kernel

```
\(k(\mathbf{x}, \mathbf{y}) = \theta_1^2 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right),\)
```

```
\(\frac{\partial}{\partial \theta_1} k(\mathbf{x}, \mathbf{y}) = 2\theta_1 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right) = \frac{2}{\theta_1} k(\mathbf{x}, \mathbf{y}),\)
\(\frac{\partial}{\partial \theta_2} k(\mathbf{x}, \mathbf{y}) = \frac{\|\mathbf{x} - \mathbf{y}\|^2}{\theta_2^3} \theta_1^2 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right) = \frac{\|\mathbf{x} - \mathbf{y}\|^2}{\theta_2^3} k(\mathbf{x}, \mathbf{y}).\)
```

Setting the gradient of \(\mathcal{L}\) to zero and solving for the parameters is generally not straightforward. However, since the gradient is known, it can be used to approximate the maximum iteratively (see for example [2]).

![](img/d3c00252180686426c9e63ab889b535b_281_0.png)

Figure 8.15: Sum of linear and Gaussian kernel with optimized parameters.

Figure 8.14 shows the mean and two standard deviations of the posterior Gaussian process for various kernels, where the parameters have been optimized, as well as four draws. The fit near the data points is excellent, when the Gaussian kernel is used. The inverse multiquadric kernel also performs well, while the exponential kernel seems unsuitable.

The mean of the posterior Gaussian process returns to zero away from the data points due to the choice of kernel, though it does so slower than with the original choice of parameters. Therefore, we combine the Gaussian kernel with a linear kernel. That is, the kernel is given by

```
k(\mathbf{x}, \mathbf{y}) = \theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y} + \theta_3^2 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_4^2} \right).
```

After optimization the parameters are approximately \(\theta_1 \approx 10^{-5}, \theta_2 \approx 0.90, \theta_3 \approx 1.13\) and \(\theta_4 \approx 1.65\). The goodness of approximation is illustrated in Figure 8.15 over a wider range. While the mean drifts away from the true function, the general trend is kept. A better approximation can be achieved with more data. Which combination of kernels should be used depends on the application and is a field of active research with new kernels being developed for specific usages.

![](img/d3c00252180686426c9e63ab889b535b_282_0.png)

Taylor & Francis

Taylor & Francis Group

http://taylorandfrancis.com

## Feature Learning

This chapter concentrates on inferring the building blocks which are essential for an adequate model of the data. Neural networks are revisited and their many variations explained, especially how design choices such as activation (propagation functions) and error functions depend on the task at hand. Error backpropagation is derived in generality as the application of the chain rule when differentiating the different error functions. Autoencoders are introduced as very simple network architecture and illustrated with an extensive example showing how neural networks create a model space for the data. The relationships to other techniques are explored to gain an intuitive understanding of the mechanisms at work. The chapter concludes with a Bayesian treatment of inferring the model space, illustrated by the Indian Buffet Process.

In the previous chapter, the choice of model space was still largely governed by the user, making a choice on basis functions or kernels to be used. The data can inform these choices or optimize parameters of the basis functions or kernels. If the basis functions are kernels centred at the data, the data has influence also this way. However, the shape is still very much up to user choice.

In this chapter, we explore the possibility of the data deciding the model space. To do so, many examples of data generated from the same process are necessary. For example, the MNIST data set of [26], where the generating process was people writing digits, contains 60,000 images of size 28 x 28 pixels of handwritten digits. The objective is a technique which generates a model space where all samples are equally well represented, if reconstruction is the objective, or separated for classification.

One drawback is that this is only possible where enough reliable data is seen. While it is possible to have some samples, where some features are not given or given with non-negligible error, there need to be sufficiently many samples where these features have reliable values. This is known as _veracity_ and is one of the four _V's of Big Data_. The other three are _volume_, _velocity_ and _variety_.
