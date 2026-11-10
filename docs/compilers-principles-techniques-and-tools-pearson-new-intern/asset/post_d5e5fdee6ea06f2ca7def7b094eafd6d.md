
![](img/a29d16e454785bb105e96ef448ac07f6_182_0.png)

Figure 3.59: *firstpos* and *lastpos* for nodes in the syntax tree for `(a|b)*abb#`

We must also apply rule 2 to the star-node. That rule tells us positions 1 and 2 are in both *followpos*(1) and *followpos*(2), since both *firstpos* and *lastpos* for this node are {1, 2}. The complete sets *followpos* are summarized in Fig. 3.60.

| Position *n* | *followpos(n)* |
|---:|:---|
| 1 | {1, 2, 3} |
| 2 | {1, 2, 3} |
| 3 | {4} |
| 4 | {5} |
| 5 | {6} |
| 6 | ∅ |

Figure 3.60: The function *followpos*

We can represent the function *followpos* by creating a directed graph with a node for each position and an arc from position *i* to position *j* if and only if *j* is in *followpos(i)*. Figure 3.61 shows this graph for the function of Fig. 3.60.

![](img/a29d16e454785bb105e96ef448ac07f6_183_0.png)

Figure 3.61: Directed graph for the function *followpos*

It should come as no surprise that the graph for *followpos* is almost an NFA without ε-transitions for the underlying regular expression, and would become one if we:

- 1. Make all positions in *firstpos* of the root be initial states,
- 2. Label each arc from *i* to *j* by the symbol at position *i*, and
- 3. Make the position associated with endmarker # be the only accepting state.

## 3.9.5 Converting a Regular Expression Directly to a DFA

**Algorithm 3.36:** Construction of a DFA from a regular expression *r*.

**INPUT:** A regular expression *r*.

**OUTPUT:** A DFA *D* that recognizes *L(r)*.

**METHOD:**

- 1. Construct a syntax tree *T* from the augmented regular expression (*r*)#.
- 2. Compute *nullable*, *firstpos*, *lastpos*, and *followpos* for *T*, using the methods of Sections 3.9.3 and 3.9.4.
- 3. Construct *Dstates*, the set of states of DFA *D*, and *Dtran*, the transition function for *D*, by the procedure of Fig. 3.62. The states of *D* are sets of positions in *T*. Initially, each state is “unmarked,” and a state becomes “marked” just before we consider its out-transitions. The start state of *D* is *firstpos(n₀)*, where node *n₀* is the root of *T*. The accepting states are those containing the position for the endmarker symbol #.

```
initialize Dstates to contain only the unmarked state firstpos(n₀),
where n₀ is the root of syntax tree T for (r)#;
while (there is an unmarked state S in Dstates) {
    mark S;
    for (each input symbol a) {
        let U be the union of followpos(p) for all p
            in S that correspond to a;
        if (U is not in Dstates)
            add U as an unmarked state to Dstates;
        Dtran[S, a] = U;
    }
}
```

Figure 3.62: Construction of a DFA directly from a regular expression

**Example 3.37:** We can now put together the steps of our running example to construct a DFA for the regular expression *r* = (a|b)*abb. The syntax tree for (*r*)# appeared in Fig. 3.56. We observed that for this tree, *nullable* is true only for the star-node, and we exhibited *firstpos* and *lastpos* in Fig. 3.59. The values of *followpos* appear in Fig. 3.60.

The value of *firstpos* for the root of the tree is {1, 2, 3}, so this set is the start state of *D*. Call this set of states *A*. We must compute *Dtran[A, a]* and *Dtran[A, b]*. Among the positions of *A*, 1 and 3 correspond to *a*, while 2 corresponds to *b*. Thus, *Dtran[A, a] = followpos(1) ∪ followpos(3) = {1, 2, 3, 4},* and Dtran[A, b] = followpos(2) = {1, 2, 3}. The latter is state A, and so does not have to be added to Dstates, but the former, B = {1, 2, 3, 4}, is new, so we add it to Dstates and proceed to compute its transitions. The complete DFA is shown in Fig. 3.63. □

![](img/a29d16e454785bb105e96ef448ac07f6_184_0.png)

Figure 3.63: DFA constructed from Fig. 3.57

## 3.9.6 Minimizing the Number of States of a DFA

There can be many DFA’s that recognize the same language. For instance, note that the DFA’s of Figs. 3.36 and 3.63 both recognize language L((a|b)*abb). Not only do these automata have states with different names, but they don’t even have the same number of states. If we implement a lexical analyzer as a DFA, we would generally prefer a DFA with as few states as possible, since each state requires entries in the table that describes the lexical analyzer.

The matter of the names of states is minor. We shall say that two automata are *the same up to state names* if one can be transformed into the other by doing nothing more than changing the names of states. Figures 3.36 and 3.63 are not the same up to state names. However, there is a close relationship between the states of each. States *A* and *C* of Fig. 3.36 are actually equivalent, in the sense that neither is an accepting state, and on any input they transfer to the same state — to *B* on input *a* and to *C* on input *b*. Moreover, both states *A* and *C* behave like state 123 of Fig. 3.63. Likewise, state *B* of Fig. 3.36 behaves like state 1234 of Fig. 3.63, state *D* behaves like state 1235, and state *E* behaves like state 1236.

It turns out that there is always a unique (up to state names) minimum-state DFA for any regular language. Moreover, this minimum-state DFA can be constructed from any DFA for the same language by grouping sets of equivalent states. In the case of L((a|b)*abb), Fig. 3.63 is the minimum-state DFA, and it can be constructed by partitioning the states of Fig. 3.36 as {A, C}{B}{D}{E}.

In order to understand the algorithm for creating the partition of states that converts any DFA into its minimum-state equivalent DFA, we need to see how input strings distinguish states from one another. We say that string *x* distinguishes state *s* from state *t* if exactly one of the states reached from *s* and *t* by following the path with label *x* is an accepting state. State *s* is *distinguishable* from state *t* if there is some string that distinguishes them.

**Example 3.38:** The empty string distinguishes any accepting state from any nonaccepting state. In Fig. 3.36, the string *bb* distinguishes state *A* from state *B*, since *bb* takes *A* to a nonaccepting state *C*, but takes *B* to accepting state *E*. □

The state-minimization algorithm works by partitioning the states of a DFA into groups of states that cannot be distinguished. Each group of states is then merged into a single state of the minimum-state DFA. The algorithm works by maintaining a partition, whose groups are sets of states that have not yet been distinguished, while any two states from different groups are known to be distinguishable. When the partition cannot be refined further by breaking any group into smaller groups, we have the minimum-state DFA.

Initially, the partition consists of two groups: the accepting states and the nonaccepting states. The fundamental step is to take some group of the current partition, say *A* = {s1, s2, …, sk}, and some input symbol *a*, and see whether *a* can be used to distinguish between any states in group *A*. We examine the transitions from each of s1, s2, …, sk on input *a*, and if the states reached fall into two or more groups of the current partition, we split *A* into a collection of groups, so that si and sj are in the same group if and only if they go to the same group on input *a*. We repeat this process of splitting groups, until for no group, and for no input symbol, can the group be split further. The idea is formalized in the next algorithm.

**Algorithm 3.39:** Minimizing the number of states of a DFA.

**INPUT:** A DFA *D* with set of states *S*, input alphabet Σ, start state s0, and set of accepting states *F*.

**OUTPUT:** A DFA *D′* accepting the same language as *D* and having as few states as possible.

**METHOD:**

- 1. Start with an initial partition Π with two groups, *F* and *S − F*, the accepting and nonaccepting states of *D*.
- 2. Apply the procedure of Fig. 3.64 to construct a new partition Π_new.

```
initially, let Π_new = Π;
**for** ( each group G of Π ) {
    partition G into subgroups such that two states s and t
    are in the same subgroup if and only if for all
    input symbols a, states s and t have transitions on a
    to states in the same group of Π;
    /* at worst, a state will be in a subgroup by itself */
    replace G in Π_new by the set of all subgroups formed;
}
```

Figure 3.64: Construction of Π_new

- 3. If Π_new = Π, let Π_final = Π and continue with step (4). Otherwise, repeat step (2) with Π_new in place of Π.
- 4. Choose one state in each group of Π_final as the *representative* for that group. The representatives will be the states of the minimum-state DFA *D'*. The other components of *D'* are constructed as follows:

### Why the State-Minimization Algorithm Works

We need to prove two things: that states remaining in the same group in Π_final are indistinguishable by any string, and that states winding up in different groups are distinguishable. The first is an induction on *i* that if after the *i*th iteration of step (2) of Algorithm 3.39, *s* and *t* are in the same group, then there is no string of length *i* or less that distinguishes them. We shall leave the details of the induction to you.

The second is an induction on *i* that if states *s* and *t* are placed in different groups at the *i*th iteration of step (2), then there is a string that distinguishes them. The basis, when *s* and *t* are placed in different groups of the initial partition, is easy: one must be accepting and the other not, so ε distinguishes them. For the induction, there must be an input *a* and states *p* and *q* such that *s* and *t* go to states *p* and *q*, respectively, on input *a*. Moreover, *p* and *q* must already have been placed in different groups. Then by the inductive hypothesis, there is some string *x* that distinguishes *p* from *q*. Therefore, *ax* distinguishes *s* from *t*.
