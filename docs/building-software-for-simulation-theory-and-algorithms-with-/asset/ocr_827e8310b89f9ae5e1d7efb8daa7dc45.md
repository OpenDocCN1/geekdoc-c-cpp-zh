![](bbox=[0.35, 0.132, 0.663, 0.259])

**FIGURE 3.5** A logical function constructed from two types of atomic models.

where ⊕ is exclusive-or (i.e., binary addition). The machine has two inputs: x₁ and x₂. It has a single output y and remembers its previous output for use in computing its next output. The machine is constructed with two types of atomic components—one computes the exclusive-or function and the other has a memory to store y. The model’s organization is illustrated in Figure 3.5.

The component that calculates exclusive-or is denoted O for exclusive-or. It has two inputs and a single output. The input bag always contains 2 bits: b₁ and b₂. The output bag contains a single bit. The O machine has two possible states corresponding to the two possible results of its logical operation. The input, output, and state sets are

X_O = Y_O = S_O = {0, 1}

The output function and state transition functions are

λ_O(s_O) = {s_O}
δ_O(s_O, (b₁, b₂)) = b₁ ⊕ b₂

The memory component, denoted M for memory, has a single input, single output, and 2² possible states. It is defined by

X_M = Y_M = {0, 1}
S_M = {0, 1} × {0, 1}
δ_M((q₁, q₂), {x}) = (q₂, x)
λ_M((q₁, q₂)) = {q₁}

Both models have state transition functions that are only partially defined. Recall that the state transition function takes a state in S and a bag in the set X^R to a new state in S. To obtain a fully defined state transition function, a new state must be