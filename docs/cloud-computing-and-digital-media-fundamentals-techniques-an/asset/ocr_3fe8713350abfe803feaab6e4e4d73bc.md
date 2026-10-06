226 ■ Cloud Computing and Digital Media

# 9.4.5.2 Join Strategies and Optimization

With the algorithm presented above, we can get the MRJs and their execution sequence. Note that we have an assumption that cloud computing system can provide as much computing resources as required. In fact, the similar claim was made by Amazon EC2 service [45]. Based on this assumption, we can make MRJs without having ancestor-descendant relationship in P executed in parallel. Moreover, we adopt hybrid join strategy and bloom filter to improve query efficiency, which are discussed in detail as follows:

**Hybrid join strategy.** There are three basic strategies for MapReduce join: Reduce-side join (repartition join), in-memory join (broadcast join), and Map-side join (improved repartition join) [46]. Our hybrid strategy works as follows: Reduce-side join is used as the default join strategy. When a *Predicate* is small enough to be loaded into the memory, we load this in several Map tasks to perform in-memory join. Map-side join is adopted on the condition that ancestor MRJs' outputs are well partitioned on the number of reducers.

**Bloom filter.** We use bloom filter to implement the in-memory join. As described in Section 5, there are a large number of small *Predicate* files. If the query contains a BQP that refers to a small *Predicate* file, we can always read in this file completely into the main memory and generate the bloom filter of Subject or Object variables, which can be done quite efficiently with one Map task. Since the generated bloom filter is much smaller, it can be loaded into the memory later for each MRJ. With the help of bloom filter, large number of irrelevant RDF triples are filtered out at the Map phase, which greatly reduces the network volume and workload on Reduce tasks. Experiments have proven the effectiveness of this optimization strategy.

# 9.4.6 Implementations

In this section, we first present our overall system design. Then we elaborate on the data processing techniques, which facilitate the join processing.

# 9.4.6.1 System Design

We use Hadoop distributed file systems (HDFS) [47] to set up a repository of large-scale RDF dataset. Figure 9.10 presents a system overview of our solution to RDF query processing. The whole system is backed with well-organized RDF data storage on HDFS, which offers block-level management that promises efficient data retrieval. The query engine accepts users' queries and decides