
# 190 Cloud Computing and Digital Media

Zhang, Jing, Xianglong Liu, Junwu Luo, and Bo Lang. "DIRS: Distributed image retrieval system based on MapReduce." 5th International Conference on Pervasive Computing and Applications. December 1–3, IEEE, Maribor, Slovenia, pp. 93–98, 2010.

Zhao, Jun, Zhu Liang, and Yong Yang. "Parallelized incremental support support vector machines based on MapReduce and bagging technique." IEEE International Conference on Information Science and Technology. March 23–25, Hubei, 2012.

Zhu, Qisha, Lin Lin, and Mei-Lin Shu. "Correlation maximization-based discretization for supervised classification," International Journal of Business Intelligence and Data Mining 7: 40–59, 2012.

Zhu, Qisha, Lin Lin, Mei-Lin Shu, and Shu-Chu Chen. "Feature selection using correlation and reliability based scoring metric for video semantic detection." 4th IEEE International Conference on Semantic Computing. September 22–24, IEEE, Pittsburgh, PA, pp. 462–469, 2010.

Zhu, Qisha, Lin Lin, Mei-Lin Shu, and Shu-Chu Chen. "Effective supervised discretization for classification based on correlation maximization." The 12th IEEE International Conference on Information Reuse and Integration. August 3–5, IEEE, Las Vegas, NV, pp. 390–395, 2011.

Zhu, Qisha, Mei-Lin Shu, and Shu-Chu Chen. "Discriminative learning assisted video semantic concept classification." In Multimedia Security: Watermarking, Steganography, and Forensics, edited by Frank Snih. Boca Raton, FL: CRC Press, pp. 31–49, 2013.

# Efficient Join Query Processing on the Cloud

Xiaofe Zhang and Lei Chen
Hong Kong University of Science and Technology
Hong Kong, China

# CONTENTS

- 9.1 Introduction 192
- 9.2 Background 195
- 9.2.1 MapReduce Essentials 195
- 9.2.2 A Cost Model of Join Processing Using MapReduce 196
- 9.2.3 Multiway Join Processing Using MapReduce 199
- 9.3 Case Study 1: Multiway Theta-Join Processing 200
- 9.3.1 Solution Overview 201
- 9.3.2 Problem Definition 202
- 9.3.3 Cost Model 206
- 9.3.4 Join Algorithm 208
- 9.3.4.1 Multiway Theta-Join Processing with Single MRJ 208
- 9.3.5 Summary 214
- 9.4 Case Study 2: SPARQL Query Processing 214
- 9.4.1 RDF and SPARQL Query 215
- 9.4.1.1 RDF Data Model 215
- 9.4.1.2 SPARQL Queries 215
- 9.4.2 SPARQL Evaluation Using MapReduce 217
- 9.4.3 Solution Overview 218
- 9.4.4 Problem Definition 219
- 9.4.5 Query Processing 221
- 9.4.5.1 MRJ Identification and Ordering 221
- 9.4.5.2 Join Strategies and Optimization 226
- 9.4.6 Implementations 226
- 9.4.6.1 System Design 226
- 9.4.6.2 Preprocessing Updates 227
- 9.4.7 Related Work 228
- 9.4.8 Summary 230

References

JOIN QUERY is one of the most expensive and expensive analytic tools in traditional database systems. Along with the exponential growth of various data collections, NoSQL data storage has risen as the prevailing solution for big data. However, without the strong support of heavy index, the join operator becomes even more and challenging for querying against or from massive data. As reported from Facebook [1] and Google [2], the underlying data volume is hundreds of terabytes or even petabytes. In these scenarios, solutions from the traditional distributed or parallel databases are infeasible due to unsatisfactory scalability and poor fault tolerance. There have been intensive studies on different types of join operations over distributed data, for example, similarity join, set join, fuzzy join, all of which focus on efficient join query by exploring the massive parallelism of the MapReduce computing framework on the cloud platform. In this chapter, we explore the efficient processing of multiway generalized join queries, namely the “complex join,” which are widely employed in various practical analytic scenarios, that is, querying resource description framework (RDF), feature selection from biochemical data. The substantial change of complex join lies in, given a number of processing units, mapping a complex query to a number of parallel tasks and having them executed in a well-scheduled sequence that the total processing time span is minimized. In this chapter, we focus on the evaluation of complex join queries on the cloud platform and elaborate with case studies on the efficient Simple Protocol and RDF Query Language (SPARQL) query processing and the multiway theta-join evaluation.

# 9.1 INTRODUCTION

Multiway join is an important and frequently used operation for numerous applications including knowledge discovery and data mining. Since the join operation is expensive, especially on large datasets and/or in multidensions, multiway join becomes even more a costly operation. Although some researchers have devoted to the efficient evaluation of different types of pairwise joins, surprisingly few efforts have been made on the evaluation strategy of multiway join queries. Especially, with the fast increase in the scale of the input datasets, processing large data in a parallel and distributed fashion is becoming a popular practice. Even though a number of parallel algorithms for equi-joins in relational engines in MapReduce have been designed and implemented, there has little work on parallel evaluation of multiway joins in large data, which is a challenging task and becoming increasingly essential as datasets continue to grow at an exponential rate.

When dealing with extreme-scale data, parallel and distributed computing using shared-nothing clusters, which typically consist of a number of commodity machines, is quickly becoming a dominating trend. MapReduce was introduced with the goal of providing a simple yet powerful parallel and distributed computing paradigm. The MapReduce architecture also provides good scalability and fault tolerance mechanisms. In the past few years, there has been an increasing support for MapReduce from both industry and academia, making it one of the most actively utilized frameworks for parallel and distributed processing of large data today.

Moreover, the (key,value)-based MapReduce programming model guarantees great scalability and strong fault tolerance property. It has emerged as the most popular processing paradigm in a shared-nothing computing environment. Recently, devoting efforts towards an efficient and effective analytic processing over immense data have been made within the MapReduce framework. Currently, the database community mainly focuses on two issues: (1) the transformation from certain relational algebra operator, such as similarity join, to this (key,value)-based parallel implementation and (2) the tuning or redesign of the transformation function that the MapReduce job is executed more efficiently in terms of less time cost or computing resources consumption. Although relational operators, as pairwise theta-join, fuzzy join, and aggregation operators, are evaluated and implemented using MapReduce, there is little effort exploring the efficient processing of multiway join queries, especially more general computation, namely, theta-join, using MapReduce. The reason is that the problem involves more than just a relational operator (key,value) pair transformation and the tuning. There are other critical issues to be addressed: (1) How many MapReduce jobs should we employ to evaluate the query? (2) What is each MapReduce job responsible for? (3) How should multiple MapReduce jobs be scheduled?

It is not trivial to efficiently process complex join queries using MapReduce. There are two challenging issues needed to be resolved. First, the number of available computing units is in fact limited, which is often neglected when mapping a task to a set of MapReduce jobs. Although the pay-as-you-go policy of cloud platform could promise as many computing resources as required, once a computing environment is established, the maximum number of concurrent Map and Reduce tasks is fixed according the system configuration. Therefore, with the user-specified task number, a multiway theta-join query is processed with only a limited number of computing units.

The second challenge is the decomposition of the multiway join into a number of MapReduce tasks is nontrivial. The work of Wu et al. [4] targets at the multiway equi- processing. It decomposes queries into several MapReduce jobs and schedules the execution based on a specific cost model. However, it only considers the pairwise join as the basic scheduling unit. In other words, it follows the traditional multiway join processing methodology, which evaluates the query with a sequence of pairwise joins. This methodology excludes the possible opportunity to evaluate a multiway join in one MapReduce job. Our observation is that, under certain conditions, evaluating a multiway join with one MapReduce job is much more efficient than with a sequence of MapReduce jobs conducting pairwise joins. The work of Lee et al. [5] reports the same observation. One dominating reason is that the I/O costs of intermediate results generated by multiple MapReduce jobs may become unacceptable overheads. The work of Afrati and Ullman [6] presents the solution for evaluating a multiway join in one MapReduce job, which only works for the equi-join case. Since the theta-join cannot be answered by simply making the join attribute the partition key, the solution proposed in Reference 6 cannot be extended to solve the case of multiway theta-joins. The work of Okan et al. [7] demonstrates an effective pairwise theta-join processing using MapReduce. However, its solution is designed for partitioning a two-dimensional result formed by the cross-product of two relations. In the case of multiway join, the result space is a hypercube, the dimensionality of which is the number of the relations involved in the query. The solution in Reference 7 cannot be intuitively extended to handle the partition in high dimensions.
