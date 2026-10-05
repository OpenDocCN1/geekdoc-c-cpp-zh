# Chapter 13 = Basic Network Algorithms 347

+   c. If nodes i and j are connected by a link i → j, set Distance[i, j] to the cost of link.

+   2. Initialize the Via array:

+   a. For all i and j:

+   If Distance[i, j] < infinity, set Via[i, j] to indicate that the path from i to j goes node j.

+   Otherwise, set Via[i, j] to -1 to indicate that there is no path from node i to node j.

+   3. Execute the following nested loops to find improvements:

```
For node = 0 To N - 1
For from_node = 0 To N - 1
  For to_node = 0 To N - 1
    Integer; new_dist =
      Distance[from_node, via_node] +
      Distance[via_node, to_node]
    If (new_dist < Distance[from_node, to_node]) Then
      // This is an improved path. Update it.
      Distance[from_node, to_node] = new_dist
      Via[from_node, to_node] = via_node
  End
```

```
Next to_node
Next from_node
Next via_node
```

The via_node loop loops through the indices of nodes that could be intermediate nodes and improves existing paths. After that loop finishes, all the shortest paths are complete.

The following pseudocode shows how to use the Distance and Via arrays to find the shortest path from a start node to a destination node:

```
List(Of Integer): FindPath(Integer: start_node, Integer: end_node)
If (Distance[start, end] == infinity) Then
  // There is no path between these nodes.
  Return null
End
```

```
// Get the via node for this path.
Integer: via_node = Via[start_node, end_node]
```

```
// See if there is a direct connection.
If (via_node == end_node)
  // There is a direct connection.
  Return a list that contains only end_node.
```