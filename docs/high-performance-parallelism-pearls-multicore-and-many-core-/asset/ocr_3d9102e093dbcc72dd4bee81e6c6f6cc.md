(not shown) the plot follows a 1/N dependence, where N is the matrix size. This is because the compute is O(N³) whereas data transfers are O(N²). In the tiled hStreams case, the communication overhead can be partially covered by reducing the latency before which computation begins, by starting after just small tiles of data are sent, versus having to wait for the full A and B matrices to arrive at the coprocessor. This plot gives an idea of the upper bound of how much one can hope to recover by concurrent invocation of data transfers and computes by using the hStreams framework.

In this section, we looked at binary questions: to tile or not to tile, to pipeline or not to pipeline, to offload or not to offload. We saw above that **tiling generally helps, the pipelining is beneficial in all but anomalous cases, and once matrix sizes are big enough, using more efficient computing domains tends to be better than keeping all computation local.**

# TRADE-OFFS IN DEGREE OF TILING AND NUMBER OF STREAMS

Trade-offs in the degree of tiling and the number of streams are more subtle. There are no robust heuristics that we know of for determining the optimal degree of tile decomposition, or the optimal number of streams per computing domain. We first illustrate that there are trade-offs, then explain some of the underlying effects that have performance impact, and then we will show how we can formulate the matrix multiply algorithm to enable easy exploration of the optimization space.

Figure 15.9 shows the performance of the tiled hStreams matrix multiply program for a variety of choices of number of tiles per side (T) and number of streams (nstreams). Note the large variation in performance. The performance significantly drops when number of tiles on a side is 4 and number of streams is either 8 or 16. Neither four streams nor four tiles on a side are always best. In the case of

![](bbox=[0.279, 0.569, 0.704, 0.824])

**FIGURE 15.9**

Performance of tiled hStreams matmult program for different choices of number of tiles per side (T) and number of streams (nstreams). Performance is highly sensitive to the choice of these parameters. It is difficult to predict a priori what is an optimal choice, but hStreams makes it very easy to explore the optimization space.