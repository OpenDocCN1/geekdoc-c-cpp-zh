+   - 12.7.3 Lock-Free Parallelization ........................................ 234
+   - 12.7.4 Software APIs ............................................................... 235
+   - 12.8 Summary .............................................................................. 236
+   - References .................................................................................... 237

# ABSTRACT

This chapter brings together three topics: hash functions, Bloom filters, and the recently emerged streaming algorithms. Hashing is the oldest of the three and is backed by much literature. Bloom filters are based on hash functions and benefit from hashing efficiency directly. Streaming algorithms use both Bloom filters and hashing in various ways but impose strict requirements on performance. This chapter views the three topics from the viewpoint of efficiency and speed. The two main performance metrics are per-unit processing time and the size of the memory footprint. All algorithms are presented as C/C++ pseudocode. Specific attention is paid to the feasibility of hardware implementation.

# 12.1  INTRODUCTION

Hadoop file system (HDFS) [1] and MapReduce are de facto standards in Big Data processing today. Although they are two separate technologies, they form a single package as far as Big Data processing—not just storage—is concerned. This chapter will treat them as one package. Today, Hadoop and/or MapReduce lack popular alternatives [2]. HDFS solves the practical problem of not being able to store Big Data on a single machine by distributing the storage over multiple nodes [3]. MapReduce is a framework on which one can run jobs that process the contents of the storage—also in a distributed manner—and generate statistical summaries. This chapter will show that performance improvements mostly target MapReduce [4].

There are several fundamental problems with MapReduce. First, the map and reduce operators are restricted to key–value hashes (data type, not hash function), which places a cap on usability. For example, while data streaming is a good alternative for Big Data processing, MapReduce fails to accommodate the necessary data types [5]. Secondly, MapReduce jobs create heterogeneous environments where jobs compete for the same resource with no guarantee of fairness [4]. Finally, MapReduce jobs, or HDFS for that matter, lack time awareness, while some algorithms might need to process data in their time sequence or using a time window.

The core premise of this chapter is to replace HDFS/MapReduce with a time-aware storage and processing logic. Big data is replayed along the timeline, and all the jobs get the time-ordered sequence of data items. The major difference here is that the new method collects all the jobs in one place—the node that replays data—while HDFS/MapReduce sends jobs to remote nodes so that data can be processed locally. This architecture is chosen for the sole purpose of accommodating a wide range of data streaming algorithms and the data types they create [5].

The new method presented in this chapter can be viewed as a generic technology that exists independently of HDFS and MapReduce. This technology is one of many possible practical applications of the new method.