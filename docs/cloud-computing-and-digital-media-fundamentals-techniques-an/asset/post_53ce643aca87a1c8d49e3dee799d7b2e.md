
# Efficient Join Query Processing on the Cloud ■ 195

Moreover, the question about whether we should evaluate a complex query with a single MapReduce job or several MapReduce jobs is not clear. Therefore, there is no straightforward solution for combining the techniques in the existing literatures to evaluate a multiway theta-join query.

Meanwhile, assume a set of MapReduce jobs are generated for the query evaluation. Given a limited number of processing units, it remains a challenge to schedule the execution of MapReduce jobs such that the query can be answered with the minimum time span. These jobs may have dependency relationships and intercompetition for resource consumptions during the concurrent execution. Currently, the MapReduce framework requires the number of Reduce tasks as a user-specified input. Thus, after decomposing a multiway theta-join query into a number of MapReduce jobs, one challenging issue is how to specify each job a proper Reduce task number such that the overall scheduling achieves the minimum execution time.

## 9.2 BACKGROUND

### 9.2.1 MapReduce Essentials

MapReduce is a programming framework introduced by Google to perform parallel computation on very large datasets, for example, crawled documents, or Web request logs. Large amount of data requires that it is distributed over a large number of machines (nodes). Each participating node contributes storage sources and all are connected over the same distributed file system. Additionally, each machine performs the same computations over the same locally stored data, which results in large-scale distributed and parallel processing. The MapReduce framework takes care of all the underlying details regarding parallelization, data distribution, and network partition tolerant while the user can concern only the local computations executed on every machine. These computations are divided into two phases: the Map phase and the Reduce phase. The nodes assigned the Map phase take their local data as input and processes producing intermediate results that are stored locally. The nodes performing Reduce computation receive the Map intermediate outputs, and combine and process to produce the final result, which in turn is stored in the distributed file system.

As shown in Figure 9.1, the workflow of naive MapReduce is as follows: Generally, a Master node invokes Map tasks on computing nodes that possess input data, which guarantees the locality of computation. Map tasks

![](img/f13da3dd59d15874e4b22b03a274001b_218_0.png)

FIGURE 9.1 Workflow of Map task (a) and Reduce task (b).

transform the input (key,value) pair $(k^1,v^1)$ to, for example, $n$ new pairs: $(k_2^2, v_2^2), (k_n^2, v_n^2)$. The output of Map tasks is then by default hash partitioned to Reduce tasks according to $k_i^2$. Reduce tasks receive $(key,value)$ pairs grouped by $k_i^2$, then perform user-specified computation on all the values of each $key$, and write results back to the storage. For ease of presentation, we use MRJ to denote a MapReduce job in the rest of this chapter.

### 9.2.2 A Cost of Join Processing Using MapReduce

Considering the processing cost of join operations with MRJs, we elaborate a generalized analytic study of an MRJ's execution time given in Reference 8. Generally, most of the CPU time for join processing is spent on simple comparison and counting; thus, system I/O cost dominates the execution time. For MapReduce jobs, heavy cost on large-scale sequential disk scan and frequent I/O of intermediate results dominate the execution time. Therefore, we shall build a model for an MRJ's execution time based on the analysis of I/O and network cost.

General MapReduce computing framework involves three phases of data processing: Map, Reduce, and the data copying from Map tasks to

| M | M | M | M |
|---|---|---|---||
| M | M | | M |
| : | : | : | : |
| M | | M | |

| R | |
|---|n| R |
| | |
| R |

Case 1: CP | CP | CP | CP

Case 2: CP | CP | CP ... | CP

FIGURE 9.2 MapReduce workflow.

Reduce tasks, as shown in Figure 9.2. In the figure, each M stands for a Map task; each CP stands for one phase of Map output copying over network, and R stands for a Reduce task. Since each Map task is based on a data block, we assume that the unit processing cost for each Map task is $t_M$. Moreover, since the entire input data may not be loaded into the system memory within one round [9,10], we assume that these Map tasks are performed by round (we have the same observation in practice). However, the size of Reduce is subjected to the (key,value) distribution. As shown in Figure 9.2, the makespan of an MRJ is dominated by the most time-consuming Reduce task. Therefore, we only consider the Reduce task with the largest volume of inputs in the following analysis: Assume the input size of an MRJ is $S_I$. The total intermediate data copied from Map to Reduce are of size $S_{CP}$, and the number of Map tasks and Reduce tasks are $m$ and $n$, respectively. In addition, as a general assumption, $S_I$ is considered to be evenly partitioned among Map tasks [11]. Let $J_{JM}, J_{JR},$ and $J_{CD}$ denote the total time cost of three phases, respectively, and $T$ be the total execution time of an MRJ. Then.

# Efficient Join Query Processing on the Cloud ■ 197

| M | M | M | M |
|---|---|---|---|
| M | M | | M |
| : | : | : | : |
| M | | M | |

| R | | |
|---|n| R |
| | |
| R | |

Case 1: CP | CP | CP | CP

Case 2: CP | CP | CP ... | CP

FIGURE 9.2 MapReduce workflow.

Reduce tasks, as shown in Figure 9.2. In the figure, each M stands for a Map task; each CP stands for one phase of Map output copying over network, and R stands for a Reduce task. Since each Map task is based on a data block, we assume that the unit processing cost for each Map task is $t_M$. Moreover, since the entire input data may not be loaded into the system memory within one round [9,10], we assume that these Map tasks are performed by round (we have the same observation in practice). However, the size of Reduce is subjected to the (key,value) distribution. As shown in Figure 9.2, the makespan of an MRJ is dominated by the most time-consuming Reduce task. Therefore, we only consider the Reduce task with the largest volume of inputs in the following analysis: Assume the input size of an MRJ is $S_I$. The total intermediate data copied from Map to Reduce are of size $S_{CP}$, and the number of Map tasks and Reduce tasks are $m$ and $n$, respectively. In addition, as a general assumption, $S_I$ is considered to be evenly partitioned among Map tasks [11]. Let $J_{JM}, J_{JR},$ and $J_{CD}$ denote the total time cost of three phases, respectively, and $T$ be the total execution time of an MRJ. Then.

# Efficient Join Query Processing on the Cloud ■ 197

| M | M | M | M |
|---|---|---|---|
| M | M | | M |
| : | : | : | : |
| M | | M | |

| R | | |
|---|n| R |
| | | |
| R | | |

Case 1: CP | CP | CP | CP

Case 2: CP | CP | CP ... | CP

FIGURE 9.2 MapReduce workflow.

Reduce tasks, as shown in Figure 9.2. In the figure, each M stands for a Map task; each CP stands for one phase of Map output copying over network, and R stands for a Reduce task. Since each Map task is based on a data block, we assume that the unit processing cost for each Map task is $t_M$. Moreover, since the entire input data may not be loaded into the system memory within one round [9,10], we assume that these Map tasks are performed by round (we have the same observation in practice). However, the size of Reduce is subjected to the (key,value) distribution. As shown in Figure 9.2, the makespan of an MRJ is dominated by the most time-consuming Reduce task. Therefore, we only consider the Reduce task with the largest volume of inputs in the following analysis: Assume the input size of an MRJ is $S_I$. The total intermediate data copied from Map to Reduce are of size $S_{CP}$, and the number of Map tasks and Reduce tasks are $m$ and $n$, respectively. In addition, as a general assumption, $S_I$ is considered to be evenly partitioned among Map tasks [11]. Let $J_{JM}, J_{JR},$ and $J_{CD}$ denote the total time cost of three phases, respectively, and $T$ be the total execution time of an MRJ. Then.

# Efficient Join Query Processing on the Cloud ■ 197

| M | M | M | M |
|---|---|---|---|
| M | M | | M |
| : | : | : | : |
| M | | M | |

| R | | |
|---|n| R |
| | | |
| R | | |

Case 1: CP | CP | CP | CP

Case 2: CP | CP | CP ... | CP

FIGURE 9.2 MapReduce workflow.

Reduce tasks, as shown in Figure 9.2. In the figure, each M stands for a Map task; each CP stands for one phase of Map output copying over network, and R stands for a Reduce task. Since each Map task is based on a data block, we assume that the unit processing cost for each Map task is $t_M$. Moreover, since the entire input data may not be loaded into the system memory within one round [9,10], we assume that these Map tasks are performed by round (we have the same observation in practice). However, the size of Reduce is subjected to the (key,value) distribution. As shown in Figure 9.2, the makespan of an MRJ is dominated by the most time-consuming Reduce task. Therefore, we only consider the Reduce task with the largest volume of inputs in the following analysis: Assume the input size of an MRJ is $S_I$. The total intermediate data copied from Map to Reduce are of size $S_{CP}$, and the number of Map tasks and Reduce tasks are $m$ and $n$, respectively. In addition, as a general assumption, $S_I$ is considered to be evenly partitioned among Map tasks [11]. Let $J_{JM}, J_{JR},$ and $J_{CD}$ denote the total time cost of three phases, respectively, and $T$ be the total execution time of an MRJ. Then.

# Efficient Join Query Processing on the Cloud ■ 197

| M | M | M | M |
|---|---|---|---|
| M | M | | M |
| : | : | : | : |
| M | | M | |

| R | | |
|---|n| R |
| | | |
| R | | |

Case 1: CP | CP | CP | CP

Case 2: CP | CP | CP ... | CP

FIGURE 9.2 MapReduce workflow.

Reduce tasks, as shown in Figure 9.2. In the figure, each M stands for a Map task; each CP stands for one phase of Map output copying over network, and R stands for a Reduce task. Since each Map task is based on a data block, we assume that the unit processing cost for each Map task is $t_M$. Moreover, since the entire input data may not be loaded into the system memory within one round [9,10], we assume that these Map tasks are performed by round (we have the same observation in practice). However, the size of Reduce is subjected to the (key,value) distribution. As shown in Figure 9.2, the makespan of an MRJ is dominated by the most time-consuming Reduce task. Therefore, we only consider the Reduce task with the largest volume of inputs in the following-in the following analysis: Assume the input size of an MRJ is $S_I$. The total intermediate data copied from Map to Reduce are of size $S_{CP}$, and the number of Map tasks and Reduce tasks are $m$ and $n$, respectively. In addition, as a general assumption, $S_I$ is considered to be evenly partitioned among Map tasks [11]. Let $J_{JM}, J_{JR},$ and $J_{CD}$ denote the total time cost of three phases, respectively, and $T$ be the total execution time of an MRJ. Then.

# Efficient Join Query Processing on the Cloud ■ 197

| M | M | M | M |
|---|---|---|---|
| M | M | | M |
| : | : | : | : |
| M | | M | |

| R | | |
|---|n| R |
| | | |
| R | | |

Case 1: CP | CP | CP | CP

Case 2: CP | CP | CP ... | CP

FIGURE 9.2 MapReduce workflow.

Reduce tasks, as shown in Figure 9.2. In the figure, each M stands for a Map task; each CP stands for one phase of Map output copying over network, and R stands for a Reduce task. Since each Map task is based on a data block, we assume that the unit processing cost for each Map task is $t_M$. Moreover, since the entire input data may not be loaded into the system memory within one round [9,10], we assume that these Map tasks are performed by round (we have the same observation in practice). However, the size of Reduce is subjected to the (key,value) distribution. As shown in Figure 9.2, the makespan of an MRJ is dominated by the most time-consuming Reduce task. Therefore, we only consider the Reduce task with the largest volume of inputs in the following analysis: Assume the input size of an MRJ is $S_I$. The total intermediate data copied from Map to Reduce are of size $S_{CP}$, and the number of Map tasks and Reduce tasks are $m$ and $n$, respectively. In addition, as a general assumption, $S_I$ is considered to be evenly partitioned among Map tasks [11]. Let $J_{JM}, J_{JR},$ and $J_{CD}$ denote the total time cost of three phases, respectively, and $T$ be the total execution time of an MRJ. Then.

# Efficient Join Query Processing on the Cloud ■ 197

| M | M | M | M |
|---|---|---|---|
| M | M | | M |
| : | : | : | : |
| M | | M | |

| R | | |
|---|n| R |
| | | |
| R | | |

Case 1: CP | CP | CP | CP

Case 2: CP | CP | CP ... | CP

FIGURE 9.2 MapReduce workflow.

Reduce tasks, as shown in Figure 9.2. In the figure, each M stands for a Map task; each CP stands for one phase of Map output copying over network, and R stands for a Reduce task. Since each Map task is based on a data block, we assume that the unit processing cost for each Map task is $t_M$. Moreover, since the entire input data may not be loaded into the system memory within one round [9,10], we assume that these Map tasks are performed by round (we have the same observation in practice). However, the size of Reduce is subjected to the (key,value) distribution. As shown in Figure 9.2, the makespan of an MRJ is dominated by the most time-consuming Reduce task. Therefore, we only consider the Reduce task with the largest volume of inputs in the following analysis: Assume the input size of an MRJ is $S_I$. The total intermediate data copied from Map to Reduce are of size $S_{CP}$, and the number of Map tasks and Reduce tasks are $m$ and $n$, respectively. In addition, as a general assumption, $S_I$ is considered to be evenly partitioned among Map tasks [11]. Let $J_{JM}, J_{JR},$ and $J_{CD}$ denote the total time cost of three phases, respectively, and $T$ be the total execution time of an MRJ. Then.

# Efficient Join Query Processing on the Cloud ■ 195

Moreover, the question about whether we should evaluate a complex query with a single MapReduce job or several MapReduce jobs is not clear. Therefore, there is no straightforward solution for combining the techniques in the existing literatures to evaluate a multiway theta-join query.

Meanwhile, assume a set of MapReduce jobs are generated for the query evaluation. Given a limited number of processing units, it remains a challenge to schedule the execution of MapReduce jobs such that the query can be answered with the minimum time span. These jobs may have dependency relationships and intercompetition for resource consumptions during the concurrent execution. Currently, the MapReduce framework requires the number of Reduce tasks as a user-specified input. Thus, after decomposing a multiway theta-join query into a number of MapReduce jobs, one challenging issue is how to specify each job a proper Reduce task number such that the overall scheduling achieves the minimum execution time.

## 9.2 BACKGROUND

### 9.2.1 MapReduce Essentials

MapReduce is a programming framework introduced by Google to perform parallel computation on very large datasets, for example, crawled documents, or Web request logs. Large amount of data requires that it is distributed over a large number of machines (nodes). Each participating node contributes storage sources and all are connected over the same distributed file system. Additionally, each machine performs the same computations over the same locally stored data, which results in large-scale distributed and parallel processing. The MapReduce framework takes care of all the underlying details regarding parallelization, data distribution, and network partition tolerant while the user can concern only the local computations executed on every machine. These computations are divided into two phases: the Map phase and the Reduce phase. The nodes assigned the Map phase take their local data as input and processes producing intermediate results that are stored locally. The nodes performing Reduce computation receive the Map intermediate outputs, and combine and process to produce the final result, which in turn is stored in the distributed file system.

As shown in Figure 9.1, the workflow of naive MapReduce is as follows: Generally, a Master node invokes Map tasks on computing nodes that possess input data, which guarantees the locality of computation. Map tasks transform the input (key,value) pair $(k^1,v^1)$ to, for example, $n$ new pairs: $(k_2^2, v_2^2), (k_n^2, v_n^2)$. The output of Map tasks is then by default hash partitioned to Reduce tasks according to $k_i^2$. Reduce tasks receive $(key,value)$ pairs grouped by $k_i^2$, then perform user-specified computation on all the values of each $key$, and write results back to the storage. For ease of presentation, we use MRJ to denote a MapReduce job in the rest of this chapter.

### 9.2.2 A Cost of Join Processing Using MapReduce

Considering the processing cost of join operations with MRJs, we elaborate a generalized analytic study of an MRJ's execution time given in Reference 8. Generally, most of the CPU time for join processing is spent on simple comparison and counting; thus, system I/O cost dominates the execution time. For MapReduce jobs, heavy cost on large-scale sequential disk scan and frequent I/O of intermediate results dominate the execution time. Therefore, we shall build a model for an MRJ's execution time based on the analysis of I/O and network cost.

General MapReduce computing framework involves three phases of data processing: Map, Reduce, and the data copying from Map tasks to Reduce tasks, as shown in Figure 9.2.

| M | M | M | M |
|---|---|---|---|
| M | M | | M |
| : | : | : | : |
| M | | M | |

| R | | |
|---|n| R |
| | | |
| R | | |

Case 1: CP | CP | CP | CP

Case 2: CP | CP | CP ... | CP

FIGURE 9.2 MapReduce workflow.

In the figure, each M stands for a Map task; each CP stands for one phase of Map output copying over network, and R stands for a Reduce task. Since each Map task is based on a data block, we assume that the unit processing cost for each Map task is $t_M$. Moreover, since the entire input data may not be loaded into the system memory within one round [9,10], we assume that these Map tasks are performed by round (we have the same observation in practice). However, the size of Reduce is subjected to the (key,value) distribution. As shown in Figure 9.2, the makespan of an MRJ is dominated by the most time-consuming Reduce task. Therefore, we only consider the Reduce task with the largest volume of inputs in the following analysis: Assume the input size of an MRJ is $S_I$. The total intermediate data copied from Map to Reduce are of size $S_{CP}$, and the number of Map tasks and Reduce tasks are $m$ and $n$, respectively. In addition, as a general assumption, $S_I$ is considered to be evenly partitioned among Map tasks [11]. Let $J_{JM}, J_{JR},$ and $J_{CD}$ denote the total time cost of three phases, respectively, and $T$ be the total execution time of an MRJ. Then.
