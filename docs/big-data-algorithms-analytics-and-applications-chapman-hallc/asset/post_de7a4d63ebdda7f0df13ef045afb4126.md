
- 84. N. Roussopoulos, S. Kelley, and F. Vincent. "Nearest neighbor queries." In Proc. ACM SIGMOD Int'l. Conf. on Management of Data, San Jose, CA, June 1995, pp. 71–79.
- 85. L. Zhang, "High-dimensional indexing methods utilizing clustering and dimensionality reduction," PhD Dissertation, Computer Science Department, New Jersey Institute of Technology (NJIT), Newark, NJ, May 2005.
- 86. K. Chakrabarti, and S. Mehrotra. "The hybrid tree: An index structure for high dimensional feature spaces." In Proc. IEEE Int'l. Conf. on Data Engineering (ICDE), 1999, pp. 440–447.
- 87. S. Berchtold, D. A. Keim, and H. P. Kriegel. "The X-tree: An index structure for high-dimensional data." In Proc. 22nd Int'l. Conf. on Very Large Data Bases (VLDB), San Jose, CA, August 1996, pp. 28–39.
- 88. S. Berchtold, C. Böhm, and H.-P Kriegel. "The pyramid-technique: Towards breaking the curse of dimensionality." In Proc. ACM SIGMOD Int'l. Conf. on Management of Data, Seattle, WA, June 1998, pp. 142–153.
- 89. B. C. Ooi, K.-L. Tan, C. Yu, and S. Bressan. "Indexing the edges—A simple and yet efficient approach to high-dimensional indexing." In Proc. 19th ACM Int'l. Symp. on Principles of Database Systems (PODS), Dallas, May 2000, pp. 166–174.
- 90. C. Yu, B. C. Ooi, K.-L. Tan, and H. Jagadish. "Indexing the distance: An efficient method for knn processing." In Proc. 27th Int'l. Conf. on Very Large Data Bases (VLDB), Rome, Italy, September 2001, pp. 421–430.
- 91. H. V. Jagadish, B. C. Ooi, K. L. Tan, C. Yu, and R. Zhang. "iDistance: An adaptive B+-tree based indexing method for nearest neighbor search." ACM Transactions on Database Systems (TODS) 30(2): 364–397 (2000).
- 92. J. K. Uhlmann. "Satisfying general proximity/similarity queries with metric trees." Information Processing Letters (IPL) 40(4): 175–179 (1991).
- 93. P. N. Yianilos. "Data structures and algorithms for nearest neighbor search in general metric spaces." In Proc. 4th Annual ACM-SIAM Symposium on Discrete Algorithms (SODA), Austin, TX, January 1993, pp. 311–321.
- 94. T. Bozkaya, and M. Ozsoyoglu. "Distance-based indexing for high-dimensional metric spaces." In Proc. ACM SIGMOD Int'l. Conf. on Management of Data, Tucson, AZ, May 1997, pp. 357–368.
- 95. P. Ciaccia, M. Patella, and P. Zezula. "M-tree: An efficient access method for similarity search in metric spaces." In Proc. 23rd Int'l. Conf. on Very Large Data Bases (VLDB), Athens, Greece, August 1997, pp. 426–435.
- 96. R. F. S. Filho, A. Traina, C. Traina Jr., and C. Faloutsos. "Similarity search without tears: The OMNI family of all-purpose access methods." In Proc. 17th IEEE Int'l. Conf. on Data Engineering (ICDE), Heidelberg, Germany, April 2001, pp. 623–630.
- 97. B. Cui, B. C. Ooi, J. Su, and K.-L. Tan. "Indexing high-dimensional data for efficient in-memory similarity search." IEEE Transactions on Knowledge and Data Engineering (TKDE) 17(3): 339–353 (2005).
- 98. J. L. Hennessey, and D. A. Patterson. Computer Architecture: A Quantitative Approach, 5th edition. Elsevier, Burlington, MA, 2011.
- 99. K. I. Lin, H. V. Jagadish, and C. Faloutsos. "The TV-tree: An index structure for high-dimensional data." VLDB Journal 3(4): 517–542 (1994).
- 100. A. Thomasian, and L. Zhang. "The Stepwise Dimensionality-Increasing (SDI) index for high dimensional data." The Computer Journal 49(5): 609–618 (2006).
- 101. D. A. White, and R. Jain. "Similarity indexing, Algorithms and performance." In Storage and Retrieval for Image and Video Databases (SPIE), Volume 2670, San Jose, CA, 1996, pp. 62–73.
- 102. K. V. Ravikanth, D. Agrawal, and A. Singh. "Dimensionality reduction for similarity searching in dynamic databases." In Proc. ACM SIGMOD Int'l. Conf. on Management of Data, Seattle, WA, June 1998, pp. 166–176.
- 103. S. Rajamanickam. "Efficient algorithms for sparse singular value decomposition." PhD Thesis, Computer Science Dept., University of Florida, Gainesville, FL, 2009. Available at http://www.cise.ufl.edu/~srajaman/Rajamanickam_S.pdf.
- 104. A. A. Amini. "High-dimensional principal component analysis." PhD Thesis, Report Number UCB/EECS-2011-104, EECS Dept., University of California, Berkeley, CA, 2011. Available at http://www.eecs.berkeley.edu/Pubs/TechRpts/2011/EECS-2011-104.html.

## APPENDIX 3.A: COMPUTING APPROXIMATE DISTANCES WITH DIMENSIONALITY-REDUCED DATA

The dimensionality reduction method in References 3 and 14 retains $n < N$ columns of the $Y$ matrix, which correspond to the largest eigenvalues, while the method described in References 8 and 18 retains the $n$ columns of the $U$ matrix corresponding to the largest eigenvalues. In both cases, the eigenvalues or singular values are in nonincreasing order, so that columns with the smallest indices need to be preserved. We first show that retaining the $n$ columns of the $Y$ matrix results in the same distance error as retaining the same dimensions of the $U$ matrix. We also show that our method is computationally more efficient than the other method. Retaining the first $n$ dimensions (columns) of the transformed matrix $Y = XV$, we have

$$y_{i,j} = \sum_{k=1}^{N} x_{i,k} v_{k,j}, \; 1 \le j \le n, 1 \le i \le M.$$

The rest of the columns of the matrix are set to the column mean, which is zero in our case. (Some data sets are studentized by dividing the zero-mean column by the standard deviation [3].) The squared error in representing point $P_i$, $1 \le i \le M$ is then

$$e_i = \sum_{j=n+1}^{N} y_{i,j}^2 = \sum_{j=n+1}^{N} \left( \sum_{k=1}^{N} x_{i,k} v_{k,j} \right)^2, \; 1 \le i \le M.$$

The elements of $X$ are approximated as $X' \approx USV^T$ by utilizing the first $n$ dimensions of $U$ [8,18]:

$$x_{i,j} = \sum_{k=1}^{n} s_k u_{i,k} v_{k,j}, \; 1 \le j \le N, 1 \le i \le M.$$

Noting that $Y = XV = US$, the squared error in representing $P_i$ is

$$e_i = \sum_{j=1}^{N} \left( \sum_{k=n+1}^{N} s_k u_{i,k} v_{k,j} \right)^2 = \sum_{j=1}^{N} \left( \sum_{k=n+1}^{N} y_{i,k} v_{k,j} \right)^2.$$

To show that $e_i = e_i'$, $1 \le i \le M$, we use the definition $\delta_{k,k'} = 1$ for $k = k'$ and $\delta_{k,k'} = 0$ for $k \ne k'$.

$$e_i' = \sum_{j=1}^{N} \left( \sum_{k=n+1}^{N} y_{i,k} v_{k,j} \right) \left( \sum_{k'=n+1}^{N} y_{i,k'} v_{k',j} \right) = \sum_{k=n+1}^{N} \sum_{k'=n+1}^{N} y_{i,k} y_{i,k'} \sum_{j=1}^{N} v_{k,j} v_{k',j}$$

$$= \sum_{k=n+1}^{N} \sum_{k'=n+1}^{N} y_{i,k} y_{i,k'} \delta_{k,k'} = \sum_{j=n+1}^{N} y_{i,j}^2 = e_i.$$

Our method is more efficient from the viewpoint of computational cost for nearest neighbor, range, and window queries. In the case of nearest neighbor queries, once the input or query vector is transformed and the appropriate $n$ dimensions are selected, we need only be concerned with these dimensions. This is less costly than applying the inverse transformation.

## Multiple Sequence Alignment and Clustering with Dot Matrices, Entropy, and Genetic Algorithms

John Tsiligiridis

### CONTENTS

- 4.1 Introduction — 72
- 4.2 CDM — 74
- 4.3 PEA — 76
- 4.4 Divide and Conquer — 79
- 4.5 GAs — 79
- 4.6 DCGA — 80
- 4.7 K-Means — 81
- 4.8 Clustering Genetic Algorithm with the SSE Criterion — 81
- 4.9 MapReduce Section — 83
- 4.10 Simulation — 83
- 4.11 Conclusion — 87
- References — 87

### ABSTRACT

The purpose of this project is to present a set of algorithms and their efficiency for Multiple Sequence Alignment (MSA) and clustering problems, including also solutions in distributive environments with Hadoop. The strength, the adaptability, and the effectiveness of the genetic algorithms (GAs) for both problems are pointed out. MSA is among the most important tasks in computational biology. In biological sequence comparison, emphasis is given to the simultaneous alignment of several sequences. GAs are stochastic approaches for efficient and robust search that can play The parallel nature of GAs makes them an optimal base for parallelization. Beyond the Message Passing Interface (MPI), the traditional solution for the GA and hybrid GA implementation, Hadoop can improve the parallel behavior of the GAs, becoming a much better solution. In addition, for MPI programming, a sophisticated knowledge of parallel programming (i.e., synchronization, etc.) is needed. MPI does not scale well on clusters where a failure is not unlikely (i.e., long processing programs). MapReduce [5,6] provides an opportunity to easily develop large-scale distributed applications. Several different implementations of MapReduce have been developed [7,8]. Reference 7 is based on another architecture such as Phoenix, while Reference 8 deals with the issue of reducing the number of iterations for finding the right set of initial centroids.

The contribution of this chapter is the development of a set of algorithms for both MSA and GA and also the discovery of a distributed solution for CDM and for hybrid GA.

The chapter is organized as follows: CDM and PEA are developed in Sections 4.2 and 4.3, respectively. The divide-and-conquer principle is presented in Section 4.4. Sections 4.5 through 4.7 include the GAs, K-means, and GA following the divide-and-conquer method (DCGA), which represent the part of work that is based on GA. Section 4.8 refers to DCGA. Section 4.9 includes the DCGA distributed solution with Hadoop. Finally, Section 4.10 includes a simulation.

### 4.2 CDM

CDM has three phases: (1) the dot matrices' preparation, (2) the scan phase, and (3) the link phase. In the first phase, the dot matrices are examined, in the second, the diagonal similarities, and in the third phase, the vertical continuity. The dot matrix running time is proportional to the product of the size of the sequences. Working with a set of dot matrices poses the problem of how to define consistency. Scanning of graphs for a series of 1s reveals similarity or a string of the same characters. The steps of the algorithm are as follows: (1) Prepare the dot plot matrix [9] and examine the horizontal continuity (preparation phase). (2) Find gaps (horizontal) and examine the diagonal location (preparation phase). (3) Scan phase. (4) Examine the vertical continuity (link phase). Steps 1 and 2 belong to the preparation phase. Create vectors that hold the locations of 1s (as developed in the example). In the link phase, the locations are combined. The advantage of CDM is that with the link phase only (n − 1), comparisons are needed (instead of n), where n is the number of sequences.

```
CDM //input: the strings into 2 dim array in[][]
//output: MSA using pointers method, out[][]
//variable: ma[][], hold 1's in similar positions
//fin[][]: hold the similar locations of all the pairs (there are
//k-1 pairs for k sequences
//hor[][]: for horizontal/vertical gaps '-' in locations
//V arrays for similar items (k-1) arrays for k sequences
//scan phase
for each pair of strings (# pairs<= k-1)
find the similar items, seed (m : location)    extend it
        (m+1,...)
```
