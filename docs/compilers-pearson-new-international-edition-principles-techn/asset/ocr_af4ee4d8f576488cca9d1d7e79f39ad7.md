```
```text
(1)   i = m-1          (16)  t7 = 4*i
(2)   j = n            (17)  t8 = 4*j
(3)   t1 = 4*n         (18)  t9 = a[t8]
(4)   v = a[t1]        (19)  a[t7] = t9
(5)   i = i+1          (20)  t10 = 4*j
(6)   t2 = 4*i         (21)  a[t10] = x
(7)   t3 = a[t2]       (22)  goto (5)
(8)   if t3 < v goto (5) (23) t11 = 4*i
(9)   j = j-1          (24)  x = a[t11]
(10)  t4 = 4*j         (25)  t12 = 4*i
(11)  t5 = a[t4]       (26)  t13 = 4*n
(12)  if t5>v goto (9) (27)  t14 = a[t13]
(13)  if i>j goto (23) (28)  a[t12] = t14
(14)  t6 = 4*i         (29)  t15 = 4*n
(15)  x = a[t6]        (30)  a[t15] = x
```
```

Figure 9.2: Three-address code for fragment in Fig. 9.1

```
```text
t6 = 4*i
x = a[t6]
```
```

as shown in steps (14) and (15) of Fig. 9.2. Similarly, a[j] = x becomes

```
```text
t10 = 4*j
a[t10] = x
```
```

in steps (20) and (21). Notice that every array access in the original program translates into a pair of steps, consisting of a multiplication and an array-subscripting operation. As a result, this short program fragment translates into a rather long sequence of three-address operations.

Figure 9.3 is the flow graph for the program in Fig. 9.2. Block B₁ is the entry node. All conditional and unconditional jumps to statements in Fig. 9.2 have been replaced in Fig. 9.3 by jumps to the block of which the statements are leaders, as in Section 8.4. In Fig. 9.3, there are three loops. Blocks B₂ and B₃ are loops by themselves. Blocks B₂, B₃, B₄, and B₅ together form a loop, with B₂ the only entry point.

# 9.1.3 Semantics-Preserving Transformations

There are a number of ways in which a compiler can improve a program without changing the function it computes. Common-subexpression elimination, copy propagation, dead-code elimination, and constant folding are common examples of such function-preserving (or semantics-preserving) transformations; we shall consider each in turn.