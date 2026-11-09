comes a comparison of terms purely of the problem size. This is true of both time and space requirements.

For example, sorting a small list of jumbled numbers into a ranked linear order can be done by hand, but if the list has millions of numbers, and we want to design a computer program that sorts many such lists, large and small, we will want to design an algorithm that we can program into the computer that is as efficient as possible. It turns out there are an infinite number of inefficient ways to sort a list of numbers, but only a small, finite number of general ways to efficiently do so. It has been proved in fact that for a general list of N numbers, that there is a best efficiency in the worst case, that no algorithm can be designed that can be more efficient for sorting the numbers than a certain lower bound in the costliest operation of the algorithm, that of comparing two numbers. That bound is N lg N comparisons for a general list of N numbers, jumbled in a worst case order for sorting. Common sorting algorithms (*quicksort*, *mergesort*, *insertion sort*, *bubble sort*, etc.) typically have performance that varies between N lg N and N^2, and space requirements that are typically linear in N.

We can formally rank the relative complexity of algorithms with common asymptotic bounds. The focus here is when N grows large. If N is small, constants that accrue due to implementation details and other factors may overturn the relative rankings, but for most instances N need not be very large to make the relative rankings conform to the asymptotic bounds, providing hardware and software are consistent across implementations. And, if we change to new hardware or software across implementations, those rankings will remain the same.

There are three basic bounds that we will consider throughout this text. Remember in what follows that the equals sign, =, is really the verb, "equivalence," and not the arithmetic relation, such as 2 = 2.

+   1. Bounding the time efficiency performance in terms of the worst case, what is known as the asymptotic upper bound, is denoted as:
+   
+      $$f(N)=O(g(N)), \tag{1.1}$$
+   
+      where $N$ is a natural number and there is some positive real number constant $C$ such that
+   
+      $$f(N)=Cg(N), \tag{1.2}$$
+   
+      as $N \to \infty$. This can be recast to show that there may be a non-trivial minimum positive integer, $N_0$, such that:
+   
+      $$|f(N)| \le C|g(N)|, \tag{1.3}$$
+   
+      as $N \to \infty$ and $N > N_0$.
+   
+   2. Bounding the performance more tightly is denoted as:
+   
+      $$f(N)=\Theta(g(N)), \tag{1.4}$$