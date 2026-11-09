![](bbox=[0.126, 0.091, 0.838, 0.503])

**Figure 4.7** Structural coupling

On the right side of the diagram, we see five production code modules, α, β, γ, δ, and ε. The α and ε modules stand alone, but β is coupled to γ, which is coupled to δ. On the left, we see the test modules. Note that each of the test modules is coupled to the corresponding production code module. However, because β is coupled to γ and δ, βₜₑₛₜ may also be coupled to γ and δ.

This coupling may not be obvious. The reason that βₜₑₛₜ is likely to have couplings to γ and δ is that β may need to be constructed with γ and δ, or the methods of β may take γ and δ as arguments.

This powerful coupling between βₜₑₛₜ and so much of the production code means that a minor change to δ could affect βₜₑₛₜ, γₜₑₛₜ, and δₜₑₛₜ. Thus, the one-to-one correspondence between the tests and production code can lead to very tight coupling and fragility.