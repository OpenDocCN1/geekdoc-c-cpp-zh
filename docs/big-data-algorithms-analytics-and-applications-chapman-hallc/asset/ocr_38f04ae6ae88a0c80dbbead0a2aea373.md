streams a partial data stream to a global computing center when local resources become insufficient.

# 11.4.1.5 High Throughput

High-throughput stream computing will improve data stream computing ability by running multiple independent instances of a task topology graph on multiple processors at the same time. In BDSC environments, it is difficult to achieve high throughput, as it is hard to decide how to identify the need for a replication subgraph in a task topology graph, to decide the number of replicas, and to decide the fraction of the data stream to assign to each replica.

To achieve high throughput in BDSC environments, a good multiple-instance replication strategy is needed. Usually, the data stream loading of all instances of all nodes in a task topology graph being equal is a good choice, as the computing ability of all computing nodes are efficient, and it is easy to achieve high-throughput states.

# 11.4.2 On-the-Fly Work

Future investigation will focus on the following aspects:

+   1. Research on new strategies to optimize a task topology graph, such as subgraph partitioning strategy, subgraph replication strategy, and subgraph allocating strategy, and to provide a high-throughput BDSC environment
+   2. Research on dynamic extensible data stream strategies, such that a data stream can be adjusted according to available resources and the QoS of users, and provide a highly load-balancing BDSC environment
+   3. Research on the impact of a task topology graph with a cycle, and a corresponding task topology graph optimize strategy and resource allocating strategy, and provide a highly adaptive BDSC environment
+   4. Research on the architectures for large-scale real-time stream computing environments, such as symmetric architecture and master–slave architecture, and provide a highly consistent BDSC environment
+   5. Develop a BDSC system with the features of high throughput, high fault tolerance, high consistency, and high scalability, and deploy such a system in a real BDSC environment

# ACKNOWLEDGMENTS

This work was supported in part by the National Natural Science Foundation of China under Grant No. 61170008 and Grant No. 61272055, in part by the National Grand Fundamental Research 973 Program of China under Grant No. 2014CB340402 in part by the National High Technology Research and Development Program of China under Grant No. 2013AA01A210, and in part by the China Postdoctoral Science Foundation under Grant No. 2014M560976.