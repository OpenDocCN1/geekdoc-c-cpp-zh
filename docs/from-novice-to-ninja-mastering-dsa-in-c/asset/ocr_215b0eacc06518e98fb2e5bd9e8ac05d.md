# Example:

+   1. Given items with weights [2, 3, 4, 5] and values [3, 4, 5, 6], and a knapsack capacity of 5, the maximum value is 11 (selecting items with weights 2 and 3).

# Key Takeaways:

+   > These case studies illustrate the versatility and power of dynamic programming in solving problems with optimal substructure and overlapping subproblems.
+   > Memorization and tabulation techniques provide efficient solutions to complex problems, optimizing both time and space complexity.
+   > The principles learned from these case studies can be applied to a wide range of optimization problems in various domains.

# Chapter 9: Greedy Algorithms

# Introduction to Greedy Algorithms - Optimizing Locally for Global Solutions

# Overview of Greedy Algorithms:

Greedy algorithms are problem-solving strategies that make locally optimal choices at each stage with the hope of finding a global optimum. These algorithms aim to achieve the best possible solution at each step without considering the entire problem in its entirety.

# Key Characteristics:

# Greedy Choice Property:

+   1. Greedy algorithms make choices that seem best at the current moment without reconsidering them in future steps.
+   2. The strategy is to pick the locally optimal solution with the expectation that it will contribute to the overall optimal solution.

# Lack of Backtracking:

+   1. Unlike dynamic programming, greedy algorithms do not revisit or revise choices made in the past.
+   2. Decisions are made in a one-time forward pass, with no backtracking or reconsideration.

# Suitable Problems:

+   1. Greedy algorithms are effective for problems with optimal substructure and the greedy choice property.