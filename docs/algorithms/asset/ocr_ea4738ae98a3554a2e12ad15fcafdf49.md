# 38

# Exercises

random from among family $\mathcal{H}$ of functions. In our example,

$\mathcal{H} = \{h_a : a \in \{0, \dots, n-1\}^k\}$.

To draw a hash function uniformly from this family, we just draw four numbers $a_1, \dots, a_k$ modulo $n$. (Incidentally, notice that the two simple hash functions considered earlier, namely the last or the first 8-bit segment, belong to this class. We have $h_{(0,0,0,1)}$ and $h_{(1,0,0,0)}$, respectively.) And we insisted that the family have the following property:

+   For any two distinct items $x$ and $y$, exactly $|\mathcal{H}|/n$ of all the hash functions in $\mathcal{H}$ map $x$ and $y$ to the same bucket, where $n$ is the number of buckets.

A family of hashes with this property is called *universal*. In other words, for any two items, the probability these collide is $1/n$ if the hash function is randomly drawn from a universal family. This is also the collision probability if we map $x$ and $y$ to buckets uniformly at random—in some sense the gold standard of hashing. We then showed that this property implies hash table operations have good performance in expectation.

This idea, motivated as it was by the hypothetical IP address application, can be applied more generally. By choosing the size $n$ to be some prime number that is a bit larger than the number of items expected in the table (there is usually a prime number close to any number we start with; actually, to ensure hash table operations have good performance, it is better to have the size of the hash table about twice as large as the number of items). Next assume the size of the domain of all data items $N=n^k$, a power of $n$ (if we need to overestimate the true number of data items, so be it). Then each data item can be considered as a $k$-tuple of integers modulo $n$, and $\mathcal{H}=\{h_a : a \in \{0, \dots, n-1\}^k\}$ is a universal family of hash functions.

# Exercises

+   1. In any base $b \ge 2$, the sum of any three single-digit numbers is at most two digits long.

+   2. That any binary integer is at most four times as long as the corresponding decimal integer. For large numbers, what is the ratio of these two lengths, approximately?

+   3. A $d$-tree is a rooted tree in which each node has $d$ children. Show that any $d$-tree with $n$ nodes has a depth of $\Omega(\log n/\log d)$. Can you give a formula for the minimum depth it could possibly have?

+   4. Show that

```
log(n!) = \Theta(n \log n).
```

(Hint: To show an upper bound, compare $n!$ with $n^n$. To show a lower bound, compare it with $(n/2)^{n/2}$.)