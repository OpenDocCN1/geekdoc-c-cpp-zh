# 6.7. BACKPATCHING

+   2. *merge*(*p*₁,*p*₂) concatenates the lists pointed to by *p*₁ and *p*₂, and returns a pointer to the concatenated list.
+   3. *backpatch*(*p*,*i*) inserts *i* as the target label for each of the instructions on the list pointed to by *p*.

# 6.7.2 Backpatching for Boolean Expressions

We now construct a translation scheme suitable for generating code for boolean expressions during bottom-up parsing. A marker nonterminal *M* in the grammar causes a semantic action to pick up, at appropriate times, the index of the next instruction to be generated. The grammar is as follows:

```
```text
B → B₁ || M B₂ | B₁ && M B₂ | ! B₁ | ( B₁ ) | E₁ rel E₂ | true | false
M → ε
```
```

The translation scheme is in Fig. 6.43.

```
```text
1) B → B₁ || M B₂ { backpatch(B₁.falselist, M.instr);
                    B.truelist = merge(B₁.truelist, B₂.truelist);
                    B.falselist = B₂.falselist; }
2) B → B₁ && M B₂ { backpatch(B₁.truelist, M.instr);
                    B.truelist = B₂.truelist;
                    B.falselist = merge(B₁.falselist, B₂.falselist); }
3) B → ! B₁ { B.truelist = B₁.falselist;
              B.falselist = B₁.truelist; }
4) B → ( B₁ ) { B.truelist = B₁.truelist;
                B.falselist = B₁.falselist; }
5) B → E₁ rel E₂ { B.truelist = makelist(nextinstr);
                   B.falselist = makelist(nextinstr + 1);
                   gen('if' E₁.addr rel.op E₂.addr 'goto _');
                   gen('goto _'); }
6) B → true { B.truelist = makelist(nextinstr);
              gen('goto _'); }
7) B → false { B.falselist = makelist(nextinstr);
               gen('goto _'); }
8) M → ε { M.instr = nextinstr; }
```
```

Figure 6.43: Translation scheme for boolean expressions

Consider semantic action (1) for the production B → B₁ || M B₂. If B₁ is true, then B is also true, so the jumps on B₁.truelist become part of B.truelist. If B₁ is false, however, we must next test B₂, so the target for the jumps