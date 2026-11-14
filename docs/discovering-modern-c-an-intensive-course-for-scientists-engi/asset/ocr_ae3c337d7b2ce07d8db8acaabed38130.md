For now, we will consider it as a concise form to iterate over all entries of an array or other containers:

```
int primes[] = {2, 3, 5, 7, 11, 13, 17, 19};
for (int i : primes)
    std::cout << i << " ";
```

This will print out the primes from the array separated by spaces.

# 1.4.4.4 Loop Control

There are two statements to deviate from the regular loop evaluation:

+   - break and
+   - continue.

A break terminates the loop entirely, and continue ends only the current iteration and continues the loop with the next iteration, for instance:

```
for (....; ....; ....) {
    ...
    if (dx == 0.0) continue;
    x+= dx;
    ...
    if (r < eps) break;
    ...
}
```

In the example above we assumed that the remainder of the iteration is not needed when dx == 0.0. In some iterative computations it might be clear in the middle of an iteration (here when r < eps) that work is already done.

# 1.4.5 goto

All branches and loops are internally realized by jumps. C++ provides explicit jumps called goto. However:

> **Advice**
> Do not use goto! Never! Ever!

The applicability of goto is more restrictive in C++ than in C (e.g., we cannot jump over initializations); it still has the power to ruin the structure of our program.