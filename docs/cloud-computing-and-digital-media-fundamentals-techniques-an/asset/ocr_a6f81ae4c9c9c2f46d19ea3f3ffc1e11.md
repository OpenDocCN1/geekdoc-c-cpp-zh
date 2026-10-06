# Large-Scale Correlation-Based Semantic Classification ■ 177

# 8.4 MR MCA-BASED CLASSIFICATION

MR is a data-processing programming model and supporting framework introduced by Dean and Ghemawat (2008). Its open source implementation, Hadoop (Apache 2013), is utilized by a large number of companies for distributed data processing. Hadoop offers a distributed file system called Hadoop distributed file system (HDFS) on which applications store large data as well as an MR framework on which distributed applications are built. Furthermore, the MR framework abstracts the programmer from the details of parallelization, fault tolerance, data distribution, and load balancing, which greatly reduces the complexity of developing distributed applications.

As shown in Figure 8.1

```
map ap(K₁, N₁)   list(K₂, N₂)

reduce(K₂, list(V₂))   list(K₃, N₃)
```

The processing of an input dataset begins with the map phase, in which the MR framework partitions the data into chunks called splits and invokes a map task to process each split. The size of a split is by default that of an HDFS block, although users can define their own criteria for splitting. The MR framework abstracts a split as a list of records, where a record is

![](bbox=[0.137, 0.693, 0.862, 0.908])