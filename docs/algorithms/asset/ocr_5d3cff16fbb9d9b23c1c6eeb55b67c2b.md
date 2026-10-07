Chapter 3

Algorithms 83

# Figure 3.2 Exploring a graph is rather like navigating a maze.

![](bbox=[0.273, 0.122, 0.952, 0.269])

# 3.2 Depth-first search in undirected graphs

# 3.2.1 Exploring mazes

Depth-first search is a surprisingly versatile linear-time procedure that reveals a wealth of information about a graph. The most basic question it addresses is,

What parts of the graph are reachable from a given vertex?

To understand this task, try putting yourself in the position of a computer that has just been given a new graph, in the form of an adjacency list. This representation offers just one basic operation: finding the neighbors of a vertex. With only this primitive, the reachability problem is rather like exploring a labyrinth (Figure 3.2). You start walking from a fixed place and whenever you reach any junction (vertex) there are a variety of passages (edges) you can follow. A careless choice of passages might lead you around in circles or cause you to overlook some part of the maze. Clearly, you need to record some intermediate information during exploration.

This classic challenge has amused people for centuries. Everybody knows that all you need to explore a labyrinth is a ball of string and a piece of chalk. The chalk prevents looping, by marking the junctions you have already visited. The string always takes you back to the starting place, enabling you to return to passages that you previously saw but did not yet investigate.

How can we simulate these primitives, chalk and string, on a computer? The chalk marks are easy: for each vertex, maintain a Boolean variable indicating whether it has been visited. For the ball of string, the correct analog is a stack. After, the exact role of the string is to offer two primitive operations—unwind to get to a new junction (the stack equivalent is to push the new vertex) and rewind to return to the previous junction (pop the stack).

Instead of explicitly maintaining a stack, we will do so implicitly via recursion (which is implemented using a stack of activation records). The resulting algorithm