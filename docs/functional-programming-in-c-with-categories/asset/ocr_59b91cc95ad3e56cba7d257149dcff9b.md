As a simple example consider the predicate, that tests if two integers are equal:

```
bool areEqual(int a, int b = 0) => a == b;
```

we can create a range of specialized predicates by partial applying on any of the arguments:

```
bool isZero(int a) => areEqual(a, 0);
```

```
bool isOne(int a) => areEqual(a, 1);
```

![](bbox=[0.185, 0.27, 0.68, 0.32])

obviously, we can partially apply values to more than one argument (or even all of them )

![](bbox=[0.17, 0.39, 0.62, 0.46])

currying always leaves the function at hand in the same syntactical state of x=>y=>z=>... every time we use **compose** or **partially apply** a value, we consume an arrow (=>), but the result maintained the same syntactical form; y=>z=>... thus promoting uniformity. This is idempotent design in practice. The downside is that the order of arguments becomes now important, and simple reorder refactoring of arguments might have side effects.