# 3.7. FROM REGULAR EXPRESSIONS TO AUTOMATA

![](bbox=[0.215, 0.174, 0.801, 0.339])

Figure 3.34: NFA N for `(a|b)*abb`

$Dtran[A,d] = \varepsilon\text{-closure}(\mathrm{move}(A,d)) = \varepsilon\text{-closure}(\{3,8\}) = \{1,2,3,4,6,7,8\}$

Let us call this set $B$, so $Dtran[A,a] = B$.

Now, we must compute $Dtran[A,b]$. Among the states in $A$, only 4 has a transition on $b$, and it goes to 5. Thus.

$Dtran[A,b] = \varepsilon\text{-closure}(\{5\}) = \{1,2,4,5,6,7\}$

Let us call the above set $C$, so $Dtran[A,b] = C$.

| NFA STATE | DFA STATE | a | b |
|---|---|---|---|
| {0, 1, 2, 4, 7} | A | B | C |
| {1, 2, 3, 4, 6, 7, 8} | B | D | D |
| {1, 2, 4, 5, 6, 7} | C | B | C |
| {1, 2, 4, 5, 6, 7, 9} | D | B | E |
| {1, 2, 4, 5, 6, 7, 10} | E | B | C |

Figure 3.35: Transition table $Dtran$ for DFA $D$

If we continue this process with the unmarked sets $B$ and $C$, we eventually reach a point where all the states of the DFA are marked. This conclusion is guaranteed, since there are “only” $2^{11}$ different subsets of a set of eleven NFA states. The five different DFA states we actually construct, their corresponding sets of NFA states, and the transition table for the DFA $D$ are shown in Fig. 3.35, and the transition graph for $D$ is in Fig. 3.36. State $A$ is the start state, and state $E$, which contains state 10 of the NFA, is the only accepting state.

Note that $D$ has one more state than the DFA of Fig. 3.28 for the same language. States $A$ and $C$ have the same move function, and so can be merged. We will discuss the matter of minimizing the number of states of a DFA in Section 3.9.6.