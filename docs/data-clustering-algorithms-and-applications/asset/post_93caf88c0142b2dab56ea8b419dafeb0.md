
# Data Clustering: Algorithms and Applications

![](img/b94d85a2e934001944bcc21abd9a9943_342_0.png)

FIGURE 13.4: Plate notation for the STM (a) and LDSeq (b) generative models.

dimensionality $K$ of the topic space (and thus of the Dirichlet distribution from which areas is assumed). The parameter $\beta$ is drawn as a $K \times M$ random matrix, where each row $\theta_k$ is drawn from an exchangeable Dirichlet distribution and as one mixture component. This view of $\beta$ is shared by STM and all other LDA-based models.

STM extends the LDA model by adding an additional layer in deriving word–topic proportions $\theta$, which effectively correlates document topics with segments, modeling the topic structure within a documented segment. While LDA samples $\theta$ at the document level $(\theta_d \sim Dir(\alpha_d))$, STM extends document-level proportions $(\mu_i)$ to the segment level $(\theta_{ij})$ with the aid of the two-parameter Poisson-Dirichlet Process (PDP). Du et al. [29] posit the following approximations on distributions, which enable this,

> $PDP(0, b, discrete(\theta)) \approx Dir(b\theta)$;
> $PDP(a, 0, discrete(\theta)) \approx Dir(a)$

where $a$ and $b$ are PDP construct and strength parameters and $a \rightarrow 0$. They justify the first approximation because the mean and first central moments of the LHS and RHS are equal, and the second approximation by an agreement to $O(a^2)$ in the error and first two central moments of the two sides. Since PDP is a prior conjugate to multinomial likelihoods, replacing the Dirichlet distribution with PDP allows the authors to use Collapsed samplers in the STM inference, greatly reducing computational complexity. Figure 13.4 depicts the plate notation representation of the STM model, whose generation process for each document is detailed below.

1. Generate document topic proportions, $\mu_i \sim Dir_K(\delta)$
2. For each segment $s_{ij}$ in document $d_i$
   a. Generate segment topic proportions, $\theta_{ij} \sim PDP(a, b, \mu_i)$
   b. For each word $w_{ijt}$ in segment $s_{ij}$
      i. Choose a topic $z_{ij} \sim Mult_K(\theta_{ij})$
      ii. Choose word $w_{ij} \sim Mult_M(\beta_{ij})$

STM is also similar to LDCC, a four-level probabilistic model that considers documents and segments as mixtures over latent topics. Unlike STM, LDCC considers documents and segments as random kinds of topics and associates a segment with a single topic. By using a single pool for both documents and segments, STM better model the structure of a normal document, in which document topics are a superset of the segment topics in the document. Similarly, segments can at times enhance multiple topics, e.g., a passage by Ludwig Beethoven’s Violin Concerto in D major can draw from topics related to violins, musical performance, and the life of Beethoven. By assuming segments have a topic distribution, STM allows them to share multiple topics. In contrast, LDCC assigns a specific topic to each segment. LDCC will be presented in more detail in Section 13.4.3.

**Consecutive segments.** Du et al. also propose Sequential LDA (LDSeq) [30], an extension of STM that addresses the bag of segments document clustering. Considering segment order in a document, the topic distribution of segment in LDSeq is dependent on that of the previous segment. The first segment, which does not have an ancestor, has a topic distribution dependent on the document topic distribution. Figure 13.4 (b) depicts the topic representation of the LDSeq model, whose generation process for each document is detailed below.

1. Generate document topic proportions, $\theta_{i0} = \mu_i \sim Dir(\delta)$
2. For each segment $s_j$ in document $d_i$
   a. Generate segment topic proportions, $\theta_{ij} \sim PDP(a, b, \theta_{i,j-1})$
   b. For each word $w_{ijk} \sim Multinomial(\theta_{ij})$
      i. Choose a topic $z_{ijk} \sim Multinomial(\beta_{ij})$

While documents are segment sets in STM, LDSeq sees them as sequences of documents. Du et al. [30] take advantage of the fact that the PDP is self-configuring, allowing them to model progressive dependency via a nested PDP, i.e., the PDP of the current segment sets the previous segment as base ($\theta_{ij} \sim PDP(a, b, \theta_{i,j-1})$). This assumption may not be appropriate for all tasks, but it showcases, the popularity and extensibility of the LDA model. LDCC is also related to the LDSeq model, an extension of LDCC model that follows a Markovian relationship between distributions of consecutive segments. LDSeq will be presented in more detail in Section 13.4.

## 13.4.2 Clustered Segment Documents

Using techniques outlined above, a multi-document document can be decomposed into segments that correspond to thematically coherent text passages in the original document. Segmentation can be used as a base step in long document clustering.

**Segment-based document clustering.** Tagarelli and Karypus [130] propose a framework for clustering of multi-topic document.

# Data Clustering: Algorithms and Applications

The segment-based views over the documents allow for an effective identification of overlapping clustering solutions, and the authors’ proposed segment-level overclustering improves the quality of both disjoint and overlapping clustering solutions. They also find that
