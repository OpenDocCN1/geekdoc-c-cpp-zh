# Chapter 0

# Algorithms 7

are choosing between two algorithms for a particular computational task. One takes $f_1(n)=n^2$ steps, while the other takes $f_2(n)=2n+20$ steps (Figure 0.2). Which is better? Well, this depends on the value of $n$. For $n \le 5$, $n^2$ is smaller; and thereafter, $2n+20$ is the clearer winner. In this case, $f_2$ scales much better than $n$, and therefore it is superior.

This superiority is captured by the big-O notation: $f_2 = O(f_1)$, because

```
$$\frac{f_2(n)}{f_1(n)} = \frac{2n+20}{n^2} \le 22$$
```

for all $n$; on the other hand, $f_1 \neq O(f_2)$, since the ratio $f_1(n)/f_2(n) = n^2/(2n+20)$ can be arbitrarily large, and no constant $c$ will make the definition work.

# Figure 0.2 Which running time is better?

![](bbox=[0.373, 0.363, 0.843, 0.656])

Another algorithm comes along, one that uses $f_3(n) = n+1$ steps. Is this better than $f_2$? Certainly, but only by a constant factor. The discrepancy between $2n+20$ and $n+1$ is tiny compared to the huge gap between $n^2$ and $2n+20$. In order to stay focused on the big picture, we treat functions as if they differ only by multiplicative constants.

Returning to definition of big-O, we see that $f_2 = O(f_3)$:

```
$$\frac{f_2(n)}{f_3(n)} = \frac{2n+20}{n+1} \le 20.$
```

and of course $f_3 = O(f_2)$, this time with $c = 1$.