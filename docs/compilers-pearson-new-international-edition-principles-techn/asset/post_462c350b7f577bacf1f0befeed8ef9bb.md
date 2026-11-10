
## 3.7. FROM REGULAR EXPRESSIONS TO AUTOMATA

a₁a₂···aₙ, the DFA is in that state which corresponds to the set of states that the NFA can reach, from its start state, following paths labeled a₁a₂···aₙ.

It is possible that the number of DFA states is exponential in the number of NFA states, which could lead to difficulties when we try to implement this DFA. However, part of the power of the automaton-based approach to lexical analysis is that for real languages, the NFA and DFA have approximately the same number of states, and the exponential behavior is not seen.

**Algorithm 3.20:** The *subset construction* of a DFA from an NFA.

**INPUT:** An NFA *N*.

**OUTPUT:** A DFA *D* accepting the same language as *N*.

**METHOD:** Our algorithm constructs a transition table D<sub>tran</sub> for D. Each state of D is a set of NFA states, and we construct D<sub>tran</sub> so D will simulate “in parallel” all possible moves N can make on a given input string. Our first problem is to deal with ε-transitions of N properly. In Fig. 3.31 we see the definitions of several functions that describe basic computations on the states of N that are needed in the algorithm. Note that s is a single state of N, while T is a set of states of N.

| OPERATION | DESCRIPTION |
|---|---|
| ε-closure(s) | Set of NFA states reachable from NFA state s on ε-transitions alone. |
| ε-closure(T) | Set of NFA states reachable from some NFA state s in set T on ε-transitions alone; = ∪_{s∈T} ε-closure(s). |
| move(T, a) | Set of NFA states to which there is a transition on input symbol a from some state s in T. |

Figure 3.31: Operations on NFA states

We must explore those sets of states that N can be in after seeing some input string. As a basis, before reading the first input symbol, N can be in any of the states of ε-closure(s₀), where s₀ is its start state. For the induction, suppose that N can be in set of states T after reading input string x. If it next reads input a, then N can immediately go to any of the states in move(T, a). However, after reading a, it may also make several ε-transitions; thus N could be in any state of ε-closure(move(T, a)) after reading input xa. Following these ideas, the construction of the set of D's states, Dstates, and its transition function D<sub>tran</sub>, is shown in Fig. 3.32.

```
initially, ε-closure(s₀) is the only state in Dstates, and it is unmarked;
while (there is an unmarked state T in Dstates) {
    mark T;
    for (each input symbol a) {
        U = ε-closure(move(T, a));
        if (U is not in Dstates)
            add U as an unmarked state to Dstates;
        Dtran[T, a] = U;
    }
}
```

Figure 3.32: The subset construction

The start state of D is ε-closure(s₀), and the accepting states of D are all those sets of N's states that include at least one accepting state of N. To complete our description of the subset construction, we need only to show how ε-closure(T) is computed for any set of NFA states T. This process, shown in Fig. 3.33, is a straightforward search in a graph from a set of states. In this case, imagine that only the ε-labeled edges are available in the graph.

```
push all states of T onto stack;
initialize ε-closure(T) to T;
while ( stack is not empty ) {
    pop t, the top element, off stack;
    for ( each state u with an edge from t to u labeled ε )
        if ( u is not in ε-closure(T) ) {
            add u to ε-closure(T);
            push u onto stack;
        }
}
```

Figure 3.33: Computing ε-closure(T)

**Example 3.21:** Figure 3.34 shows another NFA accepting (a|b)*abb; it happens to be the one we shall construct directly from this regular expression in Section 3.7. Let us apply Algorithm 3.20 to Fig. 3.34.

![](img/2a44b9071782fade81f3050c3b718341_159_0.png)

Figure 3.34: NFA N for `(a|b)*abb`

The start state A of the equivalent DFA is ε-closure(0), or A = {0, 1, 2, 4, 7}, since these are exactly the states reachable from state 0 via a path all of whose edges have label ε. Note that a path can have zero edges, so state 0 is reachable from itself along an ε-labeled path.

The input alphabet is {a, b}. Thus, our first step is to mark A and compute Dtran[A, a] = ε-closure(move(A, a)) and Dtran[A, b] = ε-closure(move(A, b)). Among the states 0, 1, 2, 4, and 7, only 2 and 7 have transitions on a, to 3 and 8, respectively. Thus, move(A, a) = {3, 8}. Also, ε-closure({3, 8}) = {1, 2, 3, 4, 6, 7, 8}, so we conclude

$Dtran[A,a] = \varepsilon\text{-closure}(\mathrm{move}(A,a)) = \varepsilon\text{-closure}(\{3,8\}) = \{1,2,3,4,6,7,8\}$

Let us call this set $B$, so $Dtran[A,a] = B$.

Now, we must compute $Dtran[A,b]$. Among the states in $A$, only 4 has a transition on $b$, and it goes to 5. Thus,

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

![](img/2a44b9071782fade81f3050c3b718341_160_0.png)

Figure 3.36: Result of applying the subset construction to Fig. 3.34

### 3.7.2 Simulation of an NFA

A strategy that has been used in a number of text-editing programs is to construct an NFA from a regular expression and then simulate the NFA using something like an on-the-fly subset construction. The simulation is outlined below.

**Algorithm 3.22:** Simulating an NFA.

**INPUT:** An input string *x* terminated by an end-of-file character *eof*. An NFA *N* with start state *s₀*, accepting states *F*, and δ-transition function *move*.

**OUTPUT:** Answer “yes” if *N* accepts *x*; “no” otherwise.

**METHOD:** The algorithm keeps a set of current states *S*, those that are reached from *s₀* following a path labeled by the inputs read so far. If *c* is the next input character, read by the function `nextChar()`, then we first compute `move(S,c)` and then close that set using ε-closure(). The algorithm is sketched in Fig. 3.37.

```
1)   S = ε-closure(s₀);
2)   c = nextChar();
3)   while (c != eof) {
4)       S = ε-closure(move(S,c));
5)       c = nextChar();
6)   }
7)   if (S ∩ F != ∅) return "yes";
8)   else return "no";
```

Figure 3.37: Simulating an NFA

### 3.7.3 Efficiency of NFA Simulation

If carefully implemented, Algorithm 3.22 can be quite efficient. As the ideas involved are useful in a number of similar algorithms involving searching of graphs, we shall look at this implementation in additional detail. The data structures we need are

- 1. Two stacks, each of which holds a set of NFA states. One of these stacks, *oldStates*, holds the “current” set of states, i.e., the value of *S* on the right side of line (4) in Fig. 3.37. The second, *newStates*, holds the “next” set of states — *S* on the left side of line (4). Unseen is a step where, as we go around the loop of lines (3) through (6), *newStates* is transferred to *oldStates*.
- 2. A boolean array *alreadyOn*, indexed by the NFA states, to indicate which states are in *newStates*. While the array and stack hold the same information, it is much faster to interrogate *alreadyOn[s]* than to search for state *s* on the stack *newStates*. It is for this efficiency that we maintain both representations.
- 3. A two-dimensional array *move[s, a]* holding the transition table of the NFA. The entries in this table, which are sets of states, are represented by linked lists.

To implement line (1) of Fig. 3.37, we need to set each entry in array *alreadyOn* to FALSE, then for each state *s* in ε-closure(*s₀*), push *s* onto *oldStates* and set *alreadyOn[s]* to TRUE. This operation on state *s*, and the implementation of line (4) as well, are facilitated by a function we shall call *addState(s)*. This function pushes state *s* onto *newStates*, sets *alreadyOn[s]* to TRUE, and calls itself recursively on the states in *move[s, ε]* in order to further the computation of ε-closure(*s*). However, to avoid duplicating work, we must be careful never to call *addState* on a state that is already on the stack *newStates*. Figure 3.38 sketches this function.

```
9)    addState(s) {
10)       push s onto newStates;
11)       alreadyOn[s] = TRUE;
12)       for (t on move[s, ε])
13)           if (!alreadyOn[t])
14)               addState(t);
15)   }
```

Figure 3.38: Adding a new state *s*, which is known not to be on *newStates*

We implement line (4) of Fig. 3.37 by looking at each state *s* on *oldStates*. We first find the set of states *move[s, c]*, where *c* is the next input, and for each
