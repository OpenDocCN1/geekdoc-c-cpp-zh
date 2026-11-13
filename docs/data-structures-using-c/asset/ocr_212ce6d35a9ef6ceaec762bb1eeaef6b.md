# Big Omega (Ω)

Definition The function f(n) = Ω(g(n)) is called 'f(n) is omega of g(n)' if and only if there exist positive constants c and N such that f(n) ≥ c × g(n) for all n ≥ N.

# Big Theta (Θ)

Definition The function f(n) = Θ(g(n)) is called 'f(n) is theta of g(n)', if and only if there exist positive constants c and N such that f(n) ≤ c × g(n) for n ≥ N.

Algorithms can be iterative or recursive; can make decisions randomly or approximately; can propagate the decision-making policies in the forward or backward manner. The algorithmic strategies work on all such characteristics and are broadly classified as follows:

+   1. Divide-and-conquer
+   2. Greedy method
+   3. Dynamic programming

The study of algorithm and design strategies

+   1. makes available templates suitable for solving a set of diverse problems;
+   2. can be translated into common control and data structures provided by most high-level languages;
+   3. analyses the temporal and spatial requirements of the algorithms in a precise manner.

# 16.2 DIVIDE-AND-CONQUER

Divide-and-conquer is one of the most popular algorithmic strategies. It works in two phases. In the first phase, the problem is divided into subproblems of smaller size till each problem can be easily solved. In the latter phase, the solutions to all such subproblems are gathered together to get the final solution. This approach, especially when used recursively, often yields efficient solutions to problems in which the subproblems are smaller versions of the original problem and can be independently solved.

Often, even the subproblems are relatively large, and the divide-and-conquer strategy is reapplied. In addition, the subproblems resulting from a divide-and-conquer design are of the same type as the original problem. For those cases, applying this design again is naturally expressed by a recursive procedure. The process of splitting the input into distinct subsets continues till these smaller subproblems, which are of the same kind, are small enough to be solved without further splitting.

# 16.2.1 Unique Characteristics and Use

Popularly, the divide-and-conquer strategy is designed keeping in mind a single processor computer. However, it is ideally suited for parallel computations as each subproblem can be solved simultaneously by its own processor. The following are some unique characteristics of the divide-and-conquer method:

+   1. The divide-and-conquer technique is well suited when a data set can be divided into smaller subsets of data elements and each data set can be independently processed.