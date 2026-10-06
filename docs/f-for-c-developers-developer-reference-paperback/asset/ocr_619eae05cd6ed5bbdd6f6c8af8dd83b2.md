```
let openList = Path()
let closedList = Path()
```

```
open System.Collections.Generic
open System.Linq
```

```
let getNeighbors (currentNode:Node) =
    currentNode.OutgoingEdges
|> List.map(fun edge -> edge.ToNode)
|> List.Filter(fun node -> not < closedList.Contains(node))
```

```
let getCost(node:Node, currentNode:Node) =
    let (Some edge) =
        currentNode.OutgoingEdges
        |> List.tryFind(fun edge -> edge.ToNode = node)
edge.Data
```

```
let `Dijkstra's algorithm` = startPoint
openList.Add(startPoint)
startPoint.Data < 0
while openList.Count > 0 do
    let currentNode = openList |> List.minBy(fun n -> n.Data)
    let neighbors = getNeighbors currentNode
    |> List.Filter(fun node ->n        let distance = getCost(node, currentNode)
        node.Data <- min(currentNode.Data + distance) node.Data)
    openList.AddRange(neighbors)
    ignore <| openList.Remove(currentNode)
closedList.Add(currentNode)
```

> Note You have added System.Xml and System.Ling to the project references.

# Examining Other Samples

This section gives you useful options to try.

Combination is an approach to select several items out of a larger collection. Unlike the permutation approach, combination does not care about the order. Listing 7-46 shows how to get a combination from a collection of elements.

LISTING 7-46 Getting a combination from a list

```
let getCombination(list:list) elementNeeded =
let rec getCombinationFunction(list:list) elementNeeded currentList =
    if elementNeeded = 0 then
        [ currentList ]
    else
        [ for n in list do
```