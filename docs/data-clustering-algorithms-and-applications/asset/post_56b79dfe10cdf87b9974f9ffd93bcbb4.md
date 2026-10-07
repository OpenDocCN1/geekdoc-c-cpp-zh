
# Data Clustering: Algorithms and Applications

![](img/b94d85a2e934001944bcc21abd9a9943_106_0.png)

**FIGURE 3.7:** Graphical representation of LDA. Circles denote random variables, and edges denote dependence between random variables. Shaded circles, the words of the documents, and topics are observed variables, while unshaded circles, like the topics, assignments, and topics, are latent (i.e., unobserved variables). The rectangular boxes are plates representing replication. The $M$ plate represents documents, while the $N$ plate represents the preferred choice of topics and words within a document.

The generative process of LDA can also be described in a graphical model representation as shown in Figure 3.7. The observed variables are the words of the documents, and the hidden variables are the topics of documents, topic assignments of words within documents, and topics. The above generative process defines a joint probabilistic distribution over both the observed and hidden random variables. With the joint distribution, we compute the posterior distribution of the hidden variables given the observed variables.

Now let us formally define some notations. The topic proportions for the $n$th document are $\theta_n$, $\alpha$ and $\beta$. Note that the word probabilities of topics are parameterized by a $K \times M$ matrix $\beta$ where $\beta_k = p(w|k)$, which are treated as quantity to be estimated. In an LDA model, a conjugate prior $\alpha \sim \text{Dir}(\alpha)$ and a multinomial distribution $\theta$ over topics, where $\theta$ follows a Dirichlet distribution $\eta \sim \text{Dir}(\eta)$ [14, 31] can be added to the multinomial distribution $\beta$ over words, serving as a smoothing over words where $\eta$ is an $M$-dimensional parameter vector and $M$ is the size of the vocabulary. The topic assignment for the $n$th document is $z_n$, where $z_{nj}$ is the assignment for the $j$th word in document $d_n$. Finally, the observed words for document $d_n$ are $w_n$, where $w_{nj}$ is the $j$th word in document $d_n$. With this notation, the probability of observing all words in a single document $d_n$ can be

```
$p(w_n|\alpha, \beta) = \int p(\theta_n|\alpha) \prod_{j=1}^{M} p(z_{nj}|\theta_n) p(w_{nj}|z_{nj}, \beta) d\theta_n.$
```

For a collection of documents $C$, the probability of observing all the documents is given by

```
$p(C|\alpha$
```

As illustrated in Figure 3.7, there are three levels to the LDA representation. The parameters $\alpha$, $\eta$, and $\beta$ are collection-level parameters, assumed to be sampled once in the process of generating a collection. The variables $z_{nj}$ and $w_{nj}$ are word-level variables, and $\theta_n$ are document-level variables, sampled per document. To estimate the parameters of LDA, there are two types of approximate algorithms, variational algorithms and sampling-based algorithms. Variational methods are used as approximation methods in a wide variety of settings [39, 78]. The application of variational methods converts the original complex problem into a simplified problem in which inference is feasible. The simplified model is generally characterized by introducing additional parameters and ignoring some troublesome models. A good description of variational inference algorithm for LDA is presented in [14].

# Probabilistic Models for Clustering

Based on that

## 3.4.3 Variations and Extensions

The simple PLSA and LDA models provide powerful tools for discovering and exploring the hidden structure in large collections of documents, which have been extended and adapted in many ways.

One active area of topic modeling research is to relax and extend the statistical assumptions, as to uncover more sophisticated structure in the texts. For example, [80] developed a topic model to relax the bag-of-words assumption by assuming that the topics generate words conditional on the previous words, and [32] developed a topic model that switches between LDA and a static HMM. These models expand the parameter space without improved language modeling performance. Another assumption is that the order of documents does not matter, but long-running collections (e.g., The New York Times and Science magazine) span years, and the topics can change over time. The dynamic topic model [12] proposes that the ordering of the documents gives a richer posterior structure. A third assumption about topic modeling is that the number of topics is assumed known and fixed. The Bayesian nonparametric topic model [74, 11] provides an elegant solution to determine the number of topics by the collection during inference.

In traditional topic modeling, documents are considered independent of each other. However, the documents could be correlated with each other based on additional information, such as author and links, which should be linked to each other when fitting a topic model. The author-topic model [73] is proposed to consider the relations between authors and documents: Papers with multiple authors are assigned to each word to author, drawn from a topic from his topics. In such way, the model allows for inferences about authors as well as documents. In addition, many documents are linked; for example, scientific papers are linked by citation or pages are linked by hyperlink. We can assume linked web pages to be similar with each other, a paper cites another indicates the two papers are somewhat similar. NetPLSA [50] is proposed to incorporate topic modeling with heterogeneous networks, and TMBP [24] is another extended algorithm that can handle heterogeneous networks. Other models that incorporate meta-data into topic models includes relational topic model [22], supervised topic model [13], and Dirichlet-multinomial regression model [51]. A comprehensive overview of current research and future directions in topic modeling is given in [10].

# 3.5 Conclusions and Summary

This chapter has introduced the most used probabilistic models for clustering, which include mixture models, such as Gaussian mixture model and Bernoulli mixture model, and probabilistic topic models, by PLSA and LDA. Some of the methods, like mixture models, may be more appropriate for quantitative data, whereas others, as topic models, PLSI, and LDA, are used more commonly for text data. The goals of learning algorithms for these probabilistic models are to find MLE or MAP estimations for parameters in these models. There are no closed form solutions for most of them. The EM algorithm provides a general and elegant framework to learn mixture models and topic models. For more complicated cases, some variations of the EM algorithm, such as generalized EM and variational EM, can be employed to solve these problems.

# Bibliography

- [1] C. Andrieu, N. de Freitas, and M. Jordan. An introduction to MCMC for machine learning. Journal of Learning Research, 3:993–1022, 2003.
- [2] L. Baum, T. Petrie, G. Soules, and N. Weiss. A maximization technique for statistical analysis of Markov chains. The Annals of Mathematical Statistics, 41(1):164–170, 1970.
- [3] H. Bensail, G. Celeux, A. Rafter, and C. Robert. Inference in model-based cluster. Statistics and Computing, 7(1):1–10, 1997.
- [4] C. Bieracki, G. Celeux, and G. Govaert. An improvement of the nec criterion for assessing the number of clusters in a mixture model. Pattern Recognition Letters, 20(3):267–272, 1999.
- [5] C. Bieracki, G. Celeux, and G. Govaert. Assessing a mixture model with integrated likelihood. IEEE Transactions on Pattern Analysis and Machine Intelligence, 22(7):719–725, 2000.
- [6] C. Bieracki, G. Celeux, and G. Govaert. Choosing values for the EM algorithm for getting the highest likelihood in multivariate Gaussian models. Computational Statistics & Data Analysis, 41(3):561–575, 2003.
- [7] J. Bilmes. A gentle tutorial of the EM algorithm and its parameter estimation for Gaussian mixture models. International Computer Science Institute, 4:126, 1998
- [8] C. M. Bish. Pattern Recognition and Machine Learning. Springer, 2006.
- [9] D. Blei and J. Lafferty. Topic models. In A. Srivastava and M. Sahami, Text Mining: Classification, Clustering, and Applications, Chapman and Hall/CRC Data Mining and Knowledge Discovery, Boca Raton, 2009.
- [10] D. M. Blei. Probabilistic topic models. Communications of the ACM, 55(4):77–84, 2012.
- [11] D. M. Blei, T. L. Griffiths, and M. I. Jordan. The nested restaurant process and Bayesian nonparametric inference of hierarchical topics. Journal of the ACM, 57(2), 2010.
- [12] D. M Blei and J. D. Lafferty. Dynamic topic models. In ICML, pages 113–120, 2006.
- [13] D. M. Blei and J. D. McAfee. Supervised topic models. In NIPS, 2007.
- [14] D. M. Blei, A. Y. Ng, and M. I. Jordan. Latent Dirichlet allocation. Journal of Learning Research, 3:993–1022, 2003.
