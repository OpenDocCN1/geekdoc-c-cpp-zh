simply place that state in the record for the new top of stack.

# 5.4.3 SDT’s With Actions Inside Productions

An action may be placed at any position within the body of a production. It is performed immediately after all symbols to its left are processed. Thus, if we have a production \(B \to X\ \{a\}\ Y\), the action \(a\) is done after we have recognized \(X\) (if \(X\) is a terminal) or all the terminals derived from \(X\) (if \(X\) is a nonterminal). More precisely,

+   - If the parse is bottom-up, then we perform action \(a\) as soon as this occurrence of \(X\) appears on the top of the parsing stack.
+   - If the parse is top-down, we perform \(a\) just before we attempt to expand this occurrence of \(Y\) (if \(Y\) a nonterminal) or check for \(Y\) on the input (if \(Y\) is a terminal).

SDT’s that can be implemented during parsing include postfix SDT’s and a class of SDT’s considered in Section 5.5 that implements L-attributed definitions. Not all SDT’s can be implemented during parsing, as we shall see in the next example.

**Example 5.16:** As an extreme example of a problematic SDT, suppose that we turn our desk-calculator running example into an SDT that prints the prefix form of an expression, rather than evaluating the expression. The productions and actions are shown in Fig. 5.21.

```
1)  L → E n
2)  E → { print('+'); } E₁ + T
3)  E → T
4)  T → { print('*'); } T₁ * F
5)  T → F
6)  F → ( E )
7)  F → digit { print(digit.lexval); }
```

Figure 5.21: Problematic SDT for infix-to-prefix translation during parsing

Unfortunately, it is impossible to implement this SDT during either top-down or bottom-up parsing, because the parser would have to perform critical actions, like printing instances of \(*\) or \(+\), long before it knows whether these symbols will appear in its input.

Using marker nonterminals \(M_2\) and \(M_4\) for the actions in productions 2 and 4, respectively, on input that is a digit, a shift-reduce parser (see Section 4.5.3) has conflicts between reducing by \(M_2 \to \epsilon\), reducing by \(M_4 \to \epsilon\), and shifting the digit.