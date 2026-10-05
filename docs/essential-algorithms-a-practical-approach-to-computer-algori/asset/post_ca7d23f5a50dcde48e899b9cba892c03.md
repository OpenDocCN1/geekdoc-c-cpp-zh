
# Chapter 12 ■ Decision Trees 313

```
// See if this solution is an improvement.
<If the test solution is better than the best solution, save it>
Next i
```

MakeImprovements

The algorithm enters a loop to perform a certain number of trials. For each trial, it picks a random test solution. 

It enters a loop that executes as long as the algorithm finds an improvement for the random test solution. Each time through this improvement loop, the algorithm tries swapping each item into the group to which it's not currently assigned. If swap improves the test solution, the algorithm keeps it. If swap does not improve the test solution, the algorithm undoes it.

After it can find no more improvements, the algorithm compares the test solution to the best solution so far and keeps it if it is better.

You pick the number of trials to run in the same ways you can for the random heuristic described in the previous section. You can let the algorithm run a fixed number of trials—a number of trials that depends on the number of weights being partitioned—until it finds no better solution, or you stop.

Sometimes it is not possible to improve a path by making a single swap. Suppose you are partitioning the weights 6, 5, 5, 5, 3, and 3, and suppose you also pick a random path that makes the two groups [6, 3, 3] and [5, 5, 5] so that the groups have total weights of 12 and 15. Therefore, their total weights differ by 3.

Moving an item from the first group to the second only makes the difference greater, so that won't improve the solution.

If you moved an item with weight 5 from the second group to the first, the groups would be [6, 5, 3, 3] and [5], so their total weights would be 17 and not an improvement.

No single swap can improve this solution. But if you move an item with weight 3 from the first group to the second, and you move an item with weight 5 from the second group to the first, you get the groups [6, 5, 3] and [5, 3]. The groups would then have weights 14 and 13, an improvement over the original solution.

The single swap strategy described in this section won't find this improvement, because it requires you to make two swaps at the same time. Other improvement strategies try swapping two items at the same time. Of course, there are also improvements you cannot make by swapping two items that you can make by swapping three items, so that strategy doesn't always work either. Still, swapping two items at a time isn't too difficult and may result in some improvements, so it is worth implementing.

# Simulated Annealing

Simulated Annealing is an improved version of the simple improvement heuristic described in the preceding section. Simulated annealing initially makes large changes to a solution and over time makes smaller and smaller changes to try to improve the solution.

As mentioned in the preceding section, one problem with the original heuristic is that sometimes moving a single item from group to the other won't let you improve the solution, but moving two items at the same time might. There may be cases where moving two items at the same time won't get you an improvement but moving three will.

Simulated annealing addresses this issue by allowing the algorithm to make large changes to the initial solution. Over time the size of the allowed changes is reduced. Simulated annealing tries smaller and smaller changes until it reaches a test solution that it compares to the best solution so far.

> Simulated annealing is modeled on the way crystals grow in a cooling metal or mineral. When the material is very hot, the molecules move quickly, so their arrangement decreases and structures form, but there is still enough energy to allow structures to merge if that forms a more stable relationship. Eventually the material cools enough that there isn't enough energy to disrupt the molecular structure. If the cooling happened slowly enough, the material should contain only a few very large crystals representing a very stable arrangement of molecules.

Another way to implement simulated annealing is to consider random changes in any complexity. If a change results in an improvement, the algorithm accepts it and continues. If a change doesn't result in an improvement, the algorithm accepts it with a certain probability. That probability decreases, so initially the algorithm may make the solution worse so that it can get later to a better result. Eventually the probability of accepting a non-improving change decreases until the algorithm accepts only changes that improve the solution.

# Hill Climbing

Imagine you're a hiker. It's nighttime, so you can't see very far, and you need to find the way to the peak. You decide to always move in the direction that goes uphill. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

Imagine you're a hiker. It's nighttime, so you can't see very far, and you need to find the way to the peak. You decide to always move in the direction that goes uphill. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

Imagine you're a hiker. It's nighttime, so you can't see very far, and you need to find the way to the peak. You decide to always move in the direction that goes uphill. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

Imagine you're a hiker. It's nighttime, so you can't see very far, and you need to find the way to the peak. You decide to always move in the direction that goes uphill. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

Imagine you're a hiker. It's nighttime, so you can't see very far, and you need to find the way to the peak. You decide to always move in the direction that goes uphill. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

Imagine you're a hiker. It's nighttime, so you can't see very far, and you need to find the way to the peak. You decide to always move in the direction that goes uphill. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

# Chapter 12 ■ Decision Trees 315

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution.

| Step | Group A | Group B | 
| :--- | :--- | :--- |
| 1 | [6, 3, 3] | [5, 5, 5] |
| 2 | [6, 5, 3, 3] | [5] |
| 3 | [6, 5, 3] | [5, 3] |

The single swap strategy described in this section won't find this improvement, because it requires you to make two swaps at the same time. Other improvement strategies try swapping two items at the same time. Of course, there are also improvements you cannot make by swapping two items that you can make by swapping three items, so that strategy doesn't always work either. Still, swapping two items at a time isn't too difficult and may result in some improvements, so it is worth implementing.

# Simulated Annealing

Simulated Annealing is an improved version of the simple improvement heuristic described in the preceding section. Simulated annealing initially makes large changes to a solution and over time makes smaller and smaller changes to try to improve the solution.

As mentioned in the preceding section, one problem with the original heuristic is that sometimes moving a single item from group to the other won't let you improve the solution, but moving two items at the same time might. There may be cases where moving two items at the same time won't get you an improvement but moving three will.

Simulated annealing addresses this issue by allowing the algorithm to make large changes to the initial solution. Over time the size of the allowed changes is reduced. Simulated annealing tries smaller and smaller changes until it reaches a test solution that it compares to the best solution so far.

> Simulated annealing is modeled on the way crystals grow in a cooling metal or mineral. When the material is very hot, the molecules move quickly, so their arrangement decreases and structures form, but there is still enough energy to allow structures to merge if that forms a more stable relationship. Eventually the material cools enough that there isn't enough energy to disrupt the molecular structure. If the cooling happened slowly enough, the material should contain only a few very large crystals representing a very stable arrangement of molecules.

Another way to implement simulated annealing is to consider random changes in any complexity. If a change results in an improvement, the algorithm accepts it and continues. If a change doesn't result in an improvement, the algorithm accepts it with a certain probability. That probability decreases, so initially the algorithm may make the solution worse so that it can get later to a better result. Eventually the probability of accepting a non-improving change decreases until the algorithm accepts only changes that improve the solution.

# Hill Climbing

Imagine you're a hiker. It's nighttime, so you can't see very far, and you need to find the way to the peak. You decide to always move in the direction that goes uphill. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution. This is a simple strategy, but it has a flaw: you might get stuck on a local peak that is not the highest point.

The hill-climbing algorithm is a simple search strategy. It starts with a random solution and then moves to a neighbor that is better than the current solution.
