# ## 9.8. SYMBOLIC ANALYSIS

```
```
1) for (i = 1; i < n; i++) {
2)     a = input();
3)     for (j = 1; j < 10; j++) {
4)         a = a - 1;
5)         b = j + a;
6)         a = a + 1;
   }
}
```
```

(a) A loop where *a* fluctuates.

```
```
for (i = 1; i < n; i++) {
    a = input();
    t = a;
    for (j = 1; j < 10; j++) {
        a = t - 1;
        b = t - 1 + j;
        a = t;
    }
}
```
```

(b) A reference variable *t* makes *b* an induction variable.

Figure 9.64: The need to introduce reference variables

**Example 9.65:** Consider the simple example in Fig. 9.64(a). Let f_j be the transfer function summarizing the effect of executing j iterations of the inner loop. Even though the value of a may fluctuate during the execution of the loop, we see that b is an induction variable based on the value of a on entry of the loop; that is, f_j(m)(b) = m(a) - 1 + j. Because a is assigned an input value, the symbolic map upon entry to the inner loop maps a to NAA. We introduce a new reference variable t to save the value of a upon entry, and perform the substitutions as in Fig. 9.64(b). □

# ### 9.8.4 Exercises for Section 9.8

**Exercise 9.8.1:** For the flow graph of Fig. 9.10 (see the exercises for Section 9.1), give the transfer functions for

+   a) Block B_2.
+   
+   b) Block B_4.
+   
+   c) Block B_5.