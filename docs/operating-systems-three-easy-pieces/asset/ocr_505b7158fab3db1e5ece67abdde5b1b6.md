# HARD DISK DRIVES

# 465

# ASIDE: COMPUTING THE “AVERAGE” SEEK

In many books and papers, you will see average disk-seek time cited as being roughly one-third of the full seek time. Where does this come from?

It turns out from a simple calculation based on average seek distance, not time. Imagine the disk as a set of tracks, 0 to $N$. The seek distance between any two tracks $x$ and $y$ is thus computed as the absolute value of the difference between them: $|x - y|$.

To compute the average seek distance, all you need to do is first add all possible seek distances:

```
$$\sum_{x=0}^{N}\sum_{y=0}^{N}|x - y|$\ (37.4)
```

Now, divide this by the number of different seeks: $N^2$. To compute the sum, we'll just use the integral:

```
$$\int_{x=0}^{N}\int_{y=0}^{N}|x - y|dydx$\ (37.5)
```

To compute the inner integral, let's break out the absolute value:

```
$$\int_{y=0}^{x}(x - y)dy + \int_{y=x}^{N}(y - x)dy$\ (37.6)
```

Solving this leads to $(xy - \frac{1}{2}y^2)|_{y=0}^{x} + (\frac{1}{2}y^2 - xy)|_{x}^{N}$ which can be simplified to $(x^2 - Nx + \frac{1}{2}N^2)$. Now we have to compute the outer integral:

```
$$\int_{x=0}^{N}(x^2 - Nx + \frac{1}{2}N^2)dx$\ (37.7)
```

which results in:

```
$$\frac{1}{3}x^3 - \frac{N}{2}x^2 + \frac{N^2}{2}x|_{0}^{N} = \frac{N^3}{3}$\ (37.8)
```

Remember that we still have to divide by the total number of seeks $(N^2)$ to compute the average seek distance: $(\frac{N^3}{3})/(N^2) = \frac{1}{3}N$. Thus the average seek distance on a disk, over all possible seeks, is one-third of the full seek. And now when you hear that an average seek is one-third of a full seek, you'll know where it came from.

© 2008–19

# THREE EASY PIECES