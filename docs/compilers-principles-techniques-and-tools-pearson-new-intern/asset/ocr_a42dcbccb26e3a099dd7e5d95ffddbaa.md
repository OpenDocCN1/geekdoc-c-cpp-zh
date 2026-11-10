![](bbox=[0.359, 0.177, 0.644, 0.39])

Figure 3.50: An NFA constructed from a Lex program

+   - **a** — { action $A_1$ for pattern $p_1$ }
+   - **abb** — { action $A_2$ for pattern $p_2$ }
+   - **a*b+** — { action $A_3$ for pattern $p_3$ }

Note that these three patterns present some conflicts of the type discussed in Section 3.5.3. In particular, string $abb$ matches both the second and third patterns, but we shall consider it a lexeme for pattern $p_2$, since that pattern is listed first in the above Lex program. Then, input strings such as $aabbb\ldots$ have many prefixes that match the third pattern. The Lex rule is to take the longest, so we continue reading b’s, until another a is met, whereupon we report the lexeme to be the initial a’s followed by as many b’s as there are.

Figure 3.51 shows three NFA’s that recognize the three patterns. The third is a simplification of what would come out of Algorithm 3.23. Then, Fig. 3.52 shows these three NFA’s combined into a single NFA by the addition of start state 0 and three ε-transitions. □

# 3.8.2 Pattern Matching Based on NFA’s

If the lexical analyzer simulates an NFA such as that of Fig. 3.52, then it must read input beginning at the point on its input which we have referred to as lexemeBegin. As it moves the pointer called forward ahead in the input, it calculates the set of states it is in at each point, following Algorithm 3.22.

Eventually, the NFA simulation reaches a point on the input where there are no next states. At that point, there is no hope that any longer prefix of the input would ever get the NFA to an accepting state; rather, the set of states will always be empty. Thus, we are ready to decide on the longest prefix that is a lexeme matching some pattern.