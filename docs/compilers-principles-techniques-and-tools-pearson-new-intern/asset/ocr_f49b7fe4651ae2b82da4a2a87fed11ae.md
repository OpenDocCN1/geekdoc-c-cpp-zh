![](bbox=[0.332, 0.175, 0.685, 0.292])

Figure 3.30: NFA for Exercise 3.6.4

**Exercise 3.6.4:** Repeat Exercise 3.6.3 for the NFA of Fig. 3.30.

**Exercise 3.6.5:** Give the transition tables for the NFA of:

+   a) Exercise 3.6.3.
+   
+   b) Exercise 3.6.4.
+   
+   c) Figure 3.26.

# 3.7 From Regular Expressions to Automata

The regular expression is the notation of choice for describing lexical analyzers and other pattern-processing software, as was reflected in Section 3.5. However, implementation of that software requires the simulation of a DFA, as in Algorithm 3.18, or perhaps simulation of an NFA. Because an NFA often has a choice of move on an input symbol (as Fig. 3.24 does on input a from state 0) or on ε (as Fig. 3.26 does from state 0), or even a choice of making a transition on ε or on a real input symbol, its simulation is less straightforward than for a DFA. Thus often it is important to convert an NFA to a DFA that accepts the same language.

In this section we shall first show how to convert NFA’s to DFA’s. Then, we use this technique, known as “the subset construction,” to give a useful algorithm for simulating NFA’s directly, in situations (other than lexical analysis) where the NFA-to-DFA conversion takes more time than the direct simulation. Next, we show how to convert regular expressions to NFA’s, from which a DFA can be constructed if desired. We conclude with a discussion of the time-space tradeoffs inherent in the various methods for implementing regular expressions, and see how to choose the appropriate method for your application.

# 3.7.1 Conversion of an NFA to a DFA

The general idea behind the subset construction is that each state of the constructed DFA corresponds to a set of NFA states. After reading input