# Research on Scene 3D Reconstruction ■ 285

# 11.3.1.2 MapReduce Model

The MapReduce model is a programming model for large-scale distributed data processing. It has the properties follows:

+   1. Simple, elegant concept
2. Restricted, yet powerful programming construct
3. Building block for other parallel programming tools
4. Extensible for different applications

Also, an implementation of a system to execute such programs can take the advantages listed below:

+   1. Parallelism
2. Tolerate failures
3. Hide messy internals from users
4. Provide tuning knobs for different applications

11.3.1.2.1 Basic Programming Model The computation takes a set of input key-value pairs and produces a set of output key-value pairs. The user of the MapReduce model expresses the computation as two functions: Map and Reduce (Figure 11.10).

The Map function, written by the user, takes an input pair and produces a set of intermediate key-value pairs. The MapReduce groups together all intermediate values associated with the same intermediate key $k'$ and passes them to the Reduce function.

The Reduce function, also written by the user, takes an intermediate $k'$, accepts key $k'$ and a set of values for that key. It merges these values to form a possibly smaller set of values. Typically, just zero or one

![](bbox=[0.134, 0.768, 0.862, 0.883])

FIGURE 11.10 MapReduce model.