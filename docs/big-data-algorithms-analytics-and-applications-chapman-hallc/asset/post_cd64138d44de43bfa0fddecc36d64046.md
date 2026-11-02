
The second factor is retrieval time. We define t_r as the time cost for retrieval. In fact, t_r includes extraction time (extract the semantic information from the HBase) and the matching time (match the semantic similarity of the sample document with the stored documents).

### 3. Storage cost.
Because the HBase will store the map information, the storage cost will be taken into consideration. The rate of increase for storage p_s is defined as follows:

$p_s = s_{ont} / s_{org}$  (18.8)

where $s_{ont}$ is the size of semantic information of the multimedia documents and $s_{org}$ is the size of original multimedia documents,

$s_{ont} = \sum_{i=1}^{N} s_{ont}^{i}$    $s_{org} = \sum_{i=1}^{N} s_{org}^{i}$  (18.9)

## 18.4.3 Precision Ratio Evaluation
In the experiment, we first upload a multimedia document to the search engine to search for multimedia documents similar to it. The uploaded file will be annotated by some other users. After uploading the file in the interface, the system will search for all the records whose semantic information is similar to that of the sample document. The time cost includes extracting semantic information from the sample file and matching the semantic information with multimedia documents in HBase.

To measure the performance, we use the images, videos, audio, and text as the sample documents to execute the retrieval. For every sample type, we perform 10 different retrievals using 10 different documents, which are numbered from 01 to 10. The precision ratios are listed in Figure 18.8.

We can see from Figure 18.8 that our framework achieves good retrieval precision ratios. In order to demonstrate the performance of the heterogeneous retrieval, we specially record the precision ratios of using one type to search for the four types (e.g., use an image to search for images, videos, audio, and text documents). For every document type, we perform 10 different retrievals using 10 different sample documents and compute the average precision ratios. The average precision ratios are illustrated in Figure 18.9.

![](img/1643181e79c76dc765d55a7355afb4a4_406_0.png)
FIGURE 18.8 Precision ratios of 40 retrievals.

![](img/1643181e79c76dc765d55a7355afb4a4_407_0.png)
FIGURE 18.9 Average precision ratios of heterogeneous retrievals.

Figure 18.9 indicates that even in the retrieval process between different multimedia types, the precision ratios are not reduced. This is because this framework completely abandons physical feature extraction and executes the retrieval process based only on semantic information.

However, we cannot ignore that some traditional technologies supporting content-based retrieval have good performances too. For example, Google Images search actually can get perfect results reflecting users' intent in content-based image retrieval. However, it has the following disadvantages in comparison with this framework: (1) This search pattern cannot support heterogeneous retrieval, because of the physical feature extraction. (2) Compared with physical features, annotations can better represent the users' query intent, so our framework can get more accurate results in case of the semantic multimedia retrieval. If the documents contain more abundant annotations, the retrieval performance will be better. In addition, our framework has the advantage of good speed because of skipping the physical feature extraction.

## 18.4.4 Time and Storage Cost
In order to carry out the retrieval process, we have to perform several background processes whose time cost is t_b, which includes t_pre and t_ref. Table 18.2 shows the time cost of the background processes.

We can see from Table 18.2 that t_pre and t_ref will cost some seconds (t_b costs about 132 s for image type, 91 s for video type, 71 s for audio type, and 102 s for text type). However, the background processes are not always executed. In the server, the background process will be executed every 24 h in background thread, so this time cost can be acceptable.

TABLE 18.2 Time Cost of Background Processes (s)
| Multimedia Type | t_pre | t_ref | t_b |
|---|---|---|---|
| Image | 93 | 39 | 132 |
| Video | 63 | 28 | 91 |
| Audio | 52 | 19 | 71 |
| Text | 78 | 24 | 102 |

Now we will measure the retrieval time t_r. We specially record the time cost of 16 retrieval processes. For every document type (image, video, audio, and text), we perform four different retrievals (the samples are numbered from 01 to 04). In every retrieval, t_r will be recorded respectively. The detailed time cost of 16 retrieval experiments is listed in Figure 18.10.

![](img/1643181e79c76dc765d55a7355afb4a4_408_0.png)
FIGURE 18.10 Time cost of 16 retrievals.

Figure 18.10 shows that the semantic information extraction only costs a very short time; this is because we only need to read the sample document and directly extract the semantic segment from it. After the extraction, the retrieval process will be similar to the text-based retrieval, and Table 18.2 indicates that this process can be executed in acceptable time.

The storage cost will be taken into consideration because the HBase will store the semantic information. Table 18.3 shows the storage space cost.

TABLE 18.3 Storage Space Cost
| Multimedia Type | p_i (%) |
|---|---|
| Image | 1.56 |
| Video | 0.18 |
| Audio | 0.32 |
| Text | 15.23 |

We can see from Table 18.3 that the semantic information file size has almost not increased for image, video, and audio (p_i is about 1.56% for image, 0.18% for video, and 0.32% for audio type); this is because the semantic information is represented as text and the size of semantic files is small. However, the semantic information file size occupies 15.23% for text type; this is because the semantic information in a text file is abundant.

## 18.5 DISCUSSIONS AND CONCLUSIONS
In this chapter, a new approach supporting heterogeneous multimedia retrieval and reflecting users’ retrieval intent has been proposed. We designed the framework and described semantic annotation, ontology representation, ontology storage, a MapReduce-based retrieval process, and a performance evaluation model. Experiment results show that this framework can achieve good performance in heterogeneous multimedia retrieval reflecting the users’ intent.

In this framework, we only need to purchase some cheap computers to perform the semantic storage and retrieval process. Because investment in high-performance server hardware is more expensive than organizing cheap computers into a distributed computing environment, our framework can help us to reduce the cost of hardware investment.

Also, in our framework, we use some open-source tools such as Ubuntu Linux, Java SDK, and Hadoop tools. The operating system and software tools can be freely downloaded from the corresponding websites. This will save the investment of software. In addition, Apache Hadoop provides simplified programming models for reliable, scalable, distributed computing. It allows the distributed processing of large data sets across clusters of computers using simple programming models; the programmer can use Hadoop and MapReduce with low learning cost. Therefore, the investment cost is very economical for heterogeneous multimedia Big Data retrieval using our framework.

## ACKNOWLEDGMENTS
This work is supported by the Natural Science Foundation of China (61202341, 61103203) and the China Scholarship (201308430049).

## REFERENCES
- 1. K. Guo, J. Ma, G. Duan. DHSR: A novel semantic retrieval approach for ubiquitous multimedia. *Wireless Personal Communications*, 2013, 72(4): 779–793.
- 2. K. Guo, S. Zhang. A semantic medical multimedia retrieval approach using ontology information hiding. *Computational and Mathematical Methods in Medicine*, 2013, 2013(407917): 1–7.
- 3. C. Liu, J. Chen, L. Yang et al. Authorized public auditing of dynamic Big Data storage on cloud with efficient verifiable fine-grained updates. *IEEE Transactions on Parallel and Distributed Systems*, 2014, 25(9): 2234–2244.
- 4. J.R. Smith. Minding the gap. *IEEE MultiMedia*, 2012, 19(2): 2–3.
- 5. S. Ghemawat, H. Gobioff, S.T. Leung. The Google file system. *ACM SIGOPS Operating Systems Review*. ACM, 2003, 37(5): 29–43.
- 6. F. Chang, J. Dean, S. Ghemawat et al. Bigtable: A distributed storage system for structured data. *ACM Transactions on Computer Systems*, 2008, 26(2): 1–26, Article no. 4.
- 7. J. Dean, S. Ghemawat. MapReduce: Simplified data processing on large clusters. *Communications of the ACM*, 2008, 51(1): 107–113.
- 8. Apache Hadoop. Available at http://hadoop.apache.org/.
- 9. Apache HBase. Available at http://en.wikipedia.org/wiki/HBase.
- 10. R. Zhao, W.I. Grosky. Narrowing the semantic gap-improved text-based web document retrieval using visual features. *IEEE Transactions on Multimedia*, 2002, 4(2): 189–200.
- 11. Y. Yang, F. Nie, D. Xu et al. A multimedia retrieval architecture based on semi-supervised ranking and relevance feedback. *IEEE Transactions on Pattern Analysis and Machine Intelligence*, 2012, 34(4): 723–742.
- 12. A. Smeulders, M. Worring, S. Santini et al. Content-based image retrieval at the end of the early years. *IEEE Transactions Pattern Analysis and Machine Intelligence*, 2000, 22(12): 1349–1380.
- 13. G. Zhou, K. Ting, F. Liu, Y. Yin. Relevance feature mapping for content-based multimedia information retrieval. *Pattern Recognition*, 2012, 45(4): 1707–1720.
- 14. R.C.F. Wong, C.H.C. Leung. Automatic semantic annotation of real-world web images. *IEEE Transactions on Pattern Analysis and Machine Intelligence*, 2008, 30(11): 1933–1944.
- 15. A. Gijsenij, T. Gevers. Color constancy using natural image statistics and scene semantics. *IEEE Transactions on Pattern Analysis and Machine Intelligence*, 2010, 33(4): 687–698.
- 16. W. Lei, S.C.H. Hoi, Y. Nenghai. Semantics-preserving bag-of-words models and applications. *IEEE Transactions on Image Processing*, 2010, 19(7): 1908–1920.
- 17. T. Hofmann. Unsupervised learning by probabilistic latent semantic analysis. *Machine Learning*, 2001, 42(1–2): 177–196.
