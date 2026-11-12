
false for all $k$ iterations (i.e., that Snape’s algorithm does not work) is:

$$\prod_{i=1}^{k}\Pr(X_i=0)$$
$$=\left(1-\frac{2}{n}\right)^k$$

We want to determine the minimum value of $k$ for which Snape’s algorithm works, that is, the minimum value of $k$ such that the probability of failure is no more than $\frac{1}{3}$:

$$\left(1-\frac{2}{n}\right)^k\leq\frac{1}{3}$$

Solving for $k$, we determine that:

$$k\geq\frac{\log_e\frac{1}{3}}{\log_e\left(1-\frac{2}{n}\right)}$$

We now recall the following math fact

$$\left(1-\frac{1}{x}\right)^x\leq\frac{1}{e}$$

From this, we calculate that:

$$\log_e\left(1-\frac{1}{x}\right)\leq-\frac{1}{x}$$

We then conclude the following:

$$k\geq\frac{\log_e\frac{1}{3}}{\log_e\left(1-\frac{2}{n}\right)}$$
$$k\geq\frac{n\log_e\frac{1}{3}}{-2}$$
$$k\geq\frac{n\log_e 3}{2}$$

We conclude that Snape’s algorithm is correct only if $k=\Omega(n)$.

2. Since the question only asked the asymptotic number of balls drawn, $\Theta(1)$ (plus some justification) is a sufficient answer. Below we present a more complete answer.

   Assume you draw $k$ balls from the bag (replacing each ball after examining it).

### Lemma 3

For some constant $k$ sufficiently large, at least one ball is blue with probability $\frac{2}{3}$.

## 1.6. Is this (almost) sorted?

**Proof** Define indicator random variables as follows:

$$X_i=\begin{cases}1,&\text{if ball }i\text{ is blue},\\0,&\text{if ball }i\text{ is red.}\end{cases} \tag{1.2}$$

Notice, then, that $\Pr X_i=1=\frac{1}{10}$ and $\Pr X_i=0=\frac{9}{10}$. We then calculate the probability that at least one ball is blue:

$$=1-\prod_{i=1}^{k}\Pr(X_i=0)$$
$$=1-\left(\frac{9}{10}\right)^k$$
$$\ge \frac{2}{3}.$$

Therefore, if $k\ge \frac{\log(1/3)}{\log(9/10)}$, the probability of drawing at least one blue ball is at least $\frac{2}{3}$.

## 3. An example of a binary-search decision tree of an unordered array:

![](img/78e1bff64796dccbf49e7c84b8201fb2_51_0.png)

For the purpose of understanding this problem, think of the decision-tree version of the binary search algorithm. (Notice that unlike sorting algorithms, the decision tree for binary search is relatively small, i.e., $O(n)$ nodes.)

Consider the example in the figure provided earlier, in which a binary search is performed on the unsorted array $[9\ 7\ 10\ 15\ 16\ 20\ 25\ 22]$. Assume $key_1=20$ and $key_2=25$. Both 20 and 25 are $\ge 15$, and choose the right branch at the root. At this point, the two binary searches diverge: $20<25$ and $25\ge25$. Therefore $key_1$ takes the left branch and $key_2$ takes the right branch. This ensures that eventually $key_1$ and $key_2$ are ordered correctly.

We now generalize this argument. For $key_1$, let $x_1, x_2,\ldots,x_k$ be the $k$ elements that are compared against $key_1$ in line 6 of the binary search (where $k=O(\log n)$). (In the example, $x_1=15, x_2=25$, and $x_3 = 20$.) Let $y_1,y_2,\ldots,y_t$ be the $t$ elements compared against $key_2$. We know that $x_1 = y_1$. Let $l$ be the smallest number such that $x_l \ne y_l$. (In particular, $l > 1$.) Since $i < j$, by assumption, we know that $key_1$ cannot branch right while $key_2$ simultaneously branches left. Hence we conclude that

$$key_1 < x_{l-1}=y_{l-1}\le key_2$$

(Note that a relatively informal solution was acceptable for the problem, as we simply asked that you *explain why* this is true. The above argument can be more carefully formalized.)

4. **Overview:** In order to show the algorithm correct, there are two main lemmas that have to be proved:
   - a) If the list $A$ is sorted, the algorithm always returns *true*;
   - b) If the list $A$ is not 90% sorted, the algorithm returns false with probability at least $\frac{2}{3}$.

   We begin with the more straightforward lemma, which essentially argues that binary search is correct. We then show that if the list is not 90% sorted, then at least 10% of the elements fail the *binary search test*. Finally, we conclude that for a sufficiently large constant $k$, if the list is not 90% sorted, then the algorithm will output false with probability at least $\frac{2}{3}$.

### Lemma 4

If the list $A$ is *sorted*, the algorithm always returns *true*.

**Proof** This lemma follows from the correctness of binary search on a sorted list, which was shown in recitation one. The invariant is that $key$ is in array $A$ between *left* and *right*.

For the rest of this problem, we label the elements as *good* and *bad* based on whether they pass the binary search test.

$$\operatorname{label}(i)=\begin{cases}\mathit{good}, & \text{if } i=\operatorname{BINARY-SEARCH}(A,A[i],1,n),\\ \mathit{bad}, & \text{if } i\ne\operatorname{BINARY-SEARCH}(A,A[i],1,n).\end{cases}\qquad (1.3)$$

Notice that it is not immediately obvious which elements are good and which elements are bad. In particular, some elements may appear to be sorted correctly, but be bad because of other elements being missorted. Similarly, some elements may appear entirely out of place, but be good because of other misplaced elements. A key element of the proof is showing that a badly sorted list has a lot of bad elements.

### Lemma 5

If the list $A$ is not 90% sorted, then at least 10% of the elements are bad.

**Proof** Assume, by contradiction, that fewer than 10% of the elements are bad. Then, at least 90% of the elements are good. Recall the definition of a 90% sorted list: if 10% of the elements are removed, then the remaining elements are in sorted order. Therefore, remove all the bad elements from the array. We now argue that the remaining elements are in sorted order. Consider any two of the remaining good elements, $key_i$ and $key_j$, where $key_i$ is at index $i$ and $key_j$ is at index $j$. If $i < j$, then solution to third part shows that $key_i \le key_j$. Similarly, if $j < i$, then third part shows that $key_j \le key_i$. That is, the two elements are in correctly sorted order. Since all pairs of elements are in sorted order, the array of good elements is in sorted order. Once we have shown that there are a lot of bad elements, it remains to show that we find a bad element through random sampling.

### Lemma 6

If the list is not 90% sorted, the algorithm returns false with probability at least $\frac{2}{3}$.

**Proof** From Lemma 5, we know that at least 10% of the elements are bad. From second part, we know that if we choose $k > \frac{\log(1/3)}{\log(0.9)}$ then with probability $\frac{2}{3}$ we find a bad element. Therefore, we conclude that the algorithm returns *false* with probability at least $\frac{2}{3}$.

5. Lemma 4 is the same as in fourth part. A simple modification of Lemma 5 shows that if the array is not $(1-\epsilon)$-sorted, then there must be at least $\epsilon$ bad elements; otherwise, the remaining $(1-\epsilon)n$ elements would form a $(1-\epsilon)$-sorted list. Finally, it remains to determine the appropriate value of $k$.

In this case, we want to choose $k$ such that

$$ (1 - \epsilon)^k \leq \frac{1}{3} $$

We choose $k = \frac{c}{\epsilon}$, then we can conclude that

$$ (1 - \epsilon)^k \leq \left((1 - \epsilon)^{\frac{1}{\epsilon}}\right)^c $$
$$ (1 - \epsilon)^k \leq \left(\frac{1}{e}\right)^c $$

### Lemma 7

INSERTION-SORT(A) runs in time O(n+I), where I is the number of inversions in A.

**Proof** Consider an execution of INSERTION-SORT on an array A. In the outer loop, there is O(n) work. Each iteration of the inner loop fixes exactly one inversion. When the algorithm terminates, there are no inversions left. Hence, there must be I iterations of the inner loop, resulting in O(I) work. Therefore the running time of the algorithm is O(n+I).

We next count the number of inversions in an array in which every element is within k slots of its proper position.

### Lemma 8

If every element is within k slots of its proper position, then there are at most O(nk) inversions.

**Proof** We provide an upper bound on the number of inversions. Consider some particular element, A[i]. There are at most 4k elements that can be inverted with A[i], in particular those elements in the range A[i−2k..i+2k]. Therefore, i is a part of at most 4k inversions, and hence there are at most 4nk inversions.

From this we conclude that the running time of insertion sort on an array in which every element is within k slots of its proper position is O(nk).

As a side note, it seems possible to prove this directly, without using inversions, by showing that the inner loop of insertion sort never moves an element more than k slots. However, this is not as easy as it seems: even though an element always begins within k slots of its final position, it is necessary to show that it never moves farther away. For example, what if it moves k+2 slots backwards, and then is later moved 3 slots forward? However, perhaps one can show that an element never moves more than 4k slots.

3. We already know that sorting the array requires Ω(n log n) comparisons. If k > n/2, then n log n = Ω(n log k), and the proof is complete. For the remainder of this proof, assume that k ≤ n/2.

   Our goal is to provide a lower-bound on the number of leaves in a decision tree for an algorithm that sorts an array in which every
