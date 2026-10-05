# Appendix A Summary of Algorithmic Concepts 481

Recursive approach— Recursive algorithm calls itself to solve a smaller problem. When the recursive calls reach a point where the problem is small enough, the algorithm solves it without recursion and returns to the calling instance.

Recursive definitions—Some sequences, such as the factorial and Fibonacci numbers, have natural recursive definitions. These lead easily to recursive algorithms, although they are not as efficient as nonrecursive algorithms.

Self-similar fractals are curves that start with an initiator and then recursively replace parts of the curve with a suitably scaled, rotated, and translated generator curve.

Backtracking is a recursive algorithm that considers partial solutions. If it finds a partial solution that cannot be extended to a full solution, the algorithm discards the partial solution, backtracks to the previous feasible solution, and continues searching from there.

A selection is an unordered subset of set of objects. The number of selections without duplicates of k items taken from a total of n items is given by this equation:

```
$$\frac{n}{k} = \frac{n!}{k!(n-k)!}$
```

Tail recursion removal—You can replace tail recursion with a loop that resets parameters before the end of the loop.

Storing intermediate values—If a calculation such as the Fibonacci numbers recalculate the same values many times, you can save time by storing values in a lookup table so you can calculate them only once

General recursion removal—You can remove recursion more generally by mimicking how a program calls a method recursively. Push variables onto stacks before recursion, and pop them off afterwards.

# Chapter 10: Trees

Many algorithms use trees, it's important to remember at least the most basic tree properties.

Logarithmic growth—If a tree is reasonably balanced

Lots of leaves—If a tree is reasonably balanced, roughly half its nodes are leaves.

Inductive reasoning—Proof by induction is a useful technique for proving tree theorems.

Branches and object references—You can use object references or pointers to link a node to its children. You can use similar references to create threads through trees. You also can use similar references to build networks.