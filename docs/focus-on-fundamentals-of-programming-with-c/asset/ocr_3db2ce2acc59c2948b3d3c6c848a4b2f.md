Also, the expression:

```
!(condition1 || condition2)
```

is logically equivalent to the expression:

```
(!condition1 && !condition2)
```

To summarize:

```
!(condition1 && condition2) = (!condition1 || !condition2)
!(condition1 || condition2) = (!condition1 && !condition2)
```

See if you can apply DeMorgan's Law to the following expression:

```
!(x > 5) || !(y > 7)
```