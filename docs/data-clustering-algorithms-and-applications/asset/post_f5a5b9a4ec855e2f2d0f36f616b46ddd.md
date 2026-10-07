
# Contents

- 22.4.2.2 Relating Consensus Clustering to Other Optimization Formulations . . . . . . . . . . 562
- 22.4.3 Direct Approaches Using Cluster Labels . . . . . . . . . . . . 562
- 22.4.3.1 Graph Partitioning . . . . . . . . . . . . . . . . . 562
- 22.4.3.2 Cumulative Voting . . . . . . . . . . . . . . . . . 563
- 22.5 Applications of Consensus Clustering . . . . . . . . . . . . . 564
- 22.5.1 Gene Expression Data Analysis . . . . . . . . . . . . 564
- 22.5.2 Image Segmentation . . . . . . . . . . . . . . . 564
- 22.6 Concluding Remarks . . . . . . . . . . . . . . . . . 566

## 23 Clustering Validation Measures . . . . . . . . . . . . . . 571

- Hui Xiong and Zhonglou Li . . . . . . . . . . . . . . . . . . . . 572
- 23.1 Introduction . . . . . . . . . . . . . . . . . . . . . . 573
- 23.2 External Clustering Validation Measures . . . . . . . 574
- 23.2.1 An Overview of External Clustering Validation Measures . . . 575
- 23.2.2 Defective Validation Measures . . . . . . . . . 575
- 23.2.2.1 K-Means: The Uniform Effect . . . . . . . . 575
- 23.2.2.2 A Necessary Selection Criterion . . . . . . 576
- 23.2.2.3 The Cluster Validation Results . . . . . . . . 576
- 23.2.2.4 The Issues with the Defective Measures . . . . 577
- 23.2.2.5 Improving the Defective Measures . . . . . . 577
- 23.2.3 Measure Normalization . . . . . . . . . . . . . 577
- 23.2.3.1 Normalizing the Measures . . . . . . . . 578
- 23.2.3.2 The DCV Criterion . . . . . . . . . . . . 581
- 23.2.3.3 The Effect of Normalization . . . . . . 583
- 23.2.4 Measure Properties . . . . . . . . . . . . 584
- 23.2.4.1 The Consistency Between Measures . . . 584
- 23.2.4.2 Properties of Measures . . . . . . . . 586
- 23.2.4.3 Discussions . . . . . . . . . . . . 589
- 23.3 Internal Clustering Validation Measures . . . . 589
- 23.3.1 An Overview of Internal Clustering Measures 589
- 23.3.2 Understanding of Internal Clustering Validation Measures . . . 592
- 23.3.2.1 The Impact of Monotonicity . . . . . . 593
- 23.3.2.2 The Impact of Noise . . . . . . 594
- 23.3.2.3 The Impact of Density . . . . . . 595
- 23.3.2.4 The Impact of Subclusters . . . . . 596
- 23.3.2.5 The Impact of Skewed Distributions . . . . 598
- 23.3.2.6 The Impact of Arbitrary Shapes . . . . 600
- 23.3.3 Properties of Measures . . . . . . 600
- 23.4 Summary . . . . . . . . . . . . . . . 601

## 24 Educational and Software Resources for Data Clustering . . . . . . . 607

- Charu C. Aggarwal and Chandan K. Reddy . . . . . . . 607
- 24.1 Introduction . . . . . . . . . . . . . . . . . . 607
- 24.2 Educational Resources . . . . . . . . . . . . . . 608
- 24.2.1 Books on Data Clustering . . . . 608
- 24.2.2 Popular Survey Papers on Data Clustering . . . . 608
- 24.3 Software for Data Clustering . . . . . 610
- 24.3.1 Free and Open-Source Software . . . . . 610
- 24.3.1.1 General Clustering . . . . 610
- 24.3.1.2 Specialized Clustering . . . . 610
- 24.3.2 Commercial Packages . . . . . . . . . . . . . . . 611
- 24.3.3 Data Benchmarks for Software and Research . . . . . . 611
- 24.4 Summary . . . . . . . . . . . . . . . . . . . . . . . 612

# Index . . . . . . . ................................................. . . . . . . . . . 617

# Preface

The problem of clustering is perhaps one of the most widely studied in the data mining and machine learning communities. This problem has been studied by researchers from several disciplines over five decades. Applications of clustering include a wide variety of problem domains such as text, multimedia, social networks, and biological data. Furthermore, the problem may be encountered in many different scenarios such as streaming or uncertain clustering. Clustering is a diverse topic, and the algorithms generally depend on the data and problem.

Therefore, this book will focus on three primary aspects of data clustering. These include methods such as probabilistic clustering, density-based clustering, grid-based clustering, and spectral clustering. The second set of chapters will focus on order-based clustering, multimedia data, biological data, categorical data, network data, data streams and uncertain data. The third set of chapters will focus on detailed insights from the clustering process, because of the subjectivity of the clustering process, and the many ways in which the same data set can be clustered. How do we know that a particular clustering is good or that it solves the problem of application? There are numerous ways these issues can be explored. The exploration could be through interactive visualization and human interaction, external knowledge-based supervision, explicitly examining the multiple solutions in order to evaluate different possibilities, combining multiple solutions or to judge the quality of different solutions with different validation criteria.

The clustering problem has been addressed by a number of different communities such as pattern recognition, databases, data mining and machine learning. In some cases, the work by the different communities tends to be fragmented and has not been addressed in a unified way. This book will make a conscious effort to address the work of the different communities in a unified way. The book will start off with an overview of the basic methods in data clustering, and then progress more refined and complex methods for data clustering. Special attention will also be paid to more recent problem domains such as graphs and social networks.

The chapters in the book will be divided into three:

- **Method Chapters**: These chapters discuss the key techniques which are commonly used for clustering such as feature selection, agglomerative clustering, partitioning clustering, density-based clustering, probabilistic clustering, grid-based clustering, spectral clustering, and non-negative matrix factorization.
- **Domain Chapters**: These chapters discuss the specific methods used for different domains such as categorical data, text data, multimedia data, graph data, biological data, stream data, uncertain time series clustering, high-dimensional clustering, and big data. Many of these chapters can also be considered application chapters, because they explore the specific characteristics of the problem in a particular domain.
- **Variations and Insights**: These chapters discuss the key variations on the clustering process such as semi-supervised clustering, interactive clustering, multi-view clustering, cluster ensembles, and cluster validation. These methods are typically used in order to obtain detailed insights from the clustering process, and also to explore different possibilities on the process through either supervision, human interaction, or through automated generation of alternative clusters. The methods for cluster validation provide an idea of the quality of the clusters. This book is designed to be comprehensive in its coverage of the entire area, and it is hoped that it will serve students and researchers.

# Editor Biographies

Charu C. Aggarwal is a Research Scientist at IBM T. J. Watson Research Center in Yorktown, New York. He completed his B.S. from IIT Kanpur in 1993 and his Ph.D. from Massachusetts Institute of Technology in 1996. His research interest during his Ph.D. years was in combinatorial optimization (network flow), and his thesis advisor was James B. Orlin. He has worked in the field of performance analysis, databases, and data mining. He has published over 200 papers in referred conferences and journals, and has applied for or granted 80 patents. He is an author or editor of many books, including this one. For the aforementioned patents, he has thrice designated a Master Inventor at IBM. He is a recipient of the IBM Corporate Award (2003) for his work in data streams, a recipient of the IBM Innovation Award (2008) for his scientific contributions to privacy technology, and a recipient of the IBM Research Division Award (2008) for his scientific contributions to data stream research. He has served on the program committees of most major database/data mining conferences, and served as program vice-chairs of the SIAM Conference on Data Mining (2007), the IEEE ICDM Conference (2007), the WWW Conference (2009), and the IEEE ICDM Conference (2009). He has served as an associate editor of the IEEE Transactions on Knowledge and Data Engineering Journal from 2004 to 2008. He is an associate editor of the ACM TKDD Journal, an action editor of the Data Mining and Discovery Journal, an associate editor of ACM SIGKDD Explorations, and an associate editor of the Knowledge and Information Systems Journal. He is a fellow of the IEEE for “contributions to knowledge discovery and data mining,” and a member of the ACM.

Chandan K. Reddy is an Assistant Professor in the Department of Computer Science at Wayne State University. He has his Ph.D. from Cornell University and M.S. from Michigan State University. His primary research interests are in the areas of data mining and machine learning with applications to healthcare, bioinformatics, and social network analysis. His research is funded by the National Science Foundation, the National Institutes of Health, Department of Transportation, and the Susan G. K for Cure Foundation. He has published over 40 peer-reviewed articles in leading conferences and journals. He received the Best Application Paper Award at the ACM SIGKDD conference in 2010 and was a finalist of the INFORMS Franz Edelman Award Competition in 2011. He is a member of IEEE, ACM, and SIAM.
