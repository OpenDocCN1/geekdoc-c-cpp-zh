With the graph structure in hand, I can now implement several graph algorithms.

# Depth-first search Depth-first search (DFS) is a search algorithm that traverses the tree down a single branch as far as possible before backtracking. The sample code for the DFS graph is shown in Listing 7-41. The code executed on the graph in Figure 7-18 generates a result such as [Node("1"); Node("2"); Node("3"); Node("4"); Node("5"); Node("6")].

![](bbox=[0.125, 0.185, 0.455, 0.335])

FIGURE 7-18 Sample graph in DGML format

LISTING 7-41 DFS on a graph

```
DFS code in the Portable Class Library Project
type NodeStack = System.Collections.Generic.Stack<Node>
type VisitedList = System.Collections.Generic.List<Node>

let stack = NodeStack()
let visited = VisitedList()

let visit node =
    visited.Add(node)

let ( Visited | _ ) node =
    if visited.Contains(node)
        Some node
    else
        None

let dfsGraph graph(start:Node)=
    stack.Push(start)
    visited.Clear()

while stack.Count > 0 do
    let currentNode = stack.Pop()
    match currentNode with
        | Visited() ->
        | -> =
            visit currentNode
            let nodes =
                currentNode.OutgoingEdges
                | Seq.map (fun edge -> edge.Node)
```