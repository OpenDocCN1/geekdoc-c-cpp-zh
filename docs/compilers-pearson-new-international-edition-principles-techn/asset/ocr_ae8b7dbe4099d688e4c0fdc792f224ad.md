# 6.6. CONTROL FLOW

```
```text
ifFalse a < b goto L₁
ifFalse c < d goto L₁
t = true
goto L₂
L₁:  t = false
L₂:  x = t
```
```

Figure 6.42: Translating a boolean assignment by computing the value of a temporary

! b) A for-loop for (S₁; B; S₂) S₃.

**Exercise 6.6.2:** Modern machines try to execute many instructions at the same time, including branching instructions. Thus, there is a severe cost if the machine speculatively follows one branch, when control actually goes another way (all the speculative work is thrown away). It is therefore desirable to minimize the number of branches. Notice that the implementation of a while-loop in Fig. 6.35(c) has two branches per iteration: one to enter the body from the condition B and the other to jump back to the code for B. As a result, it is usually preferable to implement the while (B) S as if it were if (B) { repeat S until !(B) }. Show what the code layout looks like for this translation, and revise the rule for while-loops in Fig. 6.36.

! **Exercise 6.6.3:** Suppose that there were an “exclusive-or” operator (true if and only if exactly one of its two arguments is true) in C. Write the rule for this operator in the style of Fig. 6.37.

**Exercise 6.6.4:** Translate the following expressions using the goto-avoiding translation scheme of Section 6.6.5:

+   a) `if (a==b && c==d || e==f) x == 1;`
+   
+   b) `if (a==b || c==d || e==f) x == 1;`
+   
+   c) `if (a==b && c==d && e==f) x == 1;`

**Exercise 6.6.5:** Give a translation scheme based on the syntax-directed definition in Figs. 6.36 and 6.37.

**Exercise 6.6.6:** Adapt the semantic rules in Figs. 6.36 and 6.37 to allow control to fall through, using rules like these ones in Figs. 6.39 and 6.40.

! **Exercise 6.6.7:** The semantic rules for statements in Exercise 6.6.6 generate unnecessary labels. Modify the rules for statements in Fig. 6.36 to create labels as needed, using a special label deferred to start at a label has not yet been created. Your rules must generate code similar to that in Example 6.21.