# Chapter 6 Algorithms and complexity

swap operations were more than values to sort. Hence, knowing the nature of the input to a particular problem can inform us about how best to solve that problem.

# 6.4.2 Resource scarcity: complexity of algorithms

In addition to the subtleties of bubble sort introduced above, there are more important qualities of algorithms that result directly from the reality of modern computation. The most obvious answer to a process requires time: there will usually be a time-scale in which a task is expected to complete. This is normally achieved by some interaction with a human being (who, for example, might not wish to wait ten minutes while a computer sorts a scheduler's values), also can be restricted by the needs of other computer systems. Many biological databases, as discussed in Chapter 3, hold quantities of data, and are growing exponentially. Taking, for example, ENA's tally of >230 terabytes of data (Section 3.1), it's clear that developing algorithms for dealing with these size is of paramount importance.

The speed of an algorithm can be described by its time complexity: a measure of how well it performs, in relation to the size of the data it's meant to work on. This measure is often described using the ‘big O notation’, which is mathematical terminology used to describe the behaviour of a function as a particular value (in our naive bubble sort example tends to infinity). In general, it can be thought of as a measure of the algorithms with scaled-up input.

Counting the number of comparisons required in a sorting algorithm is often the best measure of performance; in the algorithm in Figure 6.7, $n-1$ pairs are compared with each other in $n-1$ passes. For a list of size $n$, $(n-1)(n-1)$ comparisons are required to sort the list. The largest-order component $n^2-2n+1$, is $n^2$; therefore, as $n$ tends to infinity, this dominates the behaviour of the algorithm. This gives us bubble sort formulation a time complexity of $O(n^2)$. Even if the naivety were removed, and the algorithm implemented as efficiently as possible, thereby speeding up the general case, it would still exhibit a time complexity of $O(n^2)$. Table 6.1 shows the ordering of some big O magnitudes, and how they measure an algorithm's behaviour (here, the time it takes to complete) as the input size changes.

For small inputs, this tends not to be an issue: modern computers are fast enough, and have enough RAM, to be able to mitigate the effects of inefficient algorithms. However, with increased input sizes, complexity begins to dominate, and

# Table 6.1

Descriptions of how some big O magnitudes behave when the size of input changes. The list begins with the best possible behaviour, O(1), and gets progressively worse.

| Complexity | Description |
| O(1) | The measure remains constant regardless of the size of input. |
| O(log n) | The measure behaves logarithmically in relation to the input size. |
| O(n) | The measure is linearly proportional to the input size. |
| O(n log n) | Linearith behaviours fall between linear and polynomial. |
| O(n²) | Doubling the input size quadruples compared with input size. |
| O(2^n) | The measure increases exponentially compared with input size. |
| O(n!) | The measure increases factorially compared with input size. |