
If \(w\) occurs in the document at least once, then we assign the value 1 to the feature corresponding to the word, and if it does not occur in the document we assign the value 0 to the feature. Basically, each document will be represented by a feature vector of ones and zeros with the same length as the size of the dictionary. Therefore, we are dealing with high dimensionality for large dictionaries, and Naive Bayes classifier is particularly suited for solving this problem.

We create a matrix **D** with the element \(D_{xw}\) to denote the feature (presence or absence) of the word \(w\) in document \(x\), where rows correspond to documents and columns represent the dictionary terms. Based on the Naive Bayes classifier, we can model the class-conditional probability of a document \(x\) coming from class \(k\) as

\[
p(D_x\mid C_k)=\prod_{w=1}^{|\mathcal{D}|}p(D_{xw}\mid C_k)=\prod_{w=1}^{|\mathcal{D}|}p_{kw}^{D_{xw}}(1-p_{kw})^{1-D_{xw}}.
\]

According to the maximum-likelihood estimate described in Section 3.2.3, we may easily obtain the parameter \(p_{kw}\) by

\[
\hat{p}_{kw}=\frac{\sum_{x\in C_k}D_{xw}}{N_k},
\]

where \(N_k\) is the number of documents from class \(k\), and \(\sum_{x\in C_k}D_{xw}\) is the number of documents from class \(k\) that contain the term \(w\). To handle the case that a term does not occur in any document from class \(k\) (i.e., \(\hat{p}_{kw}=0\)), the smoothed estimate is given by

\[
\hat{p}_{kw}=\frac{\sum_{x\in C_k}D_{xw}+1}{N_k+2}.
\]

Similarly, we can obtain the estimation for the prior probability \(p(C_k)\) based on Equation (3.18). Once the parameters \(p_{kw}\) and \(p(C_k)\) are estimated, then the estimate of the class-conditional likelihood can be plugged into the classification rule Equation (3.14) to make a prediction.

**Discussion:** Naive Bayes classifier has proven effective in text classification, medical diagnosis, and computer performance management, among many other applications [21, 25, 27, 36]. Various empirical studies of this classifier in comparison to decision tree and neural network classifiers have found it to be comparable in some domains. As the independence assumption on which Naive Bayes classifiers are based almost never holds for natural data sets, it is important to understand why Naive Bayes often works well even though its independence assumption is violated. It has been observed that the optimality in terms of classification error is not necessarily related to the quality of the fit to the probability distribution (i.e., the appropriateness of the independence assumption) [36]. Moreover, Domingos and Pazzani [10] found that an optimal classifier is obtained as long as both the actual and estimated distributions agree on the most-probable class, and they proved Naive Bayes optimality for some problem classes that have a high degree of feature dependencies, such as disjunctive and conjunctive concepts. In summary, considerable theoretical and experimental evidence has been developed that a training procedure based on the Naive Bayes assumptions can yield an optimal classifier in a variety of situations where the assumptions are wildly violated. However, in practice this is not always the case, owing to inaccuracies in the assumptions made for its use, such as the conditional independence and the lack of available probability data.

## 3.3 Logistic Regression Classification

We have introduced an example of a generative classifier by fitting class-conditional probabilities and class priors separately and then applying Bayes’ theorem to find the parameters. In a direct way, we can maximize a likelihood function defined through the conditional distribution \(p(C_k\mid X)\), which represents a form of discriminative model. In this section, we will introduce a popular discriminative classifier, logistic regression, as well as the parameter estimation method and its applications.

### 3.3.1 Logistic Regression

Logistic regression is an approach to learning \(p(Y\mid X)\) directly in the case where \(Y\) is discrete-valued, and \(X=\langle X_1,\ldots,X_d\rangle\) is any vector containing discrete or continuous variables. In this section, we will primarily consider the case where \(Y\) is a Boolean variable and that \(Y\in\{0,1\}\).

The goal of logistic regression is to directly estimate the distribution \(P(Y\mid X)\) from the training data. Formally, the logistic regression model is defined as

\[
p(Y=1\mid X)=g(\theta^T X)=\frac{1}{1+e^{-\theta^T X}}. \tag{3.19}
\]

where

\[
g(z)=\frac{1}{1+e^{-z}},
\]

is called the logistic function or the sigmoid function, and

\[
\theta^T X=\theta_0+\sum_{i=1}^{d}\theta_iX_i
\]

by introducing the convention of letting \(X_0=1\) (\(X=\langle X_0,X_1,\ldots,X_d\rangle\)). Notice that \(g(z)\) tends towards \(1\) as \(z\to\infty\), and \(g(z)\) tends towards \(0\) as \(z\to-\infty\). Figure 3.1 shows a plot of the logistic function.

![](img/e042be977d84f1032c985f0d70b57c8b_101_0.png)

**FIGURE 3.1:** Illustration of logistic function. In logistic regression, \(p(Y=1\mid X)\) is defined to follow this form.

As we can see from Figure 3.1, \(g(z)\), and hence \(g(\theta^T X)\) and \(p(Y\mid X)\), are always bounded between \(0\) and \(1\).

As the sum of the probabilities must equal \(1\), \(p(Y=0\mid X)\) can be estimated using the following equation

\[
p(Y=0\mid X)=1-g(\theta^T X)=\frac{e^{-\theta^T X}}{1+e^{-\theta^T X}}. \tag{3.20}
\]

Because logistic regression predicts probabilities, rather than just classes, we can fit it using likelihood. For each training data point, we have a vector of features, \(X=\langle X_0,X_1,\ldots,X_d\rangle\) (\(X_0=1\)), and an observed class, \(Y=y_k\). The probability of that class was either \(g(\theta^T X)\) if \(y_k=1\), or \(1-g(\theta^T X)\) if \(y_k=0\). Note that we can combine both Equation (3.19) and Equation (3.20) as a more compact form

\[
p(Y=y_k\mid X;\theta) = \bigl(p(Y=1\mid X)\bigr)^{y_k}\bigl(p(Y=0\mid X)\bigr)^{1-y_k} \tag{3.21}
\]

\[
= \bigl(g(\theta^T X)\bigr)^{y_k}\bigl(1-g(\theta^T X)\bigr)^{1-y_k}. \tag{3.22}
\]

Assuming that the \(N\) training examples were generated independently, the likelihood of the parameters can be written as

\[
L(\theta) = p(\mathbf{Y}\mid \mathbf{X};\theta)
\]

\[
= \prod_{n=1}^{N} p(Y^{(n)} = y_k \mid X^{(n)};\theta)
\]

\[
= \prod_{n=1}^{N} \bigl(p(Y^{(n)} = 1\mid X^{(n)})\bigr)^{Y^{(n)}} \bigl(p(Y^{(n)} = 0\mid X^{(n)})\bigr)^{1-Y^{(n)}}
\]

\[
= \prod_{n=1}^{N} \bigl(g(\theta^T X^{(n)})\bigr)^{Y^{(n)}} \bigl(1-g(\theta^T X^{(n)})\bigr)^{1-Y^{(n)}}
\]

where \(\theta\) is the vector of parameters to be estimated, \(Y^{(n)}\) denotes the observed value of \(Y\) in the \(n\)th training example, and \(X^{(n)}\) denotes the observed value of \(X\) in the \(n\)th training example. To classify any given \(X\), we generally want to assign the value \(y_k\) to \(Y\) that maximizes the likelihood as discussed in the following subsection.

### 3.3.2 Parameters Estimation for Logistic Regression

In general, maximum likelihood is used to determine the parameters of the logistic regression. The conditional likelihood is the probability of the observed \(Y\) values in the training data, conditioned on their corresponding \(X\) values. We choose parameters \(\theta\) that satisfy

\[
\theta \leftarrow \arg\max_\theta L(\theta),
\]

where \(\theta = \{\theta_0, \theta_1, \ldots, \theta_d\}\) is the vector of parameters to be estimated, and this model has \(d+1\) adjustable parameters for a \(d\)-dimensional feature space.

Maximizing the likelihood is equivalent to maximizing the log likelihood:

\[
l(\theta) = \log L(\theta) = \sum_{n=1}^{N} \log p(Y^{(n)} = y_k \mid X^{(n)};\theta)
\]

\[
= \sum_{n=1}^{N} \left[ Y^{(n)} \log g(\theta^T X^{(n)}) + (1-Y^{(n)}) \log\bigl(1-g(\theta^T X^{(n)})\bigr) \right] \tag{3.23}
\]

\[
= \sum_{n=1}^{N} \left[ Y^{(n)} (\theta^T X^{(n)}) - \log\bigl(1+e^{\theta^T X^{(n)}}\bigr) \right]. \tag{3.24}
\]

To estimate the vector of parameters \(\theta\), we maximize the log likelihood with the following rule

\[
\theta \leftarrow \arg\max_\theta l(\theta). \tag{3.25}
\]

Since there is no closed-form solution to maximizing \(l(\theta)\) with respect to \(\theta\), we use gradient ascent [37,38] to solve the problem. Written in vectorial notation, our updates will therefore be given by

\[
\theta \leftarrow \theta + \alpha \sum_{n=1}^{N} \bigl(Y^{(n)} - g(\theta^T X^{(n)})\bigr) X^{(n)},
\]

where \(\alpha\) is the learning rate.

### 3.3.3 Regularization

To reduce overfitting, we can instead choose \(\theta\) to maximize the regularized log likelihood \(l(\theta) + \log p(\theta)\), where \(p(\theta)\) is a prior distribution over the parameters, and if \(p(\theta)\) is a zero mean Gaussian distribution, then \(\log p(\theta)\) yields a term proportional to \(\|\theta\|^2\). After taking partial derivatives, we can easily obtain the form

\[
\frac{\partial l(\theta)}{\partial \theta_i} = \sum_{n=1}^{N} \bigl(Y^{(n)} - g(\theta^T X^{(n)})\bigr) X_i^{(n)} - \lambda \theta_i,
\]

and the modified gradient descent rule becomes

\[
\theta_i \leftarrow \theta_i + \alpha \sum_{n=1}^{N} \bigl(Y^{(n)} - g(\theta^T X^{(n)})\bigr) X_i^{(n)} - \alpha \lambda \theta_i.
\]

### 3.3.4 Applications

Logistic regression is used extensively in numerous disciplines [26], including the Web, and medical and social science fields. For example, logistic regression might be used to predict whether a patient has a given disease (e.g., diabetes), based on observed characteristics of the patient (age, gender, body mass index, results of various blood tests, etc.) [3,22]. Another example [2] might be to predict whether an American voter will vote Democratic or Republican, based on age, income, gender, race, state of residence, votes in previous elections, etc. The technique can also be used in engineering, especially for predicting the probability of failure of a given process, system, or product. It is also used in marketing applications such as predicting of a customer’s propensity for purchasing a product or ceasing a subscription, etc. In economics it can be used to predict the likelihood of a person’s choosing to be in the labor force, and in a business application, it would be used to predict the likelihood of a homeowner defaulting on a mortgage.

## 3.4 Probabilistic Graphical Models for Classification

A graphical model [13, 17] is a probabilistic model for which a graph denotes the conditional independence structure between random variables. Graphical models provide a simple way to visualize the structure of a probabilistic model and can be used to design and motivate new models. In a probabilistic graphical model, each node represents a random variable, and the links express probabilistic relationships between these variables. The graph then captures the way in which the joint distribution over all of the random variables can be decomposed into a product of factors, each depending only on a subset of the variables. There are two branches of graphical representations of distributions that are commonly used: directed and undirected. In this section, we discuss the key aspects of graphical models for classification. We will mainly cover a directed graphical model hidden Markov model (HMM), and undirected graphical model conditional random fields (CRF). In addition, we will introduce basic Bayesian networks and Markov random fields as the preliminary contents for HMM and CRF, respectively.

### 3.4.1 Bayesian Networks

Bayesian networks (BNs), also known as belief networks (or Bayes nets for short), belong to the directed graphical models, in which the links of the graphs have a particular directionality indicated by arrows. Formally, BNs are directed acyclic graphs (DAG) whose nodes represent random variables, and whose edges represent conditional dependencies. For example, a link from random variable \(X\) to \(Y\) can be informally interpreted as indicating that \(X\) “causes” \(Y\). For the classification
