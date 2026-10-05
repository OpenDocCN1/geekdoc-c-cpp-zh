
can build a reasonably strong Reversi program. For more information on Reversi, including the rules and some notes about strategy, see http://en.wikipedia.org/wiki/Reversi.

The later section “Decision Heuristics” has more to say about heuristics.

## Searching General Decision Trees

By modeling a game's moves as a tree, you convert the problem of picking a good move into a search for the best path through the tree. Similarly, you can model other decision processes with a tree.

For example, consider the partition problem. You have a collection of objects of a given weight (or cost or value or some other measure), and you need to divide them into two groups that have the same total weight. In some cases, this is easy. If you have four objects with weights 2, 4, 1, and 1, it's obvious that you put the largest object in the first group and the other objects in the second group. Similarly, if you have an even number of objects that all have the same weight, you can simply place half in one group and half the other.

The problem is much harder if you have a large number of objects with varying weights. In that case, you can model the process of deciding which objects go in which group by a binary decision tree. The kth level of tree represents decision about the K object. A left branch representing the object in the first group, and a right branch representing the object in the second group.

Figure 12-3 shows a complete decision tree for a partition problem with four objects having weights 2, 4, 1, and 1. A path through the tree represents a complete assignment of objects to the two groups. For example, the path that follows the root’s left branch and the next three right branches puts the first object (weight 2) in the first group and the other objects (weights 4, 1, 1) in the second group. The numbers below the tree show the total weights of the two groups—2 and 6.

![](img/fefa42765c0b410af6705110aea7c0cb_328_0.png)

**Figure 12-3:** You use a decision tree to model the partition problem.

Notice that only two leaf nodes in Figure 12-3 correspond to dividing the objects' weights equally so that both groups have a total weight of 4. The two solutions are basically the same solution with the objects in the two groups switched.

**NOTE** In fact, any solution will have a complementary solution with the two groups switched. If you arbitrarily pick an item and place it in the first group before starting the search, you can shorten the tree by one level. It eliminates solutions that have the chosen item in the second group, but the tree will still contain them if there are.

The decision tree shown in Figure 12-3 is fairly large even though it represents a problem with few objects. For larger problems, if you need to divide 50 objects into two groups, the decision tree holds 2^50 leaf nodes, representing roughly 1.13 × 10^15 possible solutions. If only a few of the arrangements produce an even division of weight, it could be very difficult to find a good solution.

The following section explains the difference between two versions of problems such as the partition problem — one that is very hard to solve, and one that is extremely hard to solve. The sections after that explain general methods you can use to search decision trees efficiently.

## Optimization Problems

Problems as the partition problem often come in two closely related forms. The first form asks if a particular solution is possible. The second form asks you to find the best solution possible.

For the partition problem, the first question asks whether you can divide the objects into two groups with equal weights. The second question asks you to divide the objects into two groups with total weights as close to equal as possible. The second question is called an *optimization problem* because you can divide the objects in many ways, and you must find the optimum division.

The optimization of the version is in some ways easier because it allows approximate solutions. The other version of the problem requires a strictly yes-or-no answer.

For example, suppose you need to divide into two 100 items with a total weight of 400. If you search the decision tree and find an exactly equal division, you know the answer to the first question is yes. However, you might search the tree for hours or even days and never find a division that is exactly equal. In that case, you cannot conclude that no such division exists, only that you have found one.

In contrast, you can easily find solutions to the optimization version of the problem. Those solutions may not be very good, but at least you can find an answer that approximates the best possible solution. If you search the decision tree long enough, usually you can find a solution that is reasonably good, even if it isn't perfect. Of course, you might get lucky and find a solution that divides the objects exactly. If you don't find such a solution, you cannot conclude that no such solution exists, but at least you've found an approximate solution.

The following sections discuss methods you can use to search decision trees. The first two describe methods you can use to solve either the optimization or nonoptimization version of a problem. The final section, on decision tree heuristics, works only on the optimization version of the problem.

## Exhaustive Search

The simplest way to search a decision tree is to visit all its nodes, looking for the best solution. Note that you don't actually need to build a decision tree to search it. You just need to keep track of where you are in the tree. Many algorithms use recursion to pick branches at different levels of the tree, and those recursive calls can keep track of their positions in the tree.

For example, the following pseudocode shows a high-level algorithm that exhaustively searches for a solution to the optimization version of the partition problem:

```
ExhaustiveSearch()
  <Initialize best solution so it is replaced by the
  test solution>
  ExhaustiveSearch(0)
End Start ExhaustiveSearch

ExhaustiveSearch(Integer: next_index)
  // See if we are done.
  If <next_index > max_index>
    // We have assigned all items, so we are at a leaf node.
    <if the test solution is better than the
      best solution found so far, save it>
    Else
      // We have not assigned all items, so we are not at a leaf node.
      <Assign item next_index to group 0>
      ExhaustiveSearch(next_index + 1)
      <Unassign item next_index to group 0>

      <Assign item next_index to group 1>
      ExhaustiveSearch(next_index + 1)
      <Unassign item next_index to group 1>
  End If
```

The Start ExhaustiveSearch initializes the best solution so far. Normally it sets the value of that solution (which, in the case of the partition problem, is the difference between the weights of the two groups) to a very large number, so the first valid solution will be an improvement.

The ExhaustiveSearch method takes a parameter index of the item that it should assign to a group. This is the depth of recursion and the level in the decision tree.

If ExhaustiveSearch has assigned all the items, it compares the test solution to the best solution found so far. If the test solution is an improvement, the method saves it as the new best solution.

If ExhaustiveSearch has not yet assigned every item to a group, it assigns next_index to group 0 and then calls itself recursively to assign the remaining items. After the recursive call returns, the method tries assigning next_index to group 1 and again calls itself recursively to assign the remaining items.

Eventually the recursive calls work their way down the tree until they reach leaf nodes and update the best solution if appropriate.

This basic algorithm is fairly flexible and can be adapted for many different problems. For the partition problem, we use an array to store the test solution and the best solution found so far. The Kth entry in the array should be a 0 or 1 to indicate whether the Kth item is assigned to group 0 or group 1. When the algorithm reaches a leaf node, it should add up the weights of the items in each group and compare the difference to the best distance found so far.
