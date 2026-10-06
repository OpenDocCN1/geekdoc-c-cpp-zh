
## 46 Limits of Computation

and this book, we will always assume that f and g are positive-valued, non-decreasing functions defined on the positive integers.

## Definition 3.5 Restated

For positive functions f and g defined on the positive integers, f is $O(g)$ if there exists a positive integer $C$ such that $f(n) \le C g(n)$ for all positive integers $n$.

Sometimes it is convenient to consider $O(g)$ to be a set, and then we say $f \in O(g)$, instead of $f$ is $O(g)$. Some authors will say $O(f) = g$, but this is best avoided.
The distinction between $f \in O(g)$ and $f$ is $O(g)$ is rarely a problem.

## 3.9 USEFUL THEOREMS

The following two theorems are often useful for proving that one function is $O$ of another. Direct limits are often not useful, since any function that describes the order of an algorithm will be increasing, positive, and tend to infinity.

This is a standard case where applying l'Hospital's rule works well.

### Theorem 3.6

If $f$ and $g$ are positive functions,

$$\lim_{x\to\infty} \frac{f(x)}{g(x)} = C$$

for some positive number $C$, then $f$ is $O(g)$.

### Proof

This is a simple application of the definition of limit. If

$$\lim_{x\to\infty} \frac{f(x)}{g(x)} = C$$

then there is a $N$ such that

$$n \ge N, \frac{f(n)}{g(n)} \le C+1$$

### Theorem 3.7 (l'Hôpital's Rule)

If

$$\lim_{x\to\infty} \frac{f(x)}{g(x)}$$

is an indeterminate limit of the form

$$\begin{pmatrix} \infty \\ \infty \end{pmatrix} (\text{or } \begin{pmatrix} 0 \\ 0 \end{pmatrix})$$

then

$$\lim_{x\to\infty} \frac{f(x)}{g(x)} = \lim_{x\to\infty} \frac{f'(x)}{g'(x)}$$

where $f'$ is the derivative of $f$ with respect to $x$.

### Proof

Any standard calculus text. The name l'Hospital is also written Lospital or L'Hôpital. In any event, the $s$ is not pronounced.

Simple application: in $n \ln n$ is $O(n^2)$. Both $(n \ln n)$ and $n^2$ get very large (tend to infinity) as $n$ gets large—as do essentially all functions that count steps in an algorithm. By using L'Hô's rule, we have:

$$\lim_{x\to\infty} \frac{n\ln n}{n^2} = \lim_{x\to\infty} \frac{\ln n}{n} = \lim_{x\to\infty} \frac{1/n}{1} = \lim_{x\to\infty} \frac{1}{n} = 0$$

## 48 Limits of Computation

## 3.10 PROPERTIES OF O NOTATION

The following properties are useful; all are easy to prove.

- $f$ is $O(f)$ for all $f$.
- $f$ is $O(1)$ if and only if it is a bounded function.
- Constant factors can be ignored in any $O$ calculations; that is, $Kf(n)$ is $O(f(n))$ for any positive constant $K$.
- $\log_a$ is $O(\log_b n)$ for any bases $a$ and $b, b > 1$.
- $\log_b n$ is $O(n)$ for any base $b, b > 1$.
- $n^k$ is $O(b^n)$ for all $b > 1, k \ge 0$. Thus $n^5$ and $n^{51}$ are both $O(2^n)$.
- If $r \le s$, then $n'$ is $O(s')$.
- Any polynomial $p(n)$ is $O(\text{the highest-order term in } p)$. (Thus $7n^5 + 11n^2 + 5n + 1111$ is $O(n^5)$).
- For all $k > 0, k$ is $O(f)$.
- Iff $f$ is $O(g)$ and $h$ is $O(g)$, then $f + h$ is $O(g)$.
- If $f$ is $O(h)$ and $g$ is $O(h)$, then $f + g$ is $O(h)$.
- If $f$ is $O(h_1)$ and $g$ is $O(h_2)$, then $f + g$ is $O(\max(h_1, h_2))$.
- If $f$ is $O(h_1)$ and $g$ is $O(h_2)$, then logic follows.

## 3.11 FINDING O: ANALYZING AN ALGORITHM

Analyzing an algorithm involves making assumptions. Two notes: (1) As usual, we do not care about the best case, and (2) if the algorithm is a search-decision problem.

### Example: Does a list contain a certain element?

```
Algorithm: (1) element = false
(2) for each element in list
(3) if element == key
    element = true
(4) return element
```

### Example: Greatest Common Divisor (GCD)

```
Algorithm: (1) while m != 0
  (2) r = n mod m
  (3) n = m
  (4) m = r
(5) return n
```
