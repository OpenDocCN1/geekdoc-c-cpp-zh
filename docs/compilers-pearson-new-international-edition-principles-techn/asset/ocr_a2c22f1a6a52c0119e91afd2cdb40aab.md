# 6.7. BACKPATCHING

+   2. `merge(p₁, p₂)` concatenates the lists pointed to by `p₁` and `p₂`, and returns a pointer to the concatenated list.
+   
+   3. `backpatch(p, i)` inserts `i` as the target label for each of the instructions on the list pointed to by `p`.

# 6.7.2  Backpatching for Boolean Expressions

We now construct a translation scheme suitable for generating code for boolean expressions during bottom-up parsing. A marker nonterminal M in the grammar causes a semantic action to pick up, at appropriate times, the index of the next instruction to be generated. The grammar is as follows:

$$B \to B_1 \parallel M\ B_2 \mid B_1 \ \&\&\ M\ B_2 \mid !\ B_1 \mid (B_1) \mid E_1\ \mathrm{rel}\ E_2 \mid \mathrm{true} \mid \mathrm{false}$$
$$M \to \epsilon$$

The translation scheme is in Fig. 6.43.

| # | Production and semantic actions |
|---|---|
| 1) | $B \to B_1 \parallel M\ B_2$  `{ backpatch(B₁.falselist, M.instr);`<br>`B.truelist = merge(B₁.truelist, B₂.truelist);`<br>`B.falselist = B₂.falselist; }` |
| 2) | $B \to B_1 \ \&\&\ M\ B_2$  `{ backpatch(M.instr, B₁.truelist);`<br>`B.truelist = B₂.truelist;`<br>`B.falselist = merge(B₁.falselist, B₂.falselist); }` |
| 3) | $B \to !\ B_1$  `{ B.truelist = B₁.falselist;`<br>`B.falselist = B₁.truelist; }` |
| 4) | $B \to (B_1)$  `{ B.truelist = B₁.truelist;`<br>`B.falselist = B₁.falselist; }` |
| 5) | $B \to E_1\ \mathrm{rel}\ E_2$  `{ B.truelist = makelist(nextinstr);`<br>`B.falselist = makelist(nextinstr + 1);`<br>`gen('if E₁.addr rel.op E₂.addr goto _');`<br>`gen('goto _'); }` |
| 6) | $B \to \mathrm{true}$  `{ B.truelist = makelist(nextinstr);`<br>`gen('goto _'); }` |
| 7) | $B \to \mathrm{false}$  `{ B.falselist = makelist(nextinstr);`<br>`gen('goto _'); }` |
| 8) | $M \to \epsilon$  `{ M.instr = nextinstr; }` |

Figure 6.43: Translation scheme for boolean expressions

Consider semantic action (1) for the production $B \to B_1 \parallel M\ B_2$. If $B_1$ is true, then $B$ is also true, so the jumps on $B_1.truelist$ become part of $B.truelist$. If $B_1$ is false, however, we must next test $B_2$, so the target for the jumps