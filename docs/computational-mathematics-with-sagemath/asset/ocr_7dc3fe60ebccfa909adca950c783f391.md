```
```text
[True, True, True, True, True, True, True, True, True, True,
 True, True, True, True]
```
```

Is the converse true?

**Exercise 58.** Try the two following commands and explain the considerable difference in the length of the calculations:

```
```text
sage: all( [ is_prime(mersenne(p)) for p in range(1000) if is_prime(p) ] )
False
sage: all( is_prime(mersenne(p)) for p in range(1000) if is_prime(p) )
False
```
```

We now try to find the smallest counter-example. In order to do this, we use the Sage function exists:

```
```text
sage: exists( (p for p in range(1000) if is_prime(p)),
.....:        lambda p: not is_prime(mersenne(p)) )
(True, 11)
```
```

Alternatively, we could construct an iterator on the counter-examples:

```
```text
sage: counter_examples = \
.....:     (p for p in range(1000)
.....:      if is_prime(p) and not is_prime(mersenne(p)))
sage: counter_examples.next()
11
sage: counter_examples.next()
23
```
```

**Exercise 59.** What do the following commands do?

```
```text
sage: cubes = [t**3 for t in range(-999,1000)]
sage: exists([(x,y) for x in cubes for y in cubes], lambda (x,y): x+y == 218)
sage: exists([(x,y) for x in cubes for y in cubes], lambda (x,y): x+y == 218)
```
```

Which of the last two are more economical in terms of time? In terms of memory? By how much?

**Exercise 60.** Try each of the following commands, and explain the results. Warning: it will be necessary to interrupt the execution of some of them.

```
```text
sage: x = var('x'); sum( x^len(s) for s in Subsets(8) )
```
```

```
```text
sage: sum( x^p.length() for p in Permutations(3) )
```
```

```
```text
sage: P = Permutations(5)
sage: all( p in P for p in P )
```
```

```
```text
sage: for p in GL(2, 2): print(p); print("------")
```
```

```
```text
sage: for p in Partitions(3): print(p)
```
```

```
```text
sage: for p in Partitions(): print(p)
```
```

```
```text
sage: for p in Primes(): print(p)
```
```