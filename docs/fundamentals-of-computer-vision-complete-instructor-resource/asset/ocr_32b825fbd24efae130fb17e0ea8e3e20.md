![](bbox=[0.195, 0.115, 0.435, 0.255])

Figure 4.3 An image containing two connected components.

A cutting algorithm begins with edges between all adjacent pixels, and then cutting edges to separate the image graph into distinct components. Examples of both methods will be described in Chapter 8.

# 4.2.6 The Adjacency Paradox and Hexagonal Pixels

As a sidenote to the subject of image representation, we discuss the issue of “adjacency” as well as the famous “adjacency paradox” in somewhat more depth. We also briefly describe an alternative sampling approach that requires hexagonally shaped pixels rather than the traditional square-shaped pixel. We discuss how this alternative sampling would completely resolve the adjacency paradox.

Two pixels are either adjacent to each other or not, right? In the sense of graphical representations for images, it would appear so. But pixels are (usually) rectangular, so they may be adjacent to pixels above, below, left, or right. In a graph representation, an edge of the graph runs between two nodes to indicate that they are adjacent. But how about diagonals? Let’s look at that a bit more carefully.

We may define neighborhoods in a variety of ways, but the most common and most intuitive way is to say that two pixels are neighbors if they share a side (4-connected) or they share either a side or a vertex (8-connected). The neighborhood (or aura) of a pixel is the set of pixels that are neighbors (surprise!). The 4-neighbors of the center point are illustrated in Figure 4.5(b). The neighbors of a pixel are usually adjacent to that pixel, but there is no fundamental requirement that they be. We will see this again when we talk about “cliques.”

```
1111222111111111111111111111
1112222111113333333333333111
1112222111113333333333333111
1112222111111111133333311111
1112221111111111113333331111
1122222211111111113333333111
1122442221111111133333331111
1122222211111111111333311111
1112222111111111111111111111
```

Figure 4.4 The label image corresponding to Figure 4.3.