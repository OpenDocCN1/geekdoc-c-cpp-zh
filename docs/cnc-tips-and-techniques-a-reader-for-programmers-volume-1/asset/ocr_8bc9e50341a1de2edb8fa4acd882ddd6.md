settings is often the best way — sometimes the only way — to solve any threading problem.

Although the general description of individual cycle entries is available from numerous sources, the details are often obscure and contain no useful details for practical applications.

Understanding the basic background of possible threading problems is essential to their solution. In a separate essay, we will look at the G76 cycle structure from the perspective of the CNC operator and evaluate individual cycle parameters in more detail. Look for continuation of this discussion in the essay *Threading with G76 Cycle — Details*, where the many format details of the G76 threading cycle will be discussed.

![](bbox=[0.084, 0.459, 0.174, 0.503])

# Threading with G76 Cycle — Details

*July 2009*

The essay *Threading with G76 Cycle — Basics* covered the basics of threading on CNC lathes, using the G76 multiple repetitive cycle. When a program containing G76 cycle reaches the CNC operator, all threading data are contained in two blocks. Older controls use only one block, but the two-block format is far more popular and will be described here in more detail.

# Two-Block format

As an example, a standard external thread of 12 threads per inch (12 TPI) will be made on a three-inch diameter. Its length will be 2.5 inches. The programmer will provide the following data:

```
```text
G76 P010060 Q0040 R0.002
G76 X2.8978 Z-2.5 R0 P0511 Q0120 F0.083333
```
```

In the first block, the *P010060* is a six-digit entry in three