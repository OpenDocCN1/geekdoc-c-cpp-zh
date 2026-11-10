a1a2 · · · an, the DFA is in that state which corresponds to the set of states that the NFA can reach, from its start state, following paths labeled a1a2 · · · an.

It is possible that the number of DFA states is exponential in the number of NFA states, which could lead to difficulties when we try to implement this DFA. However, part of the power of the automaton-based approach to lexical analysis is that for real languages, the NFA and DFA have approximately the same number of states, and the exponential behavior is not seen.

# **Algorithm 3.20:** The subset construction of a DFA from an NFA.

**INPUT:** An NFA *N*.

**OUTPUT:** A DFA *D* accepting the same language as *N*.

**METHOD:** Our algorithm constructs a transition table *Dtran* for *D*. Each state of *D* is a set of NFA states, and we construct *Dtran* so *D* will simulate "in parallel" all possible moves *N* can make on a given input string. Our first problem is to deal with ε-transitions of *N* properly. In Fig. 3.31 we see the definitions of several functions that describe basic computations on the states of *N* that are needed in the algorithm. Note that *s* is a single state of *N*, while *T* is a set of states of *N*.

| OPERATION | DESCRIPTION |
| --- | --- |
| ε-closure(s) | Set of NFA states reachable from NFA state s on ε-transitions alone. |
| ε-closure(T) | Set of NFA states reachable from some NFA state s in set T on ε-transitions alone; = ∪_{s in T} ε-closure(s). |
| move(T, a) | Set of NFA states to which there is a transition on input symbol a from some state s in T. |

Figure 3.31: Operations on NFA states

We must explore those sets of states that *N* can be in after seeing some input string. As a basis, before reading the first input symbol, *N* can be in any of the states of ε-closure(s0), where s0 is its start state. For the induction, suppose that *N* can be in set of states *T* after reading input string *x*. If it next reads input *a*, then *N* can immediately go to any of the states in move(*T*, *a*). However, after reading *a*, it may also make several ε-transitions; thus *N* could be in any state of ε-closure(move(*T*, *a*)) after reading input *xa*. Following these ideas, the construction of the set of *D*'s states, *Dstates*, and its transition function *Dtran*, is shown in Fig. 3.32.

The start state of *D* is ε-closure(s0), and the accepting states of *D* are all those sets of *N*'s states that include at least one accepting state of *N*. To complete our description of the subset construction, we need only to show how