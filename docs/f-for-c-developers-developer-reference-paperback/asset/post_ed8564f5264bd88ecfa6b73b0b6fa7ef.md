
With the graph structure in hand, I can now implement several graph algorithms.

## Depth-first search

Depth-first search (DFS) is a search algorithm that traverses the tree down a single branch as far as possible before backtracking. The sample code for the DFS graph is shown in Listing 7-41. The code executed on the graph in Figure 7-18 generates a result such as [Node("1"); Node("2"); Node("3"); Node("4"); Node("5"); Node("6")].

![](img/63aaf94e22830ab98ce16c5946be8ef6_449_0.png)

FIGURE 7-18 Sample graph in DGML format

### LISTING 7-41 DFS on a graph

```fsharp
DFS code in the Portable Class Library Project
type NodeStack = System.Collections.Generic.Stack<Node>
type VisitedList = System.Collections.Generic.List<Node>

let stack = NodeStack()
let visited = VisitedList()

let visit node =
    visited.Add(node)

let (| Visited | _ ) node =
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
        | _ ->
            visit currentNode
            let nodes =
                currentNode.OutgoingEdges
                |> Seq.map (fun edge -> edge.Node)
                |> Seq.distinctBy (fun node -> node.ID)
                |> Seq.toList
            nodes
            |> Seq.iter (fun node -> stack.Push node)

// Invoker code
```fsharp
let g = DGML.Graph.DGMLReader(new System.IO.StreamReader("C:\My\ConsoleApplication\Graph1.dgml"))
let (Some startNode) = g.Graph.FindNode("1")
DGMLGraph.DfsGraph g startNode
printf("%A", (Seq.toList DGMLGraph.visited))
```

Breadth-first search (BFS) differs from DFS in only how it stores nodes. DFS uses a stack, and BFS uses a queue. Listing 7-42 provides a BFS sample.

### LISTING 7-42 A BFS graph sample

```fsharp
type NodeQueue = System.Collections.Generic.Queue<Node>
type VisList = System.Collections.Generic.List<Node>

let queue = NodeQueue()
let visited = VisList()

let visit node =
    visited.Add(node)

let (| Visited | _ ) node =
    if visited.Contains(node) then
        Some node
    else
        None

let bfs graph (start:Node)=
    queue.Enqueue start
    visited.Clear()

while queue.Count <> 0 do
    let currentNode = queue.Dequeue()
    match currentNode with
    | _ ->
        visit currentNode
        let nodes =
            currentNode.OutgoingEdges
            |> Seq.map (fun edge -> edge.ToNode)
            |> Seq.distinctBy (fun node -> node.ID)
            |> Seq.toList
        |> Seq.iter (fun node -> queue.Enqueue node)
```

## Find all paths in a graph

Another way to represent a graph is to use a matrix. Listing 7-43 shows how to access the graph and find all possible paths from one to another. If the element in the matrix is 1, that is a passage. If the element in the matrix is 0, it is a blocker. The sample code finds all of paths from (0,0) to (4,2).

### LISTING 7-43 Finding all paths in a graph

```fsharp
type Location = { X : int; Y : int }
type Path = { Location list }

let graph = {
    [1:1:1;1:0]
    [0:1:0;1:0]
    [0:0:1;1:1]
    [0:1:1;1:0]
    [0:1:0;1:0]
}

let getNeighbors(point:Location) =
    let getLeft(point:Location) =
        if point.X = 0 then None
        else { X = point.X - 1; Y = point.Y }
    let getTop(point:Location) =
        if point.Y = 0 then None
        else { X = point.X; Y = point.Y - 1 }
    let getRight(point:Location) =
        if point.X = 4 then None
        else { X = point.X + 1; Y = point.Y }
    let getBottom(point:Location) =
        if point.Y = 4 then None
        else { X = point.X; Y = point.Y + 1 }
    let result =
        [getLeft point;
         getTop point;
         getRight point;
         getBottom point]
        |> List.filter(fun n -> match n with Some _ -> true | None -> false )
        |> List.map(fun n -> n)
        |> List.filter(fun n -> not graph.[n.Y][n.X] < 0)
```

```fsharp
rec findAllPath(startPoint:Location)(endpoint:Location)(path:Path)=
    if startPoint = endpoint then
        [ path ]
    else
        let neighbours =
            getNeighbors startPoint
        |> List.filter(fun n -> not (path |> List.exists(fun x -> x=n)))
        for n in neighbours do
            for path in findAllPath n endpoint (n::path) do
                if path.Length > 0 then
                    yield path
                else
                    []
```

```fsharp
let start = { X = 0; Y = 0 }
let endpoint = { X = 4; Y = 2 }
let path = [start]
```

> Note In Portable Class Library project, `List<T>` is still present. You can replace it with F# lists to take advantage of immutability.

The A* algorithm (pronounced A star) is another graph algorithm. The graph is represented in a matrix, where 0 cannot be passed. There is an openList and a closedList. The openList keeps track of the unvisited nodes and the closedList nodes that have already been processed. The node cost is computed from two nodes: H is a heuristic cost that is estimate from current node. On the way to your destination, the H value plays a role in your decision when making a move closer to or further from the destination. This is how A* works. The algorithm starts from the openList with a starting point, and TotalCost set to 0. During each iteration, the minimum TotalCost node is taken from the openList and denoted as currentNode. The neighbor nodes are retrieved and put on the openList as long as they are not visited and not on closedList. The MoveCost value of neighbor is computed from the current node. If the cost is less than the current value, which means the current node is a better choice, the node's PreviousNode is set to currentNode. When all of the target nodes are closed or openList is empty, as shown in Listing 7-44.

### LISTING 7-44 A* algorithm sample

```fsharp
type Location = { X : int; Y : int }

type Node() as this =
    member IsBlock = false
    member val PreviousNode: Node option = None
    member val Location = { X = 0; Y = 0 }
    member val H = 0
    member val MoveCost = 1000
    member this.TotalCost = this.MoveCost + this.H

type Path = Location list

let graph = [
    [1:1:1:1:1:1]
    [1:1:1:0:1:1]
    [1:1:1:0:1:1]
    [1:1:1:0:1:1]
    [1:1:1:1:1:1]
    [1:1:1:1:1:1]
]

let nodeGraph = (
  graph
  |> List.map (fun x ->
    |> List.map (fun y ->
      let loc = {X = x; Y = y}
      Node(IsBlock=(if y = 1 then false else true), Location = loc)))

let rightMax = 6

let getNeighbors(point:Location) =
    let getLeft(point:Location) =
        if point.X = 0 then None
        else { X = point.X - 1; Y = point.Y }
    let getTop(point:Location) =
        if point.Y = 0 then None
        else { X = point.X; Y = point.Y - 1 }
    let getRight(point:Location) =
        if point.X = rightMax then None
        else { X = point.X + 1; Y = point.Y }
    let getBottom(point:Location) =
        if point.Y = rightMax then None
        else { X = point.X; Y = point.Y + 1 }
    let getLeftTop(point:Location) =
        if point.X = 0 || point.Y = 0 then None
        else { X = point.X - 1; Y = point.Y - 1 }
    let getRightTop(point:Location) =
        if point.X = rightMax || point.Y = 0 then None
        else { X = point.X + 1; Y = point.Y - 1 }
    let getRightBottom(point:Location) =
        if point.X = rightMax || point.Y = rightMax then None
        else { X = point.X + 1; Y = point.Y + 1 }
    let getLeftBottom(point:Location) =
        if point.X = 0 || point.Y = rightMax then None
        else { X = point.X - 1; Y = point.Y + 1 }
    let result =
        [(10, getLeft point); (10, getTop point); (10, getRight point); (10, getBottom point);
        (14, getLeftTop point); (14, getRightTop point); (14, getRightBottom point);
        (14, getLeftBottom point)]
    result
```
