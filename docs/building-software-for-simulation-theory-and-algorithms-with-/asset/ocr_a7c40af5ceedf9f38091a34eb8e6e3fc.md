![](bbox=[0.33, 0.1, 0.73, 0.51])

**FIGURE B.4** Lookahead of components connected in series (a) and in parallel (b).

response function that satisfies y₁(t′ ⊳ (ε, 0)) = y₂(t′ ⊳ (ε, 0)), where t′ is the same described above. So, if the input trajectory is known to time t, then the output is fixed to, but not at, time t ⊳ (ε, 0).[^3]

Lookahead in an atomic model is found by a careful study of its dynamics. An atomic model whose autonomous actions are always separated by some positive, real interval of time has a lookahead equal to that interval. The machine model from Section 4.2.3 has this property; it has a lookahead equal to its processing time. The tank's *PacketProcessing* model has this property as well; its lookahead is equal to the packet processing time.

The lookahead of a network model can be found from the lookaheads of its components. The combined lookahead of models connected in series is equal to the sum of their individual lookaheads, a fact derived easily from the definition. Referring to Figure B.4, the response of the first component to x|t, t′ is known to time t′ ⊳ (ε₁, 0). Consequently, the input to the second component is known to this

[^3]: A more restrictive definition of lookahead is found in most of the literature on conservative parallel simulation; standard definitions can be found, for example, in the textbook by Fujimoto [44]. Our definition allows a model to produce output in the interval spanned by its lookahead; other definitions permit this only in special cases.