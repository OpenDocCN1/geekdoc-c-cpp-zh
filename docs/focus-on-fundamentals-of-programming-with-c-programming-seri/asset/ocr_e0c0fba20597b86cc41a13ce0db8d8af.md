For example, we can determine the internal representation of -6 by taking the two's complement of 6:

```
00000110   = 6
11111001   flip all bits
+      1   add 1
11111010   = -6
```

According to this scheme, -6 is represented as:

```
11111010
```

We can test this by adding 6 and -6:

```
00000110   = 6
11111010   = -6
00000000   = 0
```

Note that we are only doing 8-bit arithmetic, so any final carry can be ignored. As another example, let's determine how -25 is represented:

```
00011001   = 25
11100110   flip all bits
+      1   add 1
11100111   = -25
```