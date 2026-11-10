+   2. If there is a production \(A \to \alpha\beta\), then everything in \(\mathrm{FIRST}(\beta)\) except \(\epsilon\) is in \(\mathrm{FOLLOW}(B)\).
+   
+   3. If there is a production \(A \to \alpha B\), or a production \(A \to \alpha B\beta\), where \(\mathrm{FIRST}(\beta)\) contains \(\epsilon\), then everything in \(\mathrm{FOLLOW}(A)\) is in \(\mathrm{FOLLOW}(B)\).

**Example 4.30:** Consider again the non-left-recursive grammar (4.28). Then:

+   1. \(\mathrm{FIRST}(F)=\mathrm{FIRST}(T)=\mathrm{FIRST}(E)=\{(,\mathrm{id}\}\). To see why, note that the two productions for \(F\) have bodies that start with these two terminal symbols, \(\mathrm{id}\) and the left parenthesis. \(T\) has only one production, and its body starts with \(F\). Since \(F\) does not derive \(\epsilon\), \(\mathrm{FIRST}(T)\) must be the same as \(\mathrm{FIRST}(F)\). The same argument covers \(\mathrm{FIRST}(E)\).
+   
+   2. \(\mathrm{FIRST}(E')=\{+,\epsilon\}\). The reason is that one of the two productions for \(E'\) has a body that begins with terminal \(+\), and the other’s body is \(\epsilon\). Whenever a nonterminal derives \(\epsilon\), we place \(\epsilon\) in FIRST for that nonterminal.
+   
+   3. \(\mathrm{FIRST}(T')=\{*,\epsilon\}\). The reasoning is analogous to that for \(\mathrm{FIRST}(E')\).
+   
+   4. \(\mathrm{FOLLOW}(E)=\mathrm{FOLLOW}(E')=\{),\$\}\). Since \(E\) is the start symbol, \(\mathrm{FOLLOW}(E)\) must contain \(\$\). The production body \((E)\) explains why the right parenthesis is in \(\mathrm{FOLLOW}(E)\). For \(E'\), note that this nonterminal appears only at the ends of E-productions. Thus, \(\mathrm{FOLLOW}(E')\) must be the same as \(\mathrm{FOLLOW}(E)\).
+   
+   5. \(\mathrm{FOLLOW}(T)=\mathrm{FOLLOW}(T')=\{+,),\$\}\). Notice that \(T\) appears in bodies only followed by \(E'\). Thus, everything except \(\epsilon\) that is in \(\mathrm{FIRST}(E')\) must be in \(\mathrm{FOLLOW}(T)\); that explains the symbol \(+\). However, since \(\mathrm{FIRST}(E')\) contains \(\epsilon\), \(E' \Rightarrow^* \epsilon\), and \(E'\) is the entire string following \(T\) in the bodies of the E-productions, everything in \(\mathrm{FOLLOW}(E)\) must also be in \(\mathrm{FOLLOW}(T)\). That explains the symbols \(\$\) and the right parenthesis. As for \(T'\), since it appears only at the ends of the T-productions, it must be that \(\mathrm{FOLLOW}(T')=\mathrm{FOLLOW}(T)\).
+   
+   6. \(\mathrm{FOLLOW}(F)=\{+,*,),\$\}\). The reasoning is analogous to that for \(T\) in point (5).

□

# 4.4.3  LL(1) Grammars

Predictive parsers, that is, recursive-descent parsers needing no backtracking, can be constructed for a class of grammars called LL(1). The first “L” in LL(1) stands for scanning the input from left to right, the second “L” for producing a leftmost derivation, and the “1” for using one input symbol of lookahead at each step to make parsing action decisions.