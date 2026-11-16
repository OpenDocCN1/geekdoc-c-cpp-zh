structure for inference and decision making, we are only interested in learning relationships among some of the variables. In particular, in the gene expression example, we are interested in the dependence and causal relationships between the expression levels of certain genes (see [Lander and Shenoy, 1999]).

# 13.2.9 Approximate Model Averaging*

As is the case for model selection, when the number of possible DAGs is large, we cannot average over all DAGs. In these situations, we heuristically search for high-probability DAGs, and then we average over them. In particular, in the gene expression example, because there are thousands of variables, we could not average over all DAGs. Approximate model averaging is discussed next.

# 13.2.9.1 Approximate Model Averaging Using MCMC

Next we discuss how we can heuristically search for high-probability structures and then average over them using the Markov Chain Monte Carlo (MCMC) method.

Recall our two examples of model averaging (Examples 13.14 and 13.15). The first involved computing a conditional probability over all possible DAGs as follows:

```
P(x|\mathbf{y}, \mathbf{D}) = \sum_{\mathbb{G}} P(x|y, \mathbb{G}, \mathbf{D})P(\mathbb{G}|\mathbf{a}, \mathbf{D}).
```

The second involved computing the probability a feature is present as follows:

```
P(F = present|\mathbf{D}) = \sum_{gp} P(F = present|gp)P(gp|\mathbf{D}).
```

In general, these problems involve some function of the DAG or DAG pattern and possibly the data and a probability distribution of the DAGs or DAG patterns conditional on the data. If we average over DAG patterns, we can represent the general problem to be the determination of

```
\sum_{gp} f(gp, \mathbf{D})P(gp|\mathbf{D}), (13.21)
```

where f is some function of gp and possibly D, and P is some probability distribution of the DAG patterns. Although we represented the problem in terms of DAG patterns, we could sum over DAGs instead.

To approximate the value of Expression 13.21 using MCMC, our stationary distribution r is P(gp|D). Ordinarily we can compute P(D|gp) but not P(gp|D). However, if we assume that the prior probability P(gp) is the same for all DAG patterns,

```
P(gp|\mathbf{D}) = \frac{P(\mathbf{D}|gp)P(gp)}{P(\mathbf{D})} = kP(\mathbf{D}|gp)P(gp),
```