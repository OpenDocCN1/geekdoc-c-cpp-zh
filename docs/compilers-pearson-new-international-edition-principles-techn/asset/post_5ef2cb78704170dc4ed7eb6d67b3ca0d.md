
## 5.5 Implementing L-Attributed SDD's

- **1.** Start with the SDT constructed as in Section 5.4.5, which places embedded actions before each nonterminal to compute its inherited attributes and an action at the end of the production to compute synthesized attributes.
- **2.** Introduce into the grammar a marker nonterminal in place of each embedded action. Each such place gets a distinct marker, and there is one production for any marker \(M\), namely \(M \to \epsilon\).
- **3.** Modify the action \(a\) if marker nonterminal \(M\) replaces it in some production \(A \to \alpha\{a\}\beta\), and associate with \(M \to \epsilon\) an action \(a'\) that
  - **(a)** Copies, as inherited attributes of \(M\), any attributes of \(A\) or symbols of \(\alpha\) that action \(a\) needs.
  - **(b)** Computes attributes in the same way as \(a\), but makes those attributes be synthesized attributes of \(M\).

This change appears illegal, since typically the action associated with production \(M \to \epsilon\) will have to access attributes belonging to grammar symbols that do not appear in this production. However, we shall implement the actions on the LR parsing stack, so the necessary attributes will always be available a known number of positions down the stack.

**Example 5.25:** Suppose that there is a production \(A \to BC\) in an LL grammar, and the inherited attribute \(B.i\) is computed from inherited attribute \(A.i\) by some formula \(B.i = f(A.i)\). That is, the fragment of an SDT we care about is

$$A \to \{B.i = f(A.i);\}\ B\ C$$

We introduce marker \(M\) with inherited attribute \(M.i\) and synthesized attribute \(M.s\). The former will be a copy of \(A.i\) and the latter will be \(B.i\). The SDT will be written

$$A \to M\ B\ C$$
$$M \to \{M.i = A.i;\ M.s = f(M.i);\}$$

Notice that the rule for \(M\) does not have \(A.i\) available to it, but in fact we shall arrange that every inherited attribute for a nonterminal such as \(A\) appears on the stack immediately below where the reduction to \(A\) will later take place. Thus, when we reduce to \(M\), we shall find \(A.i\) immediately below it, from where it may be read. Also, the value of \(M.s\), which is left on the stack along with \(M\), is really \(B.i\) and properly is found right below where the reduction to \(B\) will later occur. □

**Example 5.26:** Let us turn the SDT of Fig. 5.28 into an SDT that can operate with an LR parser of the revised grammar. We introduce a marker \(M\) before \(C\) and a marker \(N\) before \(S_1\), so the underlying grammar becomes

$$
\begin{aligned}
S &\to \text{while }(\,M\ C\,)\ N\ S_1\\
M &\to \epsilon\\
N &\to \epsilon
\end{aligned}
$$

### Why Markers Work

Markers are nonterminals that derive only ε and that appear only once among all the bodies of all productions. We shall not give a formal proof that, when a grammar is LL, marker nonterminals can be added at any position in the body, and the resulting grammar will still be LR. The intuition, however, is as follows. If a grammar is LL, then we can determine that a string w on the input is derived from nonterminal A, in a derivation that starts with production A → α, by seeing only the first symbol of w (or the following symbol if w = ε). Thus, if we parse w bottom-up, then the fact that a prefix of w must be reduced to α and then to S is known as soon as the beginning of w appears on the input. In particular, if we insert markers anywhere in α, the LR states will incorporate the fact that this marker has to be there, and will reduce ε to the marker at the appropriate point on the input.

Before we discuss the actions that are associated with markers \(M\) and \(N\), let us outline the “inductive hypothesis” about where attributes are stored.

- **1.** Below the entire body of the while-production — that is, below while on the stack — will be the inherited attribute \(S.next\). We may not know the nonterminal or parser state associated with this stack record, but we can be sure that it will have a field, in a fixed position of the record, that holds \(S.next\) before we begin to recognize what is derived from this \(S\).
- **2.** Inherited attributes \(C.true\) and \(C.false\) will be just below the stack record for \(C\). Since the grammar is presumed to be LL, the appearance of while on the input assures us that the while-production is the only one that can be recognized, so we can be sure that \(M\) will appear immediately below \(C\) on the stack, and \(M\)'s record will hold the inherited attributes of \(C\).
- **3.** Similarly, the inherited attribute \(S_1.next\) must appear immediately below \(S_1\) on the stack, so we may place that attribute in the record for \(N\).
- **4.** The synthesized attribute \(C.code\) will appear in the record for \(C\). As always when we have a long string as an attribute value, we expect that in practice a pointer to (an object representing) the string will appear in the record, while the string itself is outside the stack.
- **5.** Similarly, the synthesized attribute \(S_1.code\) will appear in the record for \(S_1\).

Let us follow the parsing process for a while-statement. Suppose that a record holding \(S.next\) appears on the top of the stack, and the next input is the terminal **while**. We shift this terminal onto the stack. It is then certain that the production being recognized is the while-production, so the LR parser can shift “(” and determine that its next step must be to reduce ε to \(M\). The stack at this time is shown in Fig. 5.36. We also show in that figure the action that is associated with the reduction to \(M\). We create values for \(L_1\) and \(L_2\), which live in fields of the \(M\)-record. Also in that record are fields for \(C.true\) and \(C.false\). These attributes must be in the second and third fields of the record, for consistency with other stack records that might appear below \(C\) in other contexts and also must provide these attributes for \(C\). The action completes by assigning values to \(C.true\) and \(C.false\), one from the \(L_2\) just generated, and the other by reaching down the stack to where we know \(S.next\) is found.

| ? | **while** | ( | \(M\) |
|---|---|---|---|
| \(S.next\) |  |  | \(C.true\) |
|  |  |  | \(C.false\) |
|  |  |  | \(L_1\) |
|  |  |  | \(L_2\) |

Top of stack: \(M\)

```
L1 = new();
L2 = new();
C.true = L2;
C.false = stack[top − 3].next;
```

Figure 5.36: LR parsing stack after reduction of \(\epsilon\) to \(M\)

We presume that the next inputs are properly reduced to \(C\). The synthesized attribute \(C.code\) is therefore placed in the record for \(C\). This change to the stack is shown in Fig. 5.37, which also incorporates the next several records that are later placed above \(C\) on the stack.

| ? | **while** | ( | \(M\) | \(C\) | ) | \(N\) | \(S_1\) |
|---|---|---|---|---|---|---|---|
| \(S.next\) |  |  | \(C.true\) | \(C.code\) |  | \(S_1.next\) | \(S_1.code\) |
|  |  |  | \(C.false\) |  |  |  |  |
|  |  |  | \(L_1\) |  |  |  |  |
|  |  |  | \(L_2\) |  |  |  |  |

Top of stack: \(S_1\)

Figure 5.37: Stack just before reduction of the while-production body to \(S\)

Continuing with the recognition of the while-statement, the parser should next find “)” on the input, which it pushes onto the stack in a record of its own. At that point, the parser, which knows it is working on a while-statement because the grammar is LL, will reduce ε to \(N\). The single piece of data associated with \(N\) is the inherited attribute \(S_1.next\). Note that this attribute needs to be in the record for \(N\) because that will be just below the record for \(S_1\). The code that is executed to compute the value of \(S_1.next\) is

```
S_1.next = stack[top - 3].L1;
```

This action reaches three records below \(N\), which is at the top of stack when the code is executed, and retrieves the value of \(L1\).

Next, the parser reduces some prefix of the remaining input to \(S\), which we have consistently referred to as \(S_1\) to distinguish it from the \(S\) at the head of the production. The value of \(S_1.code\) is computed and appears in the stack record for \(S_1\). This step takes us to the condition that is illustrated in Fig. 5.37.

At this point, the parser will reduce everything from while to \(S_1\) to \(S\). The code that is executed during this reduction is:

```
tempCode = label || stack[top − 4].L1 || stack[top − 3].code ||
  label || stack[top − 4].L2 || stack[top].code;
top = top − 5;
stack[top].code = tempCode;
```

That is, we construct the value of \(S.code\) in a variable \(tempCode\). That code is the usual, consisting of the two labels \(L1\) and \(L2\), the code for \(C\) and the code for \(S_1\). The stack is popped, so \(S\) appears where while was. The value of the code for \(S\) is placed in the code field of that record, where it can be interpreted as the synthesized attribute \(S.code\). Note that we do not show, in any of this discussion, the manipulation of LR states, which must also appear on the stack in the field that we have populated with grammar symbols.

### 5.5.5 Exercises for Section 5.5

- **Exercise 5.5.1:** Implement each of your SDD's of Exercise 5.4.4 as a recursive-descent parser in the style of Section 5.5.1.
- **Exercise 5.5.2:** Implement each of your SDD's of Exercise 5.4.4 as a recursive-descent parser in the style of Section 5.5.2.
- **Exercise 5.5.3:** Implement each of your SDD's of Exercise 5.4.4 with an LL parser in the style of Section 5.5.3, with code generated “on the fly.”
- **Exercise 5.5.4:** Implement each of your SDD's of Exercise 5.4.4 with an LL parser in the style of Section 5.5.3, but with code (or pointers to the code) stored on the stack.
- **Exercise 5.5.5:** Implement each of your SDD's of Exercise 5.4.4 with an LR parser in the style of Section 5.5.4.
- **Exercise 5.5.6:** Implement your SDD of Exercise 5.2.4 in the style of Section 5.5.1. Would an implementation in the style of Section 5.5.2 be any different?
