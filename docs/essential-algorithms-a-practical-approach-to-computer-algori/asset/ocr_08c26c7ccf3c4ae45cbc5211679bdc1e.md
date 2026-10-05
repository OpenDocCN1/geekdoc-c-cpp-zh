# 312 Chapter 12 Decision Trees

Perhaps the ideal approach is to let the algorithm run continuously, updating its best solution when it finds improvements, until you stop it. That if you don't need a solution in a hurry, you can let the algorithm run for hours or possibly even days.

# Improving Paths

You can make random path selection more effective if you pick a random path and then try to improve it. Start with a random path. Then randomly pick an item, and switch it from the group it is to the other group. If that improves the partitioning, keep that change. If change doesn't help, undo it and try again. Repeat this many times until you can't improve the path any more.
 technique has many variations. For example, instead of swapping random items, try swapping each item at a time. You might want to repeat that several times, because swapping one item may change the weights of the two groups so that it is now possible to swap some other item that you could not swap before.

The following pseudocode shows this algorithm:

```
MakeImprovements())
  Initialize best solution so it is replaced by the test solution
  For i = 1 To num_trials
    // Make a random initial solution.
    For index = 0 To max_index
      <Randomly assign item number index to group 0 or 1>
    Next index

    // Try to improve the solution.
    Boolean: had_improvement = True
    While (had_improvement)
      // Assume this time we won't have any improvement.
      had_improvement = False

      // Try swapping items.
      For index = 0 To max_index
        <Swap item number into the other group>

        // See if this improves the test solution.
        If <this swap improves the test solution> Then
          had_improvement = True
        Else
          <Swap the item back>
      End If
    Next index
Loop
```