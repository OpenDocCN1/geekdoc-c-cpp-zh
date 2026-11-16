
## 3.4. FINITE-STATE AUTOMATA

The state $q_4$ in the preceding example is often called a garbage or trap state: it is a non-accepting state which, once reached by the machine, cannot be escaped. It is fairly common to omit such states from transition diagrams. For example, one is likely to see the diagram:

![](img/e1667d904eba93816cbfc3a4b0128062_157_0.png)

Note that this cannot be a complete DFA, because a DFA is required to have a transition defined for every state-input pair. The diagram is “short for” the full diagram:

![](img/e1667d904eba93816cbfc3a4b0128062_157_1.png)

As well as recognizing what language is accepted by a given DFA, we often want to do the reverse and come up with a DFA that accepts a given language. Building DFAs for specified languages is an art, not a science. There is no algorithm that you can apply to produce a DFA from an English-language description of the set of strings the DFA should accept. On the other hand, it is not generally successful, either, to simply write down a half-dozen strings that are in the language and design a DFA to accept those strings—invariably there are strings that are in the language that aren’t accepted, and other strings that aren’t in the language that are accepted. So how do you go about building DFAs that accept all and only the strings they’re supposed to accept? The best advice I can give is to think about relevant characteristics that determine whether a string is in the language or not, and to think about what the possible values or “states” of those characteristics are; then build a machine that has a state corresponding to each possible combination of values of relevant characteristics, and determine how the consumption of inputs affects those values. I’ll illustrate what I mean with a couple of examples.

### Example 3.13

Find a DFA with input alphabet $\Sigma = \{a, b\}$ that accepts the language $L = \{w \in \Sigma^* \mid n_a(w) \text{ and } n_b(w) \text{ are both even } \}$. The characteristics that determine whether or not a string $w$ is in $L$ are the parity of $n_a(w)$ and $n_b(w)$. There are four possible combinations of “values” for these characteristics: both numbers could be even, both could be odd, the first could be odd and the second even, or the first could be even and the second odd. So we build a machine with four states $q_1, q_2, q_3, q_4$ corresponding to the four cases. We want to set up $\delta$ so that the machine will be in state $q_1$ exactly when it has consumed a string with an even number of $a$’s and an even number of $b$’s, in state $q_2$ exactly when it has consumed a string with an odd number of $a$’s and an odd number of $b$’s, and so on.

To do this, we first make the state $q_1$ into our start state, because the DFA will be in the start state after consuming the empty string $\epsilon$, and $\epsilon$ has an even number (zero) of both $a$’s and $b$’s. Now we add transitions by reasoning about how the parity of $a$’s and $b$’s is changed by additional input. For instance, if the machine is in $q_1$ (meaning an even number of $a$’s and an even number of $b$’s have been seen) and a further $a$ is consumed, then we want the machine to move to state $q_3$, since the machine has now consumed an odd number of $a$’s and still an even number of $b$’s. So we add the transition $\delta(q_1, a) = q_3$ to the machine. Similarly, if the machine is in $q_2$ (meaning an odd number of $a$’s and an odd number of $b$’s have been seen) and a further $b$ is consumed, then we want the machine to move to state $q_3$ again, since the machine has still consumed an odd number of $a$’s, and now an even number of $b$’s. So we add the transition $\delta(q_2, b) = q_3$ to the machine. Similar reasoning produces a total of eight transitions, one for each state-input pair. Finally, we have to decide which states should be final states. The only state that corresponds to the desired criteria for the language $L$ is $q_1$, so we make $q_1$ a final state. The complete machine is shown below.

![](img/e1667d904eba93816cbfc3a4b0128062_158_0.png)

### Example 3.14

Find a DFA with input alphabet $\Sigma = \{a, b\}$ that accepts the language $L = \{w \in \Sigma^* \mid n_a(w) \text{ is divisible by } 3 \}$.

The relevant characteristic here is of course whether or not the number of $a$’s in a string is divisible by 3, perhaps suggesting a two-state machine. But in fact, there is more than one way for a number to not be divisible by 3: dividing the number by 3 could produce a remainder of either 1 or 2 (a remainder of 0 corresponds to the number in fact being divisible by 3).

So we build a machine with three states $q_0, q_1, q_2$, and add transitions so that the machine will be in state $q_0$ exactly when the number of $a$’s it has consumed is evenly divisible by 3, in state $q_1$ exactly when the number of $a$’s it has consumed is equivalent to 1 mod 3, and similarly for $q_2$. State $q_0$ will be the start state, as $\epsilon$ has 0 $a$’s and 0 is divisible by 3. The completed machine is shown below. Notice that because the consumption of a $b$ does not affect the only relevant characteristic, $b$’s do not cause changes of state.

![](img/e1667d904eba93816cbfc3a4b0128062_159_0.png)

### Example 3.15

Find a DFA with input alphabet $\Sigma = \{a, b\}$ that accepts the language $L = \{w \in \Sigma^* \mid w \text{ contains three consecutive } a\text{’s } \}$.

Again, it is not quite so simple as making a two-state machine where the states correspond to "have seen aaa" and "have not seen aaa". Think dynamically: as you move through the input string, how do you arrive at the goal of having seen three consecutive $a$’s? You might have seen two consecutive $a$’s and still need a third, or you might just have seen one $a$ and be looking for two more to come immediately, or you might just have seen a $b$ and be right back at the beginning as far as seeing 3 consecutive $a$’s goes. So once again there will be three states, with the "last symbol was not an $a$" state being the start state. The complete automaton is shown below.

![](img/e1667d904eba93816cbfc3a4b0128062_159_1.png)

## Exercises

- 1. Give DFAs that accept the following languages over $\Sigma = \{a, b\}$.
  - a) $L_1 = \{x \mid x \text{ contains the substring } aba\}$
  - b) $L_2 = L(ab^*)$
  - c) $L_3 = \{x \mid n_a(x) + n_b(x) \text{ is even } \}$
  - d) $L_4 = \{x \mid n_a(x) \text{ is a multiple of } 5 \}$
  - e) $L_5 = \{x \mid x \text{ does not contain the substring } abb\}$
  - f) \( L_6 = \{x \mid x \text{ has no } a\text{'s in the even positions}\} \)
  - g) \( L_7 = L(aa^* abba^*b^*) \)

- 2. What languages do the following DFAs accept?

![](img/e1667d904eba93816cbfc3a4b0128062_160_0.png)

![](img/e1667d904eba93816cbfc3a4b0128062_160_1.png)

- 3. Let \(\Sigma = \{0, 1\}\). Give a DFA that accepts the language

\( L = \{x \in \Sigma^* \mid x \text{ is the binary representation of an integer divisible by } 3\} \).

## 3.5 Nondeterministic Finite-State Automata

As mentioned briefly above, there is an alternative school of thought as to what properties should be required of a finite-state automaton's transition function. Recall our motivating example of a C++ compiler and a legal if statement. In our description, we had the compiler in an “expecting a ”)” state; on seeing a ”)”, the compiler moved into an “expecting a ”{” or a legal statement” state. An alternative way to view this would be to say that the compiler, on seeing a ”)”, could move into one of two different states: it could move to an “expecting a ”{” state or move to an “expecting a legal statement” state. Thus, from a single state, on input ”)”, the compiler has multiple moves. This alternative interpretation is not allowed by the DFA model. A second point on which one might question the DFA model is the fact that input must be consumed for the machine to change state. Think of the syntax for C++ function declarations. The return type of a function need not be specified (the default is taken to be int). The start state of the compiler when parsing a function declaration might be “expecting a return type”; then with no input consumed, the compiler can move to the state “expecting a legal function name”. To model this, it might seem reasonable to allow transitions that do not require the consumption of input (such
