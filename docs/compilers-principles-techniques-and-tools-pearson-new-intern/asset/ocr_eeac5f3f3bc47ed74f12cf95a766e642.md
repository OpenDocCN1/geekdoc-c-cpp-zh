+   a) The same symbol can label edges from one state to several different states, and
+   
+   b) An edge may be labeled by ε, the empty string, instead of, or in addition to, symbols from the input alphabet.

**Example 3.14:** The transition graph for an NFA recognizing the language of regular expression (a|b)*abb is shown in Fig. 3.24. This abstract example, describing all strings of a’s and b’s ending in the particular string abb, will be used throughout this section. It is similar to regular expressions that describe languages of real interest, however. For instance, an expression describing all files whose name ends in .o is any*.o, where any stands for any printable character.

![](bbox=[0.321, 0.385, 0.682, 0.483])

Figure 3.24: A nondeterministic finite automaton

Following our convention for transition diagrams, the double circle around state 3 indicates that this state is accepting. Notice that the only ways to get from the start state 0 to the accepting state is to follow some path that stays in state 0 for a while, then goes to states 1, 2, and 3 by reading abb from the input. Thus, the only strings getting to the accepting state are those that end in abb.

# 3.6.2  Transition Tables

We can also represent an NFA by a *transition table*, whose rows correspond to states, and whose columns correspond to the input symbols and ε. The entry for a given state and input is the value of the transition function applied to those arguments. If the transition function has no information about that state-input pair, we put ∅ in the table for the pair.

**Example 3.15:** The transition table for the NFA of Fig. 3.24 is shown in Fig. 3.25.

The transition table has the advantage that we can easily find the transitions on a given state and input. Its disadvantage is that it takes a lot of space, when the input alphabet is large, yet most states do not have any moves on most of the input symbols.