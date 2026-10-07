# Figure 4.12 Dijkstra's algorithm will not work if there are negative edges.

![](bbox=[0.536, 0.122, 0.693, 0.237])

along edge:

```
procedure update(u, v) \in E
dist(v) = min(dist(v), dist(u) + l(u, v))
```

This update operation is simply an expression of the fact that the distance to v cannot possibly be more than the distance to u, plus l(u, v). It has the following properties.

+   - It gives the correct distance to v in the particular case where u is the secondlast node in the shortest path to v, and dist(u) is correctly set.
- It will never make dist(v) too small, and in this sense it is safe. For instance, a slew of extraneous update's can't hurt.

This operation is extremely useful: it is harmless, and if used carefully, will correctly set distances. In fact, Dijkstra's algorithm can be thought of simply as a consequence of update's. We know this particular sequence doesn't work with negative edges, but is there some other sequence that does? To get a sense of the properties this sequence must possess, pick's node t and the shortest path to t from

![](bbox=[0.397, 0.663, 0.803, 0.715])

This path can have at most |V|—1 edges (do you see?). If the sequence of updates includes (s, u₁), (u₁, u₂), (u₂, u₃), ..., (uₖ, t), in that order (though not necessarily consecutively), then the first property the distance to t will be correctly computed. It doesn't matter what other updates occur on these edges, or what happens in the rest of the graph, because updates are safe.

But still, if we don't know all the shortest paths beforehand, how can we be to update the right edges in the right order? Here is an easy solution: update all the edges, |V|—1 times! The resulting O(|V|-|E|) procedure is called the BellmanFord algorithm and is shown in Figure 4.13, with an example run in Figure 4.14.