We'll illustrate how the algorithm works with this small graph:

![](bbox=[0.435, 0.185, 0.765, 0.305])

The algorithm begins by filling in one value in the distance array. We fill in 0 for the component that is indexed by the start vertex itself, indicating that the weight of the shortest path from the start vertex to the start vertex itself is zero. This is correct since the empty path exists from the start vertex to itself. At this point, the distance array has one known value:

| distance | 0 | ? | ? | ? | ? | ? |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

At this point we have one correct value, distance[0]. In the other locations we will write a value based on what we know so far. Because we don't know too much, our initial values won't be too accurate, but that's okay. In fact, the values that we fill in will all be infinity, represented by the symbol ∞. The distance array, with mostly ∞, is shown here:

| distance | 0 | ∞ | ∞ | ∞ | ∞ | ∞ |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

In an actual implementation, we would use some special integer value for ∞. For example, we could use -1 and make sure that all the rest of our programming always treats an occurrence of -1 as if it were infinity.

Now we are ready to do some processing that will steadily improve the values in the distance array. We begin with an observation about the initial values that we've placed in the distance array. These initial values are actually correct, if we are permitting only the empty path and ignoring all other paths. In other words, if the empty path is the only path that we are permitting, then there is a path from the start vertex to itself (namely the empty path with weight 0). But there is no way to get from the start vertex to any other vertex, and the fact that there is no path is represented by ∞ in the distance array.