
A variety of methods are developed by Rogers et al. [8] to evaluate the accuracy of the predicted wind speed distribution. One method measures the accuracy in terms of ratios between true and actual parameters of the Weibull distribution: that is, true shape versus estimated shape and true scale versus estimated scale. To completely capture any possible inaccuracy in the predicted distribution, we measure a symmetric Kullback-Leibler (KL) distance. It is important to note that this measure is different from the mean-squared error or mean-absolute error, which measure the accuracy in terms of difference between each predicted value and the true observation. Methods that minimize these errors would not necessarily accurately express how close the approximation is to the true distribution. We now proceed to describe the set of statistical approaches we introduce for deployment within the MCP framework.

## 10.3 METHODOLOGY FOR WIND SPEED ESTIMATION

Notationally, we refer to a training point as \(\ell \in \{1,\ldots,L\}\) and a point for which we have to make a prediction as \(k \in \{1,\ldots,K\}\). We drop the notation for time after having time-synchronized all the measurements across locations. We also drop the subscript for directional bin. From this point onward, when we refer to a model, it is the model for a particular bin \(j\). Then, \(f_Z(z)\) refers to a probability density function of the variable (or set of variables) \(z\). \(F_Z(z)\) refers to a cumulative distribution function for the variable \(z\) such that

\[
F_Z(\alpha)=\int_{-\infty}^{\alpha} f_Z(z)\,dz
\]

for a continuous density function.

Our methodology for MCP has four steps:

- **Step 1:** To start, we build a multivariate distribution with the probability density function \(f_{X,Y}(x,y)\), where \(x = \{x_1,\ldots,x_m\}\) are the wind speeds at the historical sites and \(y\) is the wind speed at the site. To do this, we employ likelihood parameter estimation. The model building process is similar for all the bins, and only the data need to be changed.
- **Step 2:** Given the joint distribution from Step 1, we predict the probability density of \(y\) that corresponds to a given test sample \(x_k = \{x_{1,k},\ldots,x_{m,k}\}\) by estimating the conditional density \(f_Y(y|x_k)\). The conditional can be estimated by

  \[
  f_{Y|X=x_k}(y|x_k) = \frac{f_{X,Y}(x_k, y)}{\int_{y} f_{X,Y}(x_k, y)\,dy} \quad (10.1)
  \]

- **Step 3:** We now can make a point prediction of \(\hat{y}_k\) by finding the value for \(y\) that maximizes the conditional:

  \[
  \hat{y}_k = \arg\max_{y \in Y} f(y|\mathbf{X} = \mathbf{x}_k) \quad (10.2)
  \]

- **Step 4:** All the predictions for \(\hat{y}_{1\ldots K}\) are fitted to a Weibull density function, which gives an estimate of the long-term wind resource at the test site.

The methodology implies two design decisions:

- **1. Choosing a model:** A key decision is which density function should be used to model the univariate densities \(f_{x_k}(x)\), and the choice of the joint density function. A simple and straightforward choice is univariate and multivariate Gaussians. This is because Gaussian density functions have closed-form analytic equations for estimation of parameters and evaluating conditionals that are readily computed. Unfortunately, in many cases, this choice could lead to inaccuracies. Individual variables may not fit a Gaussian density function without significant error—for example, when they have significant tail properties or bimodal distribution. A joint Gaussian density function only captures the linear correlation between the variables. If we choose non-Gaussian univariate densities for \(x_n\), then we must employ *copulas* to construct a multivariate joint density function.
- **2. Assumptions regarding variable dependency structure:** Parametric estimation of a joint density function is expensive to compute and requires a large amount of data. Inference from the joint is also expensive. Assuming conditional independency among some variables offers efficiency in all three respects because it allows the density function to be factored. As an example, Figure 10.3 shows two different possible dependency structures for the variables and the output variable \(y\).

![](img/644775a10ad87164013616d709050cee_341_0.png)

FIGURE 10.3 Top: Naïve Bayes structure. This structure is assumed and no learning is required. \(x_1,\ldots,x_{14}\) represents the 14 variables from the airports and \(y\) represents the variable at the test site in Boston. Bottom: Structure is learned using the K2 algorithm. A maximum of two parents is specified, \(x_2\) emerges as a parent for most of the nodes.

Above is the simplest structure, which assumes independence among the input variables given the output variable. Below shows a possible structure that could be learnt from the data.

In wind resource assessment, a primary advantage of learning the dependency structure is the reduction in prediction time despite incorporating more airports into a model while not requiring more site data. Herein, we will evaluate whether the structure should be learned from the data or predefined.

Each of our statistical techniques for wind resource assessment follows these steps. Each is distinctive in terms of Step 1 and how it estimates the joint multivariate density function. We now proceed to describe each of them.

### 10.3.1 Multivariate Normal Model

Here, a multivariate normal model \(N(\mu,\Sigma)\) is assumed for the joint density \(f_{X,Y}(x,y)\) given by

\[
f_Z(z) = (2\pi)^{-(n+1)/2} \det(\Sigma)^{-1/2} \exp\left(-\frac{1}{2}(z-\mu)^T\Sigma^{-1}(z-\mu)\right) \quad (10.3)
\]

where \(z = \{x,y\}\) and \(\det\) represents determinant of a matrix. The multivariate Gaussian density function has two parameters \(\{\mu,\Sigma\}\). We estimate these parameters by maximizing the likelihood function given a set of \(L\) i.i.d observations. The greatest advantage of this model is the ease with which the model can be built as the maximum likelihood estimates (MLEs) simply are given by closed-form analytic forms. The MLE for the mean vector \(\mu\) for the variates \(z\) is simply the sample mean. The MLE of the covariance matrix \(\Sigma\) is given by

\[
\hat{\Sigma} = \frac{1}{L} \sum_{i=1}^{L} (z_i - \bar{z})(z_i - \bar{z})^T \quad (10.4)
\]

Once we estimate the parameters for the joint density given the training data, using closed-form expressions, we use the joint density function to derive the conditional density for \(y\) given \(x_k\) samples in the testing data. This density is also Gaussian and has a mean \(\mu_{y|x_k}\) and variance \(\sigma_{y|x_k}\). The value \(\mu_{y|x_k}\) is used as the point prediction for \(\hat{y}_k\) for the given \(x_k\). The variance \(\sigma_{y|x_k}\) provides the uncertainty around the prediction. If \(\sigma_{y|x_k}\) is high, the uncertainty is high.

### 10.3.2 Nonparametric Multivariate Model

Our second model is adapted from Chan et al. [9], in which the authors employ a multivariate kernel density estimator. A Gaussian kernel is chosen and the density is estimated using all the data \(x_{1\ldots L}\). The multivariate kernel density function is given by

\[
f_{X,Y}(x,y) = \frac{1}{L}\sum_{i=1}^{L} \prod_{j=1}^{m} K(x_j - x_{ij})K(y - y_i) \quad (10.5)
\]

For a test point \(x_k\), for which we do not know the output, a prediction is made by finding the expected value of the conditional density function \(f_Y(y|x_k)\) given by

\[
\begin{aligned}
E(Y\mid X=x_k)&=\int_y y\,f_Y(y\mid x_k)\,dy \tag{10.6}\\
&=\int_y \frac{\frac{1}{L}\sum_{i=1}^{L}\prod_{j=1}^{m}K(x_{j,k}-x_{j,i})K(y-y_i)}
{\frac{1}{L}\sum_{i=1}^{L}\prod_{j=1}^{m}K(x_{j,k}-x_{j,i})}\,dy \tag{10.7}\\
&=\frac{\sum_{i=1}^{L}y_i\prod_{j=1}^{m}K(x_{j,k}-x_{j,i})}
{\sum_{i=1}^{L}\prod_{j=1}^{m}K(x_{j,k}-x_{j,i})} \tag{10.8}
\end{aligned}
\]

In this model there are no parameters and there is no step for estimation. Although Equation (10.5) presents the density function, it is not evaluated unless we see a new testing point. For us to be able to evaluate the expected value of the wind speed at the test site, we need to store all the training points and use them in Equation (10.8) to make predictions. In Equation (10.8), given a test point \(x_k=\{x_{1,k},\ldots,x_{m,k}\}\), the kernel value is evaluated for the difference between a training point \(x_i\) and this test point. This value is multiplied with the corresponding value of \(y_i\). This is repeated for all the training points \(1\ldots L\) and summed. This forms the numerator. The summation, when done without the multiplication of \(y_i\), forms the denominator in Equation (10.8). This approach has a few drawbacks. The designer must choose the kernel. Then the parameters for the kernel should be tuned via further splitting of the training data. It also requires retaining all the training data in order to make predictions. The evaluation of the kernel is done for \(L\) times for each test point.

### 10.3.3 Graphical Model with Naïve Structure

This technique uses a multivariate Gaussian model assuming independent variable dependency structure. We model the joint density function as a Bayesian network with independent variables \(x_{1,\ldots,m}\), that is,
