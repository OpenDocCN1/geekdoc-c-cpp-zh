With symbols, a reduction is implemented by popping the body of the production from the stack (on line (2), the body is **id**) and pushing the head of the production (in this case, *F*). With states, we pop state 5 for symbol **id**, which brings state 0 to the top and look for a transition on *F*, the head of the production. In Fig. 4.31, state 0 has a transition on *F* to state 3, so we push state 3, with corresponding symbol *F*; see line (3).

As another example, consider line (5), with state 7 (symbol *) on top of the stack. This state has a transition to state 5 on input **id**, so we push state 5 (symbol **id**). State 5 has no transitions, so we reduce by *F* → **id**. When we pop state 5 for the body **id**, state 7 comes to the top of the stack. Since state 7 has a transition on *F* to state 10, we push state 10 (symbol *F*). □

# ### 4.6.3 The LR-Parsing Algorithm

A schematic of an LR parser is shown in Fig. 4.35. It consists of an input, an output, a stack, a driver program, and a parsing table that has two parts (ACTION and GOTO). The driver program is the same for all LR parsers; only the parsing table changes from one parser to another. The parsing program reads characters from an input buffer one at a time. Where a shift-reduce parser would shift a symbol, an LR parser shifts a *state*. Each state summarizes the information contained in the stack below it.

![](bbox=[0.334, 0.646, 0.718, 0.738])

Figure 4.35: Model of an LR parser

The stack holds a sequence of states, s₀s₁ … sₘ, where sₘ is on top. In the SLR method, the stack holds states from the LR(0) automaton; the canonical-LR and LALR methods are similar. By construction, each state has a corresponding grammar symbol. Recall that states correspond to sets of items, and that there is a transition from state i to state j if GOTO(Iᵢ, X) = Iⱼ. All transitions to state j must be for the same grammar symbol X. Thus, each state, except the start state 0, has a unique grammar symbol associated with it.⁴

⁴The converse need not hold; that is, more than one state may have the same grammar