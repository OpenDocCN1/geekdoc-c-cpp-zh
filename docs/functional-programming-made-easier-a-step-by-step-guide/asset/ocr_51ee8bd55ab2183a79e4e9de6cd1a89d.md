```
5! = 5 · (4 · 3 · 2 · 1)
```

where the parenthesized value is just $4!$:

```
5! = 5 · 4!
```

which leads us to an alternative definition for Factorial:

```
n! = n · (n − 1)!
```

But what happens when $n − 1$ is $0$?

How do we calculate $0!$?

We can figure this out by looking at $1!$:

```
1! = 1 · (1 − 1)!
   = 1 · 0!
```

From our original definition of Factorial (see Eq. #1), $1! = 1$. So, let’s substitute and reduce:

```
1! = 1 · 0!
1  = 1 · 0!
1  = 0!
```

Therefore, we can reasonably define $0!$ as:

```
0! = 1
```

So here’s our Mathematical Definition of Factorial:

```
0! = 1
For all n > 0, n! = n · (n − 1)!
```

In more Mathematical Symbology: