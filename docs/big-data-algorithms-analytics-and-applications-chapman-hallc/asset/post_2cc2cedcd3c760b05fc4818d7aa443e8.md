
We implemented CoGRS in Hadoop-0.20.2 and tested it on a private cloud as well as on Amazon Elastic Compute Cloud (EC2). As compared to native Hadoop, our results show that CoGRS minimizes off-rack network traffic by an average of 9.6% and 38.6% on our private cloud and on an Amazon EC2 cluster, respectively. This reflects on job execution times and provides an improvement of up to 23.8%.

Partitioning skew refers to the significant variance in intermediate keys' frequencies and their distribution across different data nodes. In essence, a reduce task scheduler can determine the pattern of the communication traffic in the network, affect the quantity of shuffled data, and influence the runtime of MapReduce jobs.

### 7.4.4 The Source of MapReduce Skews

Over the last few years, MapReduce has become popular for processing massive data sets. Most research in this area considers simple application scenarios like log file analysis, word count, and sorting, and current systems adopt a simple hashing approach to distribute the load to the reducers. However, processing massive amounts of data exhibits imperfections to which current MapReduce systems are not geared. The distribution of scientific data is typically skewed [20]. The high runtime complexity amplifies the skew and leads to highly varying execution times of the reducers.

There are three typical skews in MapReduce.
- Skewed key frequencies—If some keys appear more frequently in the intermediate data tuples, the number of tuples per cluster owned will be different. Even if every reducer receives the same number of clusters, the overall number of tuples per reducer received will be different.
- Skewed tuple sizes—In applications that hold complex objects within the tuples, unbalanced cluster sizes can arise from skewed tuple sizes.
- Skewed execution times—If the execution time of the reducer is worse than linear, processing a single large cluster may take much longer than processing a higher number of small clusters. Even if the overall number of tuples per reducer is the same, the execution times of the reducers may differ.

According to those skew types, we propose several processes to improve the performance of MapReduce.

### 7.4.5 Reduce Placement in Hadoop

In Hadoop, map and reduce tasks typically consume a large amount of data, and the total intermediate output (or total reduce input) size is sometimes equal to the total input size of all map tasks (e.g., sort) or even larger (e.g., 44.2% for K-means). For this reason, optimizing the placement of reduce tasks to save network traffic becomes very essential for optimizing the placement of map tasks, which is already well understood and implemented in Hadoop systems.

This section explores scheduling to ensure that the data that a reduce task handles the most are localized, so that it can save traffic cost and diminish data skew [21].

Sampling—Input data are loaded into a file or files in a distributed file system (DFS), where each file is partitioned into smaller chunks, called input splits. Each split is assigned to a map task. Map tasks process splits [22] and produce intermediate outputs, which are usually partitioned or hashed to one or many reduce tasks. Before a MapReduce computation

Data contain a wealth of biological information, including significant gene expression situations and protein–protein interactions. What is more, a disease network, which contains hidden information associated with the disease and gives biomedical scientists the basis of hypothesis generation, is constructed based on disease relationship mining in these biomedical data.

However, the most basic requirements for biomedical Big Data processing are difficult to meet efficiently. For example, key word searching in biomedical Big Data or the Internet can only find lots of relevant file lists, and the accuracy is not high, so that a lot of valuable information contained in the text cannot be directly shown to the people.

### 7.5.2 Biomedical Text Mining and NER

In order to explore the information and knowledge in biomedical Big Data, people integrate mathematics, computer science, and biology tools, which promote the rapid development of large-scale biomedical text mining. This refers to the biomedical Big Data analysis process of deriving high-quality information that is implicit, previously unknown, and potentially useful from massive biomedical data.

Current research emphasis on large-scale biomedical text mining is mainly composed of two aspects, that is, information extraction and data mining. Specifically, it includes biomedical named entity recognition (Bio-NER), relation extraction, text classification, and an integration framework of the above work.

Bio-NER is the first and an important and critical step in biomedical Big Data mining. It aims to help molecular biologists recognize and classify professional instances and terms, such as protein, DNA, RNA, cell_line, and cell_type. It is meant to locate and classify atomic elements with some special significance in biomedical text into predefined categories. The process of Bio-NER systems is structured as taking an unannotated block of text and then producing an annotated block of text that highlights where the biomedical named entities are [25].

However, because of lots of unique properties in the biomedical area, such as unstable quantity, nonunified naming rules, complex form, the existence of ambiguity, and so on, Bio-NER is not mature enough, especially since it takes much time. Most current Bio-NER systems are based on machine learning, which needs multiple iterative calculations from corpus data. Therefore, it is computationally intensive and seriously increases recognition time, including model training and inference. For example, it takes almost 5 hours for the CRF model training process using the Genia4ER training corpus, which is only about 14 MB [26]. How do we deal with huge amounts of biomedical text data? How do we cope with the unbearable wait for recognition for a very long time? It is natural to seek distributed computing and parallel computing to solve the problem.

### 7.5.3 MapReduce for CRFs

CRFs are an important milestone in the field of machine learning, put forward in 2001 by John Lafferty et al. [27]. CRFs, a kind of discriminant model and an undirected graph model at the same time, define a single logarithmic linear distribution for a joint probability of an entire label sequence based on a given particular observation sequence. The
model is widely used in natural language processing (NLP), including NER, part-of-speech tagging, and so on.

Figure 7.6 shows the CRF model, which computes the conditional probability $p(\vec{y}|\vec{x})$ of an output sequence $\vec{y}=(y_1,y_2,\ldots,y_n)$ under the condition of a given input sequence $\vec{x}=(x_1,x_2,\ldots,x_n)$.

A linear CRF, which is used in Bio-NER, is as follows:

$$P(\vec{y}|\vec{x}) = \frac{1}{Z(\vec{x})} \exp \sum_{i=1}^{n} \sum_{k=1}^{K} \lambda_k f_k(\vec{x}, i, y_{i-1}, y_i), \qquad (7.4)$$

where

$$Z(\vec{x}) = \sum_{\vec{y}} \exp \sum_{i=1}^{n} \sum_{k=1}^{K} \lambda_k f_k(\vec{x}, i, y_{i-1}, y_i), \qquad (7.5)$$

$i$ is the position in the input sequence $\vec{x}=(x_1,x_2,\ldots,x_n)$, $\lambda_k$ is a weight of a feature that does not depend on location $i$, and $\{f_k(\vec{x},i,y_{i-1},y_i)\}_{k=1}^{K}$ are feature functions.

For the training process of the CRF model, the main purpose is to seek for the parameter $\lambda=(\lambda_1,\lambda_2,\ldots,\lambda_K)$ that is most in accordance with the training data $T=\{(\vec{x}_i,\vec{y}_i)\}_{i=1}^{N}$. Presume every $(\vec{x},\vec{y})$ is independently and identically distributed. The parameter is obtained generally in this way:

$$L(\lambda)=\sum_i \log P(y^i|x^i). \qquad (7.6)$$

When the log-likelihood function $L(\lambda)$ reaches the maximum value, the parameter is almost the best. However, to find the parameter to maximize the training data likelihood, there is no closed-form solution. Hence, we adopt parameter estimation, that is, the limited-memory Broyden–Fletcher–Goldfarb–Shanno (L-BFGS) algorithm [28], to find the optimum solution.

![](img/1643181e79c76dc765d55a7355afb4a4_170_0.png)

FIGURE 7.6 Linear CRFs.
