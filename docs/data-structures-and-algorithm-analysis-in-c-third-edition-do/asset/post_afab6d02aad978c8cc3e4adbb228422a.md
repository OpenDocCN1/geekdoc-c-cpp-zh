
## Sec. 16.3 Numerical Algorithms

otherwise the cost is still $n^2$ multiplying to the evaluation. Even if we multiply the matrix and vector cheaply, we still need to be able to reverse the process. That is, after transforming the two input polynomials by evaluating them, and then pair-wise multiplying the evaluated points, we interpolate those points to get the resulting polynomial that corresponds to multiplying the original input polynomials.

The interpolation step is nearly identical to the evaluation step.

$F_z = A_z^{-1}b' = a'$.

We need to find $A_z^{-1}$. This turns out to be simple to compute, and is defined as follows.

$A_z^{-1} = \frac{1}{n}A_{1/z}$,

In other words, interpolation (the inverse transformation) requires the same computation as evaluation, except that we substitute $1/z$ for $z$ (and multiply by $1/n$ at the end). So, if we can do one fast, we can do the other.

If you examine the example $A_z$ matrix for $n=8$, you see that there are symmetries within the matrix. the top half is identical to the bottom half with subtle changes on some rows and columns. Likewise for the left and right halves. An efficient divide and conquer algorithm exists to perform both the evaluation and the interpolation in $\Theta(n \log n)$ time. This is called the Discrete Fourier Transform (DFT). It is a recursive function that decomposes the matrix multiplications, taking advantage of the symmetries made available by evaluation at the $n$th roots of unity. The algorithm is as follows.

```
Fourier_Transform(double +Polynomial, int n) {
   // Compute the Fourier transform of Polynomial
   // with degree n. Polynomial is a list of
   // coefficients indexed from 0 to n-1. n is
   // assumed to be a power of 2.
  double Even[n/2], Odd[n/2], List1[n/2], List2[n/2];

  if(n==1) return Polynomial[0];

  for (j=0; j<n/2; j++) {
    Even[j] = Polynomial[2*j];
    Odd[j] = Polynomial[2*j+1];
  }

  List1 = Fourier_Transform(Even, n/2);
  List2 = Fourier_Transform(Odd, n/2);
  for (j=0; j<n/2; j++) {
    Imaginary z = pow(E, 2*PI*j/n);
    k = j * (n/2);
    Polynomial[j] = List1[k] + z*List2[k];
  }
  return Polynomial;
}
```

Thus, the full process for multiplying polynomials $A$ and $B$ using the Fourier transform is as follows.

- 1. Represent an $n$-degree polynomial as $2n - 1$ coefficients:

```
$[a_0, a_1, ..., a_{n-1}, 0, ..., 0]$
```

- 2. Perform *Fourier Transform* for the representations for $A$ and $B$

- 3. Pairwise multiply the results to get $2n - 1$ values.

- 4. Perform the inverse *Fourier Transform* to get the $2n - 1$ degree polynomial $AB$.

## 16.4 Further Reading

For further information on Skip Lists, see “Skip Lists: A Probabilistic Alternative to Balanced Trees” by William Pugh [Pug90].

## 16.5 Exercises

- 16.1 Solve Towers of Hanoi using a dynamic programming algorithm.

- 16.2 There are six possible permutations of the lines

```
for (int k=0; k<G.n(); k++)
for (int i=0; i<G.n(); i++)
for (int j=0; j<G.n(); j++)
```

in Floyd's algorithm. Which one gives a correct answer?

- 16.3 Show the result of Floyd's all-pairs shortest-path on the graph of Figure 11.26.

- 16.4 The implementation for Floyd's algorithm in Section 16.1.2 is inefficient for adjacency lists because the edges are visited in a bad order when initializing $D$. What is the cost of this initialization step for the adjacency list? How can this initialization step be revised so that it costs $\Theta(|V|^2)$

- 16.5 State the greatest possible lower bound that you can prove for the all-pairs shortest-paths, and justify your answer.

- 16.6 Show the Skip List that results from inserting the following values. Draw the Skip List after each insert. With each value, assume the depth of its corresponding node is as given in the list.

| value | depth |
| --- | --- |
| 5 | 2 |
| 20 | 0 |
| 30 | 0 |
| 2 | 1 |
| 25 | 3 |
| 26 | |
| 31 | 0 |

- **16.7** If we had a linked list that would never be modified, we can use a simpler approach than the Skip List to speed access. The concept would remain the same in that we add additional pointers to list nodes for efficient access to the ith element. How can we add a second pointer to each element of a singly linked list to allow access to an arbitrary element in O(log n) time?

- **16.8** What is the expected (average) number of pointers for a Skip List?

- **16.9** Write a function to remove a node from a Skip List.

- **16.10** Write a function to find a node in a Skip List.

## 16.6 Projects

- **16.1** Complete the implementation of a Skip List.

- **16.2** Implement a standard algorithm for matrix multiplication.

- **16.3** How big must $n$ be before the algorithm becomes efficient?

## 17. Limits to Computation

This chapter presents a brief introduction to impossible problems. Section 17.1 presents the concept of reduction... 17.2 discusses “hard” problems... 17.3 considers problems that, while simple to define, are impossible to solve.

## 17.1 Reductions

We begin with an important concept for understanding the relationships between problems, called reduction. Reduction allows us to solve one problem in terms of another. Equally importantly, when we wish to understand the difficulty of a problem, reduction allows us to make relative statements about upper and lower bounds on the cost of a problem (as opposed to an algorithm or program).

Because the concept of a problem is discussed extensively in this chapter, we want notation in terms of a mapping between inputs and outputs, and the name of the problem will be defined in all capital letters. Thus, a complete definition of the sorting problem could appear as:

-   SORTING:
**Input:** A sequence of integers $x_0, x_1, x_2, \dots, x_{n-1}$.
**Output:** A permutation $y_0, y_1, y_2, \dots, y_{n-1}$ of the sequence such that $y_i \le y_j$ whenever $i < j$.
