so that the underlying grammar becomes non-left-recursive. Here, *a*, *b*, *c*, and *d* are actions, and 0 and 1 are terminals.

**Exercise 5.4.3:** The following SDT computes the value of a string of 0’s and 1’s interpreted as a positive, binary integer.

$$\begin{aligned}
B &\rightarrow B_1\ 0\ \{B.val = 2 \times B_1.val\}\\
  &\mid B_1\ 1\ \{B.val = 2 \times B_1.val + 1\}\\
  &\mid 1\ \{B.val = 1\}
\end{aligned}$$

Rewrite this SDT so the underlying grammar is not left recursive, and yet the same value of $B.val$ is computed for the entire input string.

**Exercise 5.4.4:** Write L-attributed SDD’s analogous to that of Example 5.19 for the following productions, each of which represents a familiar flow-of-control construct, as in the programming language C. You may need to generate a three-address statement to jump to a particular label $L$, in which case you should generate `goto L`.

+   a) $S \rightarrow \text{if }(C)\ S_1\ \text{else}\ S_2$
+   
+   b) $S \rightarrow \text{do }S_1\ \text{while }(C)$
+   
+   c) $S \rightarrow \{\, '\{'\ L\ '\}'\,\};\quad L \rightarrow L\ S\mid\epsilon$

Note that any statement in the list can have a jump from its middle to the next statement, so it is not sufficient simply to generate code for each statement in order.

**Exercise 5.4.5:** Convert each of your SDD’s from Exercise 5.4.4 to an SDT in the manner of Example 5.19.

**Exercise 5.4.6:** Modify the SDD of Fig. 5.25 to include a synthesized attribute $B.le$, the length of a box. The length of the concatenation of two boxes is the sum of the lengths of each. Then add your new rules to the proper positions in the SDT of Fig. 5.26.

**Exercise 5.4.7:** Modify the SDD of Fig. 5.25 to include superscripts denoted by operator subscripts between boxes. If box $B_2$ is a superscript of box $B_1$, then position the baseline of $B_2$ 0.6 times the point size of $B_1$ above the baseline of $B_1$. Add the new production and rules to the SDT of Fig. 5.26.

# ## 5.5 Implementing L-Attributed SDD’s

Since many translation applications can be addressed using L-attributed definitions, we shall consider their implementation in more detail in this section. The following methods do translation by traversing a parse tree: