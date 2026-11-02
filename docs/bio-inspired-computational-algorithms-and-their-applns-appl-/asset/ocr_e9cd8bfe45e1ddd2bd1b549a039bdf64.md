In the third part, repeat the above two operations dynamically. The process is shown as step6.

Step 6. With the data stream flowing, this algorithm continues to deal with the new incoming data and discard the old data, transfer to step 2 and continue the above operations until the data stream coming to the end.

# 3.2 NSWGA algorithm analysis

Comparing with other algorithms which use pattern tree to maintain the historical information of data stream, NSWGA processes a quantity of data parallely at one time, while the pattern tree algorithms process a single transaction item at one time, each transaction item needs match repeatedly. Mining the frequent itemsets of the data in the current window, the time of whole process is not only dependent on the times of scanning the data in the window, but also dependent on the internal basic operation - the number of matching.

Suppose a data stream has N transaction items, each transaction item has V attributes; each attribute has K possible values. The pattern tree algorithms may have K^V frequent pattern search paths. Let the window size is N. When the entire data stream in the window flow over, the necessary calculated amount to get frequent itemsets is N * K * V.

For fp-tree algorithm, when the fp-tree has L paths, the calculated amount is 2 * N * V + V * L, the number L will increase with the threshold of support degree reducing.

When the support degree is S, iteration times of genetic algorithms is T, the number of parallel computing is Z (Z according to the amount of data, in this case set Z 200),the sliding window size is N, the necessary calculated amount to get frequent itemsets is P = P1 + P2 + P3. Thereinto:

P1 ≈ N * V the calculated amount to get 1 - frequent itemsets;

P2 = V * T * N / S * Z the calculated amount to get the frequent itemsets in the nested sub-window;

P3≈ α *V^N/S*Z*M (1<= α <=1/S) the calculated amount to get the final frequent itemsets.

When the property value K is large, this algorithm has obvious advantage in time complexity. When the number of Z is larger, the runtime will become shorter.

# 4. Experiment and analysis

# 4.1 Experiment

In this experiment, we use artificial data sets and the MATLAB and CUDA C language to implement NSWGA algorithm. We use the computer with 2.6IGHZ CPU, 2GMB memory, Nvidia GPU C1060, windows XP operating system to test the performance of the algorithm.

The size of the sliding window is 100k. The size of the data set is 200K.With the data flowing, we make statistic every 10k of the data.

+   1. The analog data stream has three attributes. Each attribute has 10 possible values. The running results of the algorithms are shown in Table 1.