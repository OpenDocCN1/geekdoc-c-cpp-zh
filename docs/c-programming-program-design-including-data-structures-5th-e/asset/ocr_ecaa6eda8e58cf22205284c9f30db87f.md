Clearly, as $n$ becomes larger and larger, the term $4n + 20$ in $f(n)$ becomes insignificant, and the term $n^2$ becomes the dominant term. For large values of $n$, we can predict the behavior of $f(n)$ by looking at the behavior of $g(n)$. In the algorithm analysis, if the complexity of a function can be described by the complexity of a quadratic function without the linear term, we say that the function is of $O(n^2)$, called Big-O of $n^2$.

Let $f$ and $g$ be real-valued functions. Assume that $f$ and $g$ are nonnegative; that is, for all real numbers $n$, $f(n) \ge 0$ and $g(n) \ge 0$.

**Definition:** We say that $f(n)$ is **Big-O** of $g(n)$, written $f(n) = O(g(n))$, if there exist positive constants $c$ and $n_0$ such that:

$f(n) \le cg(n)$ for all $n \ge n_0$.

# ### EXAMPLE 19-5

Let $f(n) = a$, where $a$ is a nonnegative real number and $n \ge 0$. Note that $f$ is a constant function.

Now:

$f(n) = a \le a \cdot 1$ for all $n \ge a$.

Let $c = a$, $n_0 = a$, and $g(n) = 1$. Then, $f(n) \le cg(n)$ for all $n \ge n_0$. It now follows that $f(n) = O(g(n)) = O(1)$.

From Example 19-5, it follows that if $f$ is a nonnegative constant function, then $f$ is $O(1)$.

# ### EXAMPLE 19-6

Let $f(n) = 2n + 5$, $n \ge 0$. Note that:

$f(n) = 2n + 5 \le 2n + n = 3n$ for all $n \ge 5$.

Let $c = 3$, $n_0 = 5$, and $g(n) = n$. Then, $f(n) \le cg(n)$ for all $n \ge 5$. It now follows that $f(n) = O(g(n)) = O(n)$.

# ### EXAMPLE 19-7

Let $f(n) = n^2 + 3n + 2$, $g(n) = n^2$, $n \ge 0$. Note that:

$3n + 2 \le n^2$ for all $n \ge 4$.