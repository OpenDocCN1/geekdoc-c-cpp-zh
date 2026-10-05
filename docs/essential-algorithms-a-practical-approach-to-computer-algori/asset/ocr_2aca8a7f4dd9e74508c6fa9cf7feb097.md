# Chapter 8 Hash Tables 177

In other words, if K, K + 1, K + 2, K + 3, ... is the probe sequence created by linear probing, the sequence created by quadratic probing is K, K + 1², K + 2², K + 3², ...

Now, if two items map to different positions in the same cluster, they don't follow the same probe sequence and don't necessarily end up adding to the cluster.

Figure 8-4 shows an example. Initially the table has a cluster containing five items. The value 71 has the probe sequence 1, 1 + 1² = 2, 2 + 2² = 5, 1 + 3² = 10, so it doesn't add to the cluster. The value 93 initially maps to the same cluster but has the probe sequence 3, 3 + 1² = 4, 3 + 2² = 7, so it doesn't add to the cluster, either.

![](bbox=[0.181, 0.301, 0.775, 0.467])

Figure 8-4: Quadratic probing reduces primary clustering.

The QuadraticProbing example shown in Figure 8-5 uses quadratic probing. If you compare this figure to Figure 8-3, you'll see that quadratic probing gives a shorter average probe sequence length than linear probing. In this example, quadratic probing gave an average probe sequence length of 1.92, whereas linear probing gave an average length of 2.42.

> NOTE The program shown in Figure 8-5 is part of the solution to Exercise 8.4. See Appendix B for information.

Quadratic probing reduces primary clustering, but it can suffer from secondary clustering. In secondary clustering, values that map to the same initial position in the array follow the same probe sequence, so they create a cluster. This cluster is spread out through the array, but it still results in longer probe sequences for the items that map to the same initial position.

Quadratic probing also has the drawback that it may fail to find an empty entry even if a few positions are left in the table. Because of how a quadratic probe sequence jumps further and further through the array, it may jump over an empty position and not find it.