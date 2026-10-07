
## Document Clustering: The Next Frontier

![](img/b94d85a2e934001944bcc21abd9a9943_353_0.png)

**FIGURE 13.7:** Plate notation for the $\alpha$-DLDA (a) and $\gamma$-DLDA (b) generative models.

simultaneous training of two LDA models, the **target** model on the short texts and the **auxiliary** model on the long ones.

Depending on how the models are related to each other, Jin et al. [55] propose two sets of topics for auxiliary and target data and asymmetric Dirichlet priors to control the relative importance of when generating a document. $\alpha'$ is given higher values for entries associated with auxiliary topics. $\gamma$-DLDA introduces a document-binary switch that constraints each document to be generated from either the target model or from the auxiliary. In addition to the multinomial distributions over topics, each document is also associated with a multinomial distribution over target or auxiliary topics with a Beta prior $\gamma$. Similar to a parameter in $\alpha$-DLDA, $\gamma$ is given higher values for entries associated with target topics. Figure 13.7 (b) depicts the plate notation for the $\gamma$-DLDA model, whose generation for each document is detailed below.

1. For each target topic, generate a multinomial distribution over terms, $\beta'_k \sim Dir_M(\eta')$, $k \in \{1, \dots, K^*\}$
2. For each auxiliary topic, generate a multinomial distribution over terms, $\beta''_k \sim Dir_M(\eta'')$, $k \in \{1, \dots, K^*\}$
3. For each corpus (auxiliary and target data), $c \in \{a, t\}$
   a. For each corpus document $d_i$, $i \in \{1, \dots, N^c\}$
      i. Generate a multinomial distribution over target topics, $\theta'_i \sim Dir_K(\alpha')$
      ii. Generate a multinomial distribution over auxiliary topics, $\theta''_i \sim Dir_K(\alpha'')$
      iii. Generate a multinomial distribution over target, auxiliary topics, $\pi_i \sim Beta(\gamma)$
      iv. For each word $w_{ij}$ in document $d_i$:
         1. Choose a value for $x_{ij} \sim Binomial(\pi_i)$
         2. If $x_{ij}=t$, choose a target topic $z_{ij} \sim Multi(\theta'_i)$
         3. If $x_{ij}=a$, choose an auxiliary topic $z_{ij} \sim Multi(\theta''_i)$
         4. Choose word $w_{ij}$ from topic $z_{ij}$, i.e., $w_{ij} \sim Multi(\beta_{z_{ij}})$

Jin et al. [55] compare their DL algorithms against direct clustering with CLUTO, topic model-based clustering on the individual collections and against several algorithms that transfer knowledge from the long texts when clustering the short. While $\alpha$-DLDA and $\gamma$-DLDA outperformed the competition, the authors also note that methods utilizing long texts performed significantly better than the others, demonstrating the value of external information when noisy short documents.

## 13.6 Conclusion

This chapter primarily focused on reviewing some recently developed text clustering methods that are specifically suited for long and short document collections. These types of document collections introduce new sets of challenges. Long documents are by their nature multi-topic and as such the document clustering methods must explicitly focus on modeling and/or accounting for these purposes. On the other hand, short documents often contain domain-specific vocabulary which are noisy, and proper modeling/understanding requires the incorporation of external information. We strongly need research in clustering long and short documents is in its early stages and many new methods will be developed in the years to come. Moreover, real datasets are composed of not only standard long, or short documents, but rather documents of mixed length. Current scholarship lacks studies on these types of data. Since different methods are often used for clustering standard, long, or short documents, new methods or frameworks should be investigated to address mixed collections.

Traditional document clustering is also faced with new challenges. Today's very large, high-dimensional document collections often lead to faced valid solutions. Subspace/projective clustering approaches [63, 77] have been used to cope with high dimensionality when performing the clustering task. Ensemble clustering [36] and multiview/alternative clustering approaches [54, 86], which aim to summarize or detect different clustering solutions, have been used to manage the availability of possible, alternative clusters for a given dataset. Relatively little work has been done in document clustering to take advantage of lessons learned from these methods. Integrating subspace/ensemble/multiview clustering with topic models or segmentation may lead to developing the next-generation clustering methods specialized for the document domain.

Some topics that we have briefly touched on in this article are further detailed in other chapters of this book. Other topics relate to clustering documents, such as semisuvised clustering, stream document clustering, parallel clustering algorithms, and kernel methods for dimensionality reduction or clustering, were left for further study. Interested readers may consult document clustering surveys by Aggarwal and Chai [2], Andrews and Fox [6], and Steinbach al. [99].

## Bibliography

- [1] Charu C. Aggarwal, Stephen C. Gates, and Philip S. Yu. On the merits of building categorization systems by supervised clustering. In Proceedings of the Fifth ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, KDD '99, pages 352–356, New York, USA, 1999. ACM.
- [2] Charu C. Aggarwal and Chai. A survey of document clustering. Data Mining, 13(1):77–128, 2010.
- [3] Nicholas O. Andrews. Faster dimension reduction. Communications of the ACM, 53(2):197–204, 2012.
- [4] Abdelmalek. A framework for personalized search results. Information Technology, 394–401, 2008.
- [5] Chaitanya Chemudugunta, Padhractic Smyth, and Mark Steyers. General and specific aspects of documents with a probabilistic topic model. In Advances in Neural Information Systems 19, NIPS '06, pages 241–248, 2006.
- [6] Nicholas C. Andrews and Edward A. Fox. Recent developments in clustering. Technical report, 2007.
- [7] Markus Kriegel. OPTICS: Overlapping points to identify structure.MOD, 28(2):49–60, 1999.
- [8] Somnath Banerjee, Krishna Ramanathan, and Ajay Gupta. Clustering short texts. In Proceedings of the 30th ACM SIGIR Conference on Research and Development in Information Retrieval, SIGIR '07, pages 787–788, 2007.
- [9] Steinbach al. Generalized discriminant analysis using a kernel approach. Neural Computation, 10(12):2385–2404, 2000.
- [10] William B. Cavnar. Using an n-gram-based document representation with a vector processing retrieval model. In Text Retrieval Conference (TREC-3), pages 269–278, 1994.
- [11] David M. Blei. Probabilistic topic models. Communications of the ACM, 55(4):77–84, 2012.
- [12] David M. Blei, Thomas L. Griffiths, and Michael I. Jordan. The nested restaurant process and Bayesian nonparametric inference of hierarchies. Journal of the ACM, 57(2):1:30, 2010.
- [13] David M. Blei, Andrew Y. Ng, and Michael I. Jordan. Latent Dirichlet allocation. Journal of Machine Learning, 3:993–1022, 2003.
- [14] Daniel Boley. Political divisive partitioning. Data Mining and Knowledge Discovery, 2(4):325–344, 1998.
- [15] Thorsten Barth, Francine Chen, and Ioannis Tsochandaridis. Topic-based document segmentation with probabilistic semantic analysis. In Proceedings of the 11th ACM CIKM International Conference on Information and Knowledge Management, CIKM '02, pages 211–218, 2002.
- [16] Claudio Carpinet, Stanislaw Osiński, Giovanni Romano, and David Weiss. A survey of web clustering engines. ACM Computing Surveys (CSUR), 41(3):1–38, 2009.
- [17] Claudio Carpinet and Giovanni Romano. Optimal search results clustering. In Proceedings of the 33rd ACM SIGIR Conference on Research and Development in Information Retrieval, SIGIR '10, pages 170–177, New York, USA, 2010. ACM.
- [18] Moreno Caputo, Elisabeth Bianchi, and Ignacio Gallo. An online document clustering for short web texts. Pattern Recognition Letters, 30(10):870–876, 2009.
- [19] William B. Cavnar. Using an n-gram-based document representation with a vector processing retrieval model. In Text Retrieval Conference (TREC-3), pages 269–278, 1994.
- [20] Chaitanya Chemudugunta, Padhractic Smyth, and Mark Steyers. General and specific aspects of documents with a probabilistic topic model. In Advances in Neural Information Systems 19, NIPS '06, pages 241–248, 2006.
