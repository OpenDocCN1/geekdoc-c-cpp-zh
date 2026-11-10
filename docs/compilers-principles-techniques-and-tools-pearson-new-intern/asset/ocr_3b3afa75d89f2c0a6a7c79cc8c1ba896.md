+   2. If there is a production $A \to \alpha B\beta$, then everything in FIRST($\beta$) except $\epsilon$ is in FOLLOW($B$).
+   3. If there is a production $A \to \alpha B$, or a production $A \to \alpha B\beta$, where FIRST($\beta$) contains $\epsilon$, then everything in FOLLOW($A$) is in FOLLOW($B$).

**Example 4.30:** Consider again the non-left-recursive grammar (4.28). Then:

+   1. FIRST($F$) = FIRST($T$) = FIRST($E$) = { ( , id}. To see why, note that the two productions for $F$ have bodies that start with these two terminal symbols, id and the left parenthesis. $T$ has only one production, and its body starts with $F$. Since $F$ does not derive $\epsilon$, FIRST($T$) must be the same as FIRST($F$). The same argument covers FIRST($E$).
+   
+   2. FIRST($E'$) = {+, $\epsilon$}. The reason is that one of the two productions for $E'$ has a body that begins with terminal +, and the other’s body is $\epsilon$. Whenever a nonterminal derives $\epsilon$, we place $\epsilon$ in FIRST for that nonterminal.
+   
+   3. FIRST($T'$) = {*, $\epsilon$}. The reasoning is analogous to that for FIRST($E'$).
+   
+   4. FOLLOW($E$) = FOLLOW($E'$) = {), $\$}. Since $E$ is the start symbol, FOLLOW($E$) must contain $. The production body ($E$) explains why the right parenthesis is in FOLLOW($E$). For $E'$, note that this nonterminal appears only at the ends of bodies of $E$-productions. Thus, FOLLOW($E'$) must be the same as FOLLOW($E$).
+   
+   5. FOLLOW($T$) = FOLLOW($T'$) = {+, ), $}. Notice that $T$ appears in bodies only followed by $E'$. Thus, everything except $\epsilon$ that is in FIRST($E'$) must be in FOLLOW($T$); that explains the symbol +. However, since FIRST($E'$) contains $\epsilon$ (i.e., $E' \Rightarrow^* \epsilon$), and $E'$ is the entire string following $T$ in the bodies of the $E$-productions, everything in FOLLOW($E$) must also be in FOLLOW($T$). That explains the symbols $ and the right parenthesis. As for $T'$, since it appears only at the ends of the $T$-productions, it must be that FOLLOW($T'$) = FOLLOW($T$).
+   
+   6. FOLLOW($F$) = {+, *, ), $}. The reasoning is analogous to that for $T$ in point (5).

![](bbox=[0.22, 0.729, 0.232, 0.739])

# 4.4.3  LL(1) Grammars

Predictive parsers, that is, recursive-descent parsers needing no backtracking, can be constructed for a class of grammars called LL(1). The first “L” in LL(1) stands for scanning the input from left to right, the second “L” for producing a leftmost derivation, and the “1” for using one input symbol of lookahead at each step to make parsing action decisions.