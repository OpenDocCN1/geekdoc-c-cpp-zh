
## 6.7. BACKPATCHING

If \(S\) is the enclosing loop construct, then a break-statement is a jump to the first instruction after the code for \(S\). We can generate code for the break by (1) keeping track of the enclosing loop statement \(S\), (2) generating an unfilled jump for the break-statement, and (3) putting this unfilled jump on \(S.nextlist\), where \(nextlist\) is as discussed in Section 6.7.3.

In a two-pass front end that builds syntax trees, \(S.nextlist\) can be implemented as a field in the node for \(S\). We can keep track of \(S\) by using the symbol table to map a special identifier **break** to the node for the enclosing loop statement \(S\). This approach will also handle labeled break-statements in Java, since the symbol table can be used to map the label to the syntax-tree node for the labeled construct.

Alternatively, instead of using the symbol table to access the node for \(S\), we can put a pointer to \(S.nextlist\) in the symbol table. Now, when a break-statement is reached, we generate an unfilled jump, look up \(nextlist\) through the symbol table, and add the jump to the list, where it will be backpatched as discussed in Section 6.7.3.

Continue-statements can be handled in a manner analogous to the break-statement. The main difference between the two is that the target of the generated jump is different.

### 6.7.5 Exercises for Section 6.7

- **Exercise 6.7.1:** Using the translation of Fig. 6.43, translate each of the following expressions. Show the true and false lists for each subexpression. You may assume the address of the first instruction generated is 100.

  - a) `a==b && (c==d || e==f)`
  - b) `(a==b || c==d) || e==f`
  - c) `(a==b && c==d) && e==f`

- **Exercise 6.7.2:** In Fig. 6.47(a) is the outline of a program, and Fig. 6.47(b) sketches the structure of the generated three-address code, using the backpatching translation of Fig. 6.46. Here, \(i_1\) through \(i_8\) are the labels of the generated instructions that begin each of the “Code” sections. When we implement this translation, we maintain, for each boolean expression \(B\), two lists of places in the code for \(B\), which we denote by \(B.true\) and \(B.false\). The places on list \(B.true\) are those places where we eventually put the label of the statement to which control must flow whenever \(B\) is true; \(B.false\) similarly lists the places where we put the label that control flows to when \(B\) is found to be false. Also, we maintain for each statement \(S\), a list of places where we must put the label to which control flows when \(S\) is finished. Give the value (one of \(i_1\) through \(i_8\)) that eventually replaces each place on each of the following lists:

  - (a) \(B_3.false\)
  - (b) \(S_2.next\)
  - (c) \(B_4.false\)
  - (d) \(S_1.next\)
  - (e) \(B_2.true\)

```text
while (E1) {                     i1: Code for E1
    if (E2)                      i2: Code for E2
        while (E3)               i3: Code for E3
            S1;                  i4: Code for S1
        else {                   i5: Code for E4
            if (E4)              i6: Code for S2
                S2;              i7: Code for S3
            S3                   i8: ...
        }
}
```

Figure 6.47: Control-flow structure of program for Exercise 6.7.2

- **Exercise 6.7.3:** When performing the translation of Fig. 6.47 using the scheme of Fig. 6.46, we create lists \(S.next\) for each statement, starting with the assignment-statements \(S_1\), \(S_2\), and \(S_3\), and proceeding to progressively larger if-statements, if-else-statements, while-statements, and statement blocks. There are five constructed statements of this type in Fig. 6.47:

  - \(S_4\): **while** \((B_3)\ S_1\).
  - \(S_5\): **if** \((B_4)\ S_2\).
  - \(S_6\): The block consisting of \(S_5\) and \(S_3\).
  - \(S_7\): The statement **if** \((B_2)\ S_4\) **else** \(S_6\).
  - \(S_8\): The entire program.

For each of these constructed statements, there is a rule that allows us to construct \(S_i.next\) in terms of other \(S_j.next\) lists, and the lists \(B_k.true\) and \(B_k.false\) for the expressions in the program. Give the rules for

- (a) \(S_4.next\)
- (b) \(S_5.next\)
- (c) \(S_6.next\)
- (d) \(S_7.next\)
- (e) \(S_8.next\)

## 6.8 Switch-Statements

The “switch” or “case” statement is available in a variety of languages. Our switch-statement syntax is shown in Fig. 6.48. There is a selector expression \(E\), which is to be evaluated, followed by \(n\) constant values \(V_1, V_2, \cdots, V_n\) that the expression might take, perhaps including a *default* “value,” which always matches the expression if no other value does.

```text
switch ( E ) {
    case V1: S1
    case V2: S2
        ⋮
    case Vn-1: Sn-1
    default: Sn
}
```

Figure 6.48: Switch-statement syntax

### 6.8.1 Translation of Switch-Statements

The intended translation of a switch is code to:

- **1.** Evaluate the expression \(E\).
- **2.** Find the value \(V_j\) in the list of cases that is the same as the value of the expression. Recall that the default value matches the expression if none of the values explicitly mentioned in cases does.
- **3.** Execute the statement \(S_j\) associated with the value found.

Step (2) is an \(n\)-way branch, which can be implemented in one of several ways. If the number of cases is small, say 10 at most, then it is reasonable to use a sequence of conditional jumps, each of which tests for an individual value and transfers to the code for the corresponding statement.

A compact way to implement this sequence of conditional jumps is to create a table of pairs, each pair consisting of a value and a label for the corresponding statement’s code. The value of the expression itself, paired with the label for the default statement is placed at the end of the table at run time. A simple loop generated by the compiler compares the value of the expression with each value in the table, being assured that if no other match is found, the last (default) entry is sure to match.

If the number of values exceeds 10 or so, it is more efficient to construct a hash table for the values, with the labels of the various statements as entries. If no entry for the value possessed by the switch expression is found, a jump to the default statement is generated.

There is a common special case that can be implemented even more efficiently than by an \(n\)-way branch. If the values all lie in some small range, say \(min\) to \(max\), and the number of different values is a reasonable fraction of \(max - min\), then we can construct an array of \(max - min\) “buckets,” where bucket \(j - min\) contains the label of the statement with value \(j\); any bucket that would otherwise remain unfilled contains the default label.

To perform the switch, evaluate the expression to obtain the value \(j\); check that it is in the range \(min\) to \(max\) and transfer indirectly to the table entry at offset \(j - min\). For example, if the expression is of type character, a table of, say, 128 entries (depending on the character set) may be created and transferred through with no range testing.

### 6.8.2 Syntax-Directed Translation of Switch-Statements

The intermediate code in Fig. 6.49 is a convenient translation of the switch-statement in Fig. 6.48. The tests all appear at the end so that a simple code generator can recognize the multiway branch and generate efficient code for it, using the most appropriate implementation suggested at the beginning of this section.

```text
code to evaluate E into t
goto test
L1:  code for S1
     goto next
L2:  code for S2
     goto next
...
Ln-1: code for Sn-1
      goto next
Ln:  code for Sn
     goto next
test: if t = V1 goto L1
      if t = V2 goto L2
      ...
      if t = Vn-1 goto Ln-1
      goto Ln
next:
```

Figure 6.49: Translation of a switch-statement

The more straightforward sequence shown in Fig. 6.50 would require the compiler to do extensive analysis to find the most efficient implementation. Note that it is inconvenient in a one-pass compiler to place the branching statements at the beginning, because the compiler could not then emit code for each of the statements \(S_i\) as it saw them.

To translate into the form of Fig. 6.49, when we see the keyword **switch**, we generate two new labels **test** and **next**, and a new temporary \(t\). Then, as we parse the expression \(E\), we generate code to evaluate \(E\) into \(t\). After processing \(E\), we generate the jump **goto test**.

Then, as we see each **case** keyword, we create a new label \(L_i\) and enter it into the symbol table. We place in a queue, used only to store cases, a value-label pair consisting of the value \(V_i\) of the case constant and \(L_i\) (or a pointer to the symbol-table entry for \(L_i\)). We process each statement **case** \(V_i\): \(S_i\) by emitting the label \(L_i\) attached to the code for \(S_i\), followed by the jump **goto next**.
