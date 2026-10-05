# Chapter 12 = Decision Trees

```
<Assign item next_index to group 1>
BranchAndBound(next_index + 1)
<Unassign item next_index to group 1>
End If
BranchAndBound
```

This algorithm is similar to the exhaustive search algorithm, except that it determines the test solution can be improved to beat the best solution, and it returns if it can't.

Branch and bound often trims branches and its subtrees from the decision tree, so it can be much faster than an exhaustive search.

For example, in one test, while trying to divide 20 items into 2,097,150 nodes, but a branch and bound visited 774,650 nodes. When both algorithms were allowed to use the “short circuit” described in the preceding section to stop early, the exhaustive search visited 4,082 nodes, but the branch and bound search visited 298 nodes.

Branch and bound is a very useful technique, but I want to mention two important factors before moving on decision tree heuristics. First, branch and bound search any path through the tree that might lead to a better solution found so far. That means, unlike exhaustive search, it always finds the optimal solution.

The second important fact is that, although branch and bound avoids searching large parts of the decision tree, decision trees can be enormous, so branch and bound can still be fairly slow.

In one test, exhaustive search could search a decision tree for a 25-item problem in 6.6 seconds. Branch and bound could search the same tree in 2 seconds. That’s a big improvement, but adding new item to the problem doubles the tree’s size. Adding one more item made by branch and bound take about 4 seconds, and adding a second item made it 7.9 seconds.

Branch and bound is much faster than exhaustive search, but it still isn't fast enough to search a big decision tree like the 2.2 trillion node tree representing the partition problem with 40 items.

# Decision Tree Heuristics

Exhaustive search and branch and bound find the best possible solution. Unfortunately, decision trees are so large that those algorithms work only for relatively small problems.

To search larger trees, you need to use heuristics. A heuristic won’t necessarily find the best possible solution, but it might find a good solution—at least for the optimization version of a problem where approximate solutions make sense.