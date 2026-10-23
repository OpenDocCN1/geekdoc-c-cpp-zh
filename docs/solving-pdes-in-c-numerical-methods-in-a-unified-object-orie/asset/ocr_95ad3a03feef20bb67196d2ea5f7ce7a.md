![](bbox=[0.11, 0.17, 0.89, 0.66])

# Figure 18.7. A three-dimensional hypercube (cube) with eight processors in its nodes, numbered by the binary integers 000 to 111. Each node is connected only to the three nodes that differ from it by one binary digit only.

j by the same wire by which processor j is connected to processor i), the total number of connections is

```
K (log₂ K)/2.
```

This number is rather small, yet it supports data transfer from any processor to any other processor in at most log₂ K steps. Indeed, the binary indices of any two processors may differ in at most n = log₂ K digits, so messages can be exchanged between them indirectly through the processors with indices that are obtained by changing one digit at a time in the binary index of the sending processor until the binary index of the receiving processor is formed. For example, the zeroth processor in the above example can send a message to the seventh processor through the path

```
0000 → 0001 → 0011 → 0111.
```

Actually, it follows from Chapter 1, Section 18, that there are six different paths that lead from one processor to the other.

The implementation of a particular program can be optimized in such a way that the processors that need to communicate a lot with each other are those that are connected to each other by a short path in the hypercube. The different kinds of architectures are summarized in Figure 18.8. In what follows, we show the advantage of parallel computers in general and the hypercube architecture in particular in numerical algorithms.