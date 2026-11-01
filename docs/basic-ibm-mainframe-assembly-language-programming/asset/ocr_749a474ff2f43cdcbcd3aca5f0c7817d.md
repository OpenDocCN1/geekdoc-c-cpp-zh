```
30          PR
31
32 RECUR
S    LR      R6,R5          * SAVE CRNT FACTOR
33    S       R5,=F'1'       * DECR FOR NEXT LEVEL
34    L       R15,=V(FACT)   * RECURSE
35    BASR    R14,R15
36
37    SR      R4,R4          * GET READY TO MULT
38    LR      R5,R6          * MULTIPLICAND
39    MR      R4,R1          * R1 RETRND FROM FCN
40    LR      R1,R5          * COPY ANS TO R1 FOR RETRN
41    PR                  * RESTORE REGS AND RETURN
42
43    LTORG
    END
```

Output:
5 FACTORIAL =          120

# Figure 70 System Stack Based Linkage

At the RECURS the program saves the incoming of R5 to R6, decrements R5 and calls itself. Upon return (lines 36 through 40), it multiplies the contents of R4/R5 by R1 (the value returned), copies the result to R1 and returns.