+   - Iterates over all prime numbers whose associated Mersenne number is not prime.

**Exercise 61** page 349. Let us define recursively our iterator:

```
```sage
sage: def C(n):
....:     if n == 1:
....:         yield BinaryTree()
....:     elif n > 1:
....:         for k in range(1,n):
....:             for t1 in C(k):
....:                 for t2 in C(n-k):
....:                     yield BinaryTree([t1,t2])
```
```

Here are the small trees:

```
```sage
sage: list(C(1))
[.]
sage: list(C(2))
[[., .]]
sage: list(C(3))
[[., [., .]],
 [[., .], .]]
sage: list(C(4))
[[., [., [., .]]],
 [., [[., .], .]],
 [[., .], [., .]],
 [[., [., .]], .],
 [[[., .], .], .]]
```
```

We indeed find Catalan's sequence:

```
```sage
sage: [len(list(C(n))) for n in range(9)]
[0, 1, 1, 2, 5, 14, 42, 132, 429]
```
```

# ## A.16 Graph Theory

**Exercise 62** page 365. (*Circulant graphs*) Two loops should suffice!

```
```sage
sage: def circulant(n,d):
....:     g = Graph(n)
....:     for u in range(n):
....:         for c in range(d):
....:             g.add_edge(u,(u+c)%n)
....:     return g
```
```

**Exercise 63** page 367. (*Kneser Graphs*) The simplest method uses Sage's Subsets object. We then enumerate all pairs of vertices to find the adjacencies, albeit with many redundant calculations.