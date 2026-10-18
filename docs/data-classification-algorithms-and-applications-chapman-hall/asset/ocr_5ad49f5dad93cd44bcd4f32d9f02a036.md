Now suppose an item has been selected and it is an orange, and we would like to know which box it came from. This requires that we evaluate the probability distribution over boxes conditioned on the identity of the item, whereas the probabilities in Equation (3.4)-(3.9) illustrate the distribution of the item conditioned on the identity of the box. Based on Bayes’ theorem, we can calculate the posterior probability by reversing the conditional probability

$$p(Y=r\mid X=o)=\frac{p(X=o\mid Y=r)p(Y=r)}{p(X=o)}=\frac{6/12\times4/10}{13/50}=\frac{10}{13},$$

where the overall probability of choosing an orange $p(X=o)$ can be calculated by using the sum and product rules

$$p(X=o)=p(X=o\mid Y=r)p(Y=r)+p(X=o\mid Y=w)p(Y=w)=\frac{6}{12}\times\frac{4}{10}+\frac{1}{10}\times\frac{6}{10}=\frac{13}{50}.$$

From the sum rule, it then follows that $p(Y=w\mid X=o)=1-10/13=3/13$.

In general cases, we are interested in the probabilities of the classes given the data samples. Suppose we use random variable $Y$ to denote the class label for data samples, and random variable $X$ to represent the feature of data samples. We can interpret $p(Y=C_k)$ as the *prior probability* for the class $C_k$, which represents the probability that the class label of a data sample is $C_k$ before we observe the data sample. Once we observe the feature $X$ of a data sample, we can then use Bayes’ theorem to compute the corresponding *posterior probability* $p(Y\mid X)$. The quantity $p(X\mid Y)$ can be expressed as how probable the observed data $X$ is for different classes, which is called the *likelihood*. Note that the likelihood is not a probability distribution over $Y$, and its integral with respect to $Y$ does not necessarily equal one. Given this definition of likelihood, we can state Bayes’ theorem as *posterior* $\propto$ *likelihood* $\times$ *prior*. Now that we have introduced the Bayes’ theorem, in the next subsection, we will look at how Bayes’ theorem is used in the Naive Bayes classifier.

# 3.2.2  Naive Bayes Classifier

Naive Bayes classifier is known to be the simplest Bayesian classifier, and it has become an important probabilistic model and has been remarkably successful in practice despite its strong independence assumption [10, 20, 21, 36]. Naive Bayes has proven effective in text classification [25, 27], medical diagnosis [16], and computer performance management, among other applications [35]. In the following subsections, we will describe the model of Naive Bayes classifier, and maximum-likelihood estimates as well as its applications.

**Problem setting:** Let us first define the problem setting as follows: Suppose we have a set of training set $\{(x^{(i)},y^{(i)})\}$ consisting of $N$ examples, each $x^{(i)}$ is a $d$-dimensional feature vector, and each $y^{(i)}$ denotes the class label for the example. We assume random variables $Y$ and $X$ with components $X_1,\ldots,X_d$ corresponding to the label $y$ and the feature vector $x=\langle x_1,x_2,\ldots,x_d\rangle$. Note that the superscript is used to index training examples for $i=1,\ldots,N$, and the subscript is used to refer to each feature or random variable of a vector. In general, $Y$ is a discrete variable that falls into exactly one of $K$ possible classes $\{C_k\}$ for $k\in\{1,\ldots,K\}$, and the features of $X_1,\ldots,X_d$ can be any discrete or continuous attributes.

Our task is to train a classifier that will output the posterior probability $p(Y\mid X)$ for possible values of $Y$. According to Bayes’ theorem, $p(Y=C_k\mid X=x)$ can be represented as

$$p(Y=C_k\mid X=x)=\frac{p(X=x\mid Y=C_k)p(Y=C_k)}{p(X=x)}$$
$$=\frac{p(X_1=x_1,X_2=x_2,\ldots,X_d=x_d\mid Y=C_k)p(Y=C_k)}{p(X_1=x_1,X_2=x_2,\ldots,X_d=x_d)} \tag{3.10}$$

One way to learn $p(Y\mid X)$ is to use the training data to estimate $p(X\mid Y)$ and $p(Y)$. We can then use these estimates, together with Bayes’ theorem, to determine $p(Y\mid X=x^{(i)})$ for any new instance $x^{(i)}$.