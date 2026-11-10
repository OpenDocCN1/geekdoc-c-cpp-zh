# ### 3.7.3 Efficiency of NFA Simulation

If carefully implemented, Algorithm 3.22 can be quite efficient. As the ideas involved are useful in a number of similar algorithms involving searching of graphs, we shall look at this implementation in additional detail. The data structures we need are

+   1. Two stacks, each of which holds a set of NFA states. One of these stacks, *oldStates*, holds the “current” set of states, i.e., the value of *S* on the right side of line (4) in Fig. 3.37. The second, *newStates*, holds the “next” set of states — *S* on the left side of line (4). Unseen is a step where, as we go around the loop of lines (3) through (6), *newStates* is transferred to *oldStates*.
+   
+   2. A boolean array *alreadyOn*, indexed by the NFA states, to indicate which states are in *newStates*. While the array and stack hold the same information, it is much faster to interrogate *alreadyOn[s]* than to search for state *s* on the stack *newStates*. It is for this efficiency that we maintain both representations.
+   
+   3. A two-dimensional array *move[s,a]* holding the transition table of the NFA. The entries in this table, which are sets of states, are represented by linked lists.

To implement line (1) of Fig. 3.37, we need to set each entry in array *alreadyOn* to FALSE, then for each state *s* in ε-closure(*s₀*), push *s* onto *oldStates* and set *alreadyOn[s]* to TRUE. This operation on state *s*, and the implementation of line (4) as well, are facilitated by a function we shall call *addState(s)*. This function pushes state *s* onto *newStates*, sets *alreadyOn[s]* to TRUE, and calls itself recursively on the states in *move[s,ε]* in order to further the computation of ε-closure(*s*). However, to avoid duplicating work, we must be careful never to call *addState* on a state that is already on the stack *newStates*. Figure 3.38 sketches this function.

```
```text
 9)   addState(s) {
10)       push s onto newStates;
11)       alreadyOn[s] = TRUE;
12)       for ( t on move[s, ε] )
13)           if ( !alreadyOn[t] )
14)               addState(t);
15)   }
```
```

Figure 3.38: Adding a new state *s*, which is known not to be on *newStates*

We implement line (4) of Fig. 3.37 by looking at each state *s* on *oldStates*. We first find the set of states *move[s,c]*, where *c* is the next input, and for each