# ## 8.2. THE TARGET LANGUAGE

**Exercise 8.2.3:** Generate code for the following three-address sequence assuming that p and q are in memory locations:

```
    y = *q
    q = q + 4
    *p = y
    p = p + 4
```

**Exercise 8.2.4:** Generate code for the following sequence assuming that x, y, and z are in memory locations:

```
    if x < y goto L1
    z = 0
    goto L2
    L1: z = 1
```

**Exercise 8.2.5:** Generate code for the following sequence assuming that n is in a memory location:

```
    s = 0
    i = 0
    L1: if i > n goto L2
    s = s + i
    i = i + 1
    goto L1
    L2:
```

**Exercise 8.2.6:** Determine the costs of the following instruction sequences:

+   a)  
+       LD R0, y
+       LD R1, z
+       ADD R0, R0, R1
+       ST x, R0

+   b)  
+       LD R0, i
+       MUL R0, R0, 8
+       LD R1, a(R0)
+       ST b, R1

+   c)  
+       LD R0, c
+       LD R1, i
+       MUL R1, R1, 8
+       ST a(R1), R0

+   d)  
+       LD R0, p
+       LD R1, 0(R0)
+       ST x, R1