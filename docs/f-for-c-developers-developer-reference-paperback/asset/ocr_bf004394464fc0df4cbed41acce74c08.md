```
let rec treeHeight tree =
  match with
  | Nil -> 0
  | Node(v, left, right) ->
    let leftHeight = treeHeight left
    let rightHeight = treeHeight right
    (max leftHeight rightHeight) + 1

let rec treeDiameter tree =
  match with
  | Nil -> 0
  | Node(v, left, right) ->
    let leftHeight = treeHeight left
    let rightHeight = treeHeight right
    let leftDiameter = treeDiameter left
    let rightDiameter = treeDiameter right
    max (leftHeight + rightHeight + 1)
    (max leftDiameter rightDiameter)

treeDiameter(createBinaryTree())
```

Note If the data structure is a DU, it's common to see many match statements in the code to decompose the DU.

Find the lowest common ancestor Given two nodes in a binary tree, one common operation is used to find the lowest common ancestor (LCA) for these two nodes. For example, the ancestors for 2 and 1 in Figure 7-15 are 6 and 4, but 4 is lower than 6, so the LCA for 2 and 1 is 4. Listing 7-30 takes two nodes and returns the LCA of these two nodes.

![](bbox=[0.1635, 0.6115, 0.3565, 0.8065])

FIGURE 7-15 Finding the LCA in a binary tree