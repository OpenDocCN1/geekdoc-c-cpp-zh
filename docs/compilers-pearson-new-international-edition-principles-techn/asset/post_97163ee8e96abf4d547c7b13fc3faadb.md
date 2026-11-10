
## Eliminating the Dead State

The minimization algorithm sometimes produces a DFA with one dead state — one that is not accepting and transfers to itself on each input symbol. This state is technically needed, because a DFA must have a transition from every state on every symbol. However, as discussed in Section 3.8.3, we often want to know when there is no longer any possibility of acceptance, so we can establish that the proper lexeme has already been seen. Thus, we may wish to eliminate the dead state and use an automaton that is missing some transitions. This automaton has one fewer state than the minimum-state DFA, but is strictly speaking not a DFA, because of the missing transitions to the dead state.

- (a) The start state of $D'$ is the representative of the group containing the start state of $D$.
- (b) The accepting states of $D'$ are the representatives of those groups that contain an accepting state of $D$. Note that each group contains either only accepting states, or only nonaccepting states, because we started by separating those two classes of states, and the procedure of Fig. 3.64 always forms new groups that are subgroups of previously constructed groups.
- (c) Let $s$ be the representative of some group $G$ of $\Pi_{final}$, and let the transition of $D$ from $s$ on input $a$ be to state $t$. Let $r$ be the representative of $t$'s group $H$. Then in $D'$, there is a transition from $s$ to $r$ on input $a$. Note that in $D$, every state in group $G$ must go to some state of group $H$ on input $a$, or else, group $G$ would have been split according to Fig. 3.64.

**Example 3.40:** Let us reconsider the DFA of Fig. 3.36. The initial partition consists of the two groups $\{A,B,C,D\}\{E\}$, which are respectively the nonaccepting states and the accepting states. To construct $\Pi_{new}$, the procedure of Fig. 3.64 considers both groups on inputs $a$ and $b$. The group $\{E\}$ cannot be split, because it has only one state, so $\{E\}$ will remain intact in $\Pi_{new}$. The other group $\{A,B,C,D\}$ can be split, so we must consider the effect of each input symbol. On input $a$, each of these states goes to state $B$, so there is no way to distinguish these states using constraints that begin with $a$. On input $b$, states $A$, $B$, and $C$ go to members of group $\{A,B,C,D\}$, while state $D$ goes to $E$, a member of another group. Thus, in $\Pi_{new}$, group $\{A,B,C,D\}$ is split into $\{A,B,C\}\{D\}$, and $\Pi_{new}$ for this round is $\{A,B,C\}\{D\}\{E\}$. In the next round, we can split $\{A,B,C\}$ into $\{A,C\}\{B\}$, since A and C each go to a member of $\{A,B,C\}$ on input b, while B goes to a member of another group, $\{D\}$. Thus, after the second round, $\Pi_{new}=\{A,C\}\{B\}\{D\}\{E\}$. For the third round, we cannot split the one remaining group with more than one state, since A and C each go to the same state (and therefore to the same group) on each input. We conclude that $\Pi_{final}=\{A,C\}\{B\}\{D\}\{E\}$.

Now, we shall construct the minimum-state DFA. It has four states, corresponding to the four groups of $\Pi_{final}$, and let us pick A, B, D, and E as the representatives of these groups. The initial state is A, and the only accepting state is E. Figure 3.65 shows the transition function for the DFA. For instance, the transition from state E on input b is to A, since in the original DFA, E goes to C on input b, and A is the representative of C's group. For the same reason, the transition on b from state A is to A itself, while all other transitions are as in Fig. 3.36. □

| State | a | b |
|---|---|---|
| A | B | A |
| B | B | D |
| D | B | E |
| E | B | A |

Figure 3.65: Transition table of minimum-state DFA

### 3.9.7 State Minimization in Lexical Analyzers

To apply the state minimization procedure to the DFA's generated in Section 3.8.3, we must begin Algorithm 3.39 with the partition that groups together all states that recognize a particular token, and also places in one group all those states that do not indicate any token. An example should make the extension clear.

**Example 3.41:** For the DFA of Fig. 3.54, the initial partition is

$\{0137,7\}\{247\}\{8,58\}\{68\}\{\emptyset\}$

That is, states 0137 and 7 belong together because neither announces any token. States 8 and 58 belong together because they both announce token **a b⁺**. Note that we have added a dead state $\emptyset$, which we suppose has transitions to itself on inputs a and b. The dead state is also the target of missing transitions on a from states 8, 58, and 68.

We must split 0137 from 7, because they go to different groups on input a. We also split 8 from 58, because they go to different groups on b. Thus, all states are in groups by themselves, and Fig. 3.54 is the minimum-state DFA recognizing its three tokens.

Recall that a DFA serving as a lexical analyzer will normally drop the dead state, while we treat missing transitions as a signal to end token recognition.

### 3.9.8 Trading Time for Space in DFA Simulation

The simplest and fastest way to represent the transition function of a DFA is a two-dimensional table indexed by states and characters. Given a state and next input character, we access the array to find the next state and any special action we must take, e.g., returning a token to the parser. Since a typical lexical analyzer has several hundred states in its DFA and involves the ASCII alphabet of 128 input characters, the array consumes less than a megabyte.

However, compilers are also appearing in very small devices, where even a megabyte of storage may be too much. For such situations, there are many methods that can be used to compact the transition table. For instance, we can represent each state by a list of transitions — that is, character-state pairs — ended by a default state that is to be chosen for any input character not on the list. If we choose as the default the most frequently occurring next state, we can often reduce the amount of storage needed by a large factor.

There is a more subtle data structure that allows us to combine the speed of array access with the compression of lists with defaults. We may think of this structure as four arrays, as suggested in Fig. 3.66.⁵ The *base* array is used to determine the base location of the entries for state $s$, which are located in the *next* and *check* arrays. The *default* array is used to determine an alternative base location if the *check* array tells us the one given by $base[s]$ is invalid.

![](img/2a44b9071782fade81f3050c3b718341_189_0.png)

Figure 3.66: Data structure for representing transition tables

⁵ In practice, there would be another array indexed by states to give the action associated with that state, if any.

To compute $nextState(s, a)$, the transition for state $s$ on input $a$, we examine the *next* and *check* entries in location $l = base[s] + a$, where character $a$ is treated as an integer, presumably in the range 0 to 127. If $check[l] = s$, then this entry is valid, and the next state for state $s$ on input $a$ is $next[l]$. If $check[l] \ne s$, then we determine another state $t = default[s]$ and repeat the process as if $t$ were the current state. More formally, the function $nextState$ is defined as follows:

```c
int nextState(s,a) {
    if ( check[base[s] + a] == s ) return next[base[s] + a];
    else return nextState(default[s],a);
}
```

The intended use of the structure of Fig. 3.66 is to make the *next-check* arrays short by taking advantage of the similarities among states. For instance, state $t$, the default for state $s$, might be the state that says “we are working on an identifier,” like state 10 in Fig. 3.14. Perhaps state $s$ is entered after seeing the letters *th*, which are a prefix of keyword *then* as well as potentially being the prefix of some lexeme for an identifier. On input character $e$, we must go from state $s$ to a special state that remembers we have seen *the*, but otherwise, state $s$ behaves as $t$ does. Thus, we set $check[base[s] + e]$ to $s$ (to confirm that this entry is valid for $s$) and we set $next[base[s] + e]$ to the state that remembers *the*. Also, $default[s]$ is set to $t$.

While we may not be able to choose *base* values so that no *next-check* entries remain unused, experience has shown that the simple strategy of assigning *base* values to states in turn, and assigning each $base[s]$ value the lowest integer so that the special entries for state $s$ are not previously occupied utilizes little more space than the minimum possible.

### 3.9.9 Exercises for Section 3.9

**Exercise 3.9.1:** Extend the table of Fig. 3.58 to include the operators (a) ? and (b) +.

**Exercise 3.9.2:** Use Algorithm 3.36 to convert the regular expressions of Exercise 3.7.3 directly to deterministic finite automata.

**! Exercise 3.9.3:** We can prove that two regular expressions are equivalent by showing that their minimum-state DFA’s are the same up to renaming of states. Show in this way that the following regular expressions: $(a|b)^*$, $(a^*|b^*)^*$, and $((ε|a)b^*)^*$ are all equivalent. *Note:* You may have constructed the DFA’s for these expressions in response to Exercise 3.7.3.

**! Exercise 3.9.4:** Construct the minimum-state DFA’s for the following regular expressions:

- a) $(a|b)^*a(a|b)$.
- b) $(a|b)^*a(a|b)(a|b)$.
- c) $(a|b)^*a(a|b)(a|b)(a|b)$.
