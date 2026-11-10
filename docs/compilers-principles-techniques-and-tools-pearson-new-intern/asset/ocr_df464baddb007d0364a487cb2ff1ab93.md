conditional and unconditional jumps to one of two labels: \(B.true\) if \(B\) is true, and \(B.false\) if \(B\) is false.

| Production | Semantic Rules |
|---|---|
| \(B \to B_1 \parallel B_2\) | \(B_1.true = B.true\)<br>\(B_1.false = newlabel()\)<br>\(B_2.true = B.true\)<br>\(B_2.false = B.false\)<br>\(B.code = B_1.code \parallel label(B_1.false) \parallel B_2.code\) |
| \(B \to B_1 \&\& B_2\) | \(B_1.true = newlabel()\)<br>\(B_1.false = B.false\)<br>\(B_2.true = B.true\)<br>\(B_2.false = B.false\)<br>\(B.code = B_1.code \parallel label(B_1.true) \parallel B_2.code\) |
| \(B \to !B_1\) | \(B_1.true = B.false\)<br>\(B_1.false = B.true\)<br>\(B.code = B_1.code\) |
| \(B \to E_1\ \mathrm{rel}\ E_2\) | \(B.code = E_1.code \parallel E_2.code\)<br>\(\quad\parallel gen('if'\ E_1.addr\ rel.op\ E_2.addr\ 'goto'\ B.true)\)<br>\(\quad\parallel gen('goto'\ B.false)\) |
| \(B \to true\) | \(B.code = gen('goto'\ B.true)\) |
| \(B \to false\) | \(B.code = gen('goto'\ B.false)\) |

Figure 6.37: Generating three-address code for booleans

The fourth production in Fig. 6.37, \(B \to E_1\ rel\ E_2\), is translated directly into a comparison three-address instruction with jumps to the appropriate places. For instance, \(B\) of the form \(a < b\) translates into:

```
if a < b goto B.true
goto B.false
```

The remaining productions for \(B\) are translated as follows:

+   1. Suppose \(B\) is of the form \(B_1 \parallel B_2\). If \(B_1\) is true, then we immediately know that \(B\) itself is true, so \(B_1.true\) is the same as \(B.true\). If \(B_1\) is false, then \(B_2\) must be evaluated, so we make \(B_1.false\) be the label of the first instruction in the code for \(B_2\). The true and false exits of \(B_2\) are the same as the true and false exits of \(B\), respectively.