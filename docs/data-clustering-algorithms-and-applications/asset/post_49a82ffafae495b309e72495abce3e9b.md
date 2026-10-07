
## Document Clustering: The Next Frontier

segment-based document clustering leads to cluster descriptions that are more “useful” according to a number of aspects, including higher coherence of terms within a description, higher presence of discriminating terms, and wider coverage of topics.

Clustering legal documents. Lu et al. [70] apply a similar clustering strategy in the legal domain, where documents with multiple topics are very common. They develop a highly scalable soft clustering system centered around a topic segmentation-based clustering framework that also incorporates metadata information. The process of identifying issue-based clusters is broken down into three logical steps: (1) build a universe of legal issues (topics) to search, (2) identify relevant documents for each issue in the topic universe, and (3) associate each document in the collection with one or more issues.

The document segmentation leverages available metadata for the document collection. In particular, the algorithm represents a headnote, a brief summary of points within a document, as a compound vector with four different features: a frequency vector for the text in the headnote, a frequency vector of noun phrases, a vector of codes for legal taxonomy, and a citation network for the headnote. The similarity between two headnotes is computed as the weighted sum of their respective feature vectors, with historically determined weights. The cosine similarity with tf-idf weighting is used for comparing the first two features, and an analogous method is used for the third. Citation features are compared in terms of co-citations.

```
cite~(h_i, h_j) = cite(h_i \cap h_j)
```

where cite(h_i \cup h_j) is the number of documents containing at least one headnote, and cite(h_i \cap h_j) is the number of documents in which both h_i and h_j are cited. The use of noun phrases as a feature set is motivated by an in-house study that found to be closely related to legal concepts, which form the basis for topics in this domain.

Headnotes in each document are clustered using an agglomerative clustering algorithm employing an automatic stopping procedure. The algorithm merges clusters by maximizing the ratio of intracluster and intercluster similarity, dubbed the intraparticle similarity threshold, and does not require the number of clusters as input. The intraparticle similarity threshold is determined heuristically. The resulting clusters are considered topics within the document.

Given the large size of the topic set, the authors use dimensionality reduction to reduce the computational complexity of the next. To obtain a unique set of collection documents, document topics are clustered using a “canopy”-based soft clustering technique. A document classification engine and a support vector machine (SVM) are used to retrieve topics to some seed, the top rank of which are merged with the seeds. Similarity is extended for this step in the framework to include inclusion scores and co-similarity. The algorithm is executed recursively, using the output of each round after the first execution of the next, until intercluster similarity between any two clusters is below a threshold. The resulting clusters represent the most important topics within the collection.

The last step associates the collection documents with the discovered topics. For this, the main document text is segmented and documents are assigned to clusters based on their similarity with the clusters. The quality of the resulting-based clustering was validated by human legal experts in multiple test cases.

A statistical model. Clustering segmented documents is not limited to VSM techniques. Ponti et al. [84] describe a statistical model for topically segmented documents and provide a clustering strategy for documents modeled this way. The key idea of their work is a generative model that exploits the decomposition of documents into segments is to better capture dependencies among terms, alleviating some of the problems related to the bag-of-words assumption in large multi-topic documents.

## Data Clustering: Algorithms and Applications

![](img/b94d85a2e934001944bcc21abd9a9943_346_0.png)

FIGURE 13.5: Plate notation for the SGM generative model.

Term generation in such a model should be related not only to topics but also to segments. As a consequence, the latent variable that models topics should be directly associated with the within-document segments, rather than to the document as a whole. Whose Segment-based Generative Model (SGM), a model that explicitly considers segments within each document by introducing a segment model variable in the generative process. SGM assumes that each document $d \in \mathcal{D}$ is a sequence of $n_d$ words and, at the same time, a set $S_d$ of contiguous, nonoverlapping blocks, or segments. The segmentation strategy is decoupled from SGM, the authors using Textiling in their implementation, utilizes latent variable $z$ to model topic distributions and the model variable $s$ to represent document segments. Figure 13.5 illustrates the graphical model representation of SGM. The generative process by SGM on a corpus $D$ of segmented documents can be summarized as follows:

- 1. Select a document from $\mathcal{D} \Rightarrow Pr(d)$
- 2. For each segment $s \in S_d$
  a. Choose a topic $z$ for the document, $d \Rightarrow Pr(z|d)$
  b. Associate topic-segment probability for segment $s, z \Rightarrow Pr(s|z)$
  c. For each word $w$ in the segment $s \Rightarrow Pr(w|z,s)$

SGM provides a fine-grained document-to-topic modeling by taking into account segments. Choosing a $Pr(z|d)$ in the generative process is based on the topic-segment association $Pr(s|z)$, intuitively providing a topical affinity for segment given a selected topic. Words are generated not only by topics, but also by segments $Pr(w|z,s)$.

$Pr(d,s,w) = \sum_{z \in \mathcal{Z}} Pr(d) Pr(z|d) Pr(s|z) Pr(w|z,s)$

Ponti et al. use Expectation-Maximization (EM) to estimate cluster parameters. The resulting-based clustering could be induced from P by assigning documents to the cluster(s) for which their values are highest. The quality of the resulting-based clustering was validated by human legal experts in multiple test cases. The resulting clusters are considered topics within the document. The merging criterion determines the cluster hierarchy. The algorithm stops when the desired number of clusters is reached.

## Document Clustering: The Next Frontier

**Extending the topic space.** Wang et al. propose Matrix Space (MSM) [110], where each document is represented as topic-segmented text. Segments are then considered as tf-idf frequency. The document-topic probability matrix P where P_ij = Pr(z|d_i) is the size of the document. Given the large of of,, the the constrained problem,

```
min
  sum_{i=1}^n ||A_i - LM_i^T||_F^2
  L \in R^{m \} l} 0
  R \in R^{s \times l} 0
  M_i \in R^{l \times 1} 0
```

where ||·||_F is the standard Frobenius norm and n is the number of documents. In the reconstruction, LM is associated with the documents, while M_i^T is the size of topics.

## 14.3 Simultaneous Identification and Clustering

Assuming the previous definition of segments as topically coherent blocks of text in a document, segment identification boils down to finding the document topics. **Co-clustering in the latent space.** Latent Dirichlet Co-Clustering (LDCC) is an extension of LDA that simultaneously clusters words and documents. By focusing on meaningful segments of text, LDCC is more likely to assign adjacent documents to coherent topics. LDCC extends LDA by assuming each document is a random mixture of topics, which turn into distributions. Segments are then modeled as LDA: for each segment, a distribution over collection topics is sampled from a Dirichlet distribution; a topic is then selected according to this distribution for each segment; each term is finally sampled from a multinomial distribution over specific terms of the selected topic. Figure 13.6(a) depicts the plate notation representation of the LDCC model, whose generation process for each segment is detailed below.

+ 1. Choose the number of segments for document d_i, S_i \sim Poisson(\phi)
- 2. Generate document topics, \mu_i \sim Dir(\delta)
- 3. For each s_ij of the segments in document d_i
  a. Choose a random topic for the segment, y_ij \sim Multi(\mu_i)
  b. Choose number of words for the segment, N_ij \sim Poisson(\phi)
  c. Generate segment topic proportions, \theta_{ij} \sim Dir_K(\alpha_i,y_{ij})
