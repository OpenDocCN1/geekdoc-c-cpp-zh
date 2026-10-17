
incorporates the pressure and counterpressure of the crowd in each place via a bottleneck effect, which takes into account the narrowness and the length of the streets and the size of places. We will consider an oriented network with three nodes representing three places or public squares of different sizes, linked by narrow streets. In this network, we compute the equilibrium points that show the motion of the crowd after a terrorist attack. Section 3.4 is therefore devoted to the analysis of the impact of the size of the intermediate place of this network on the evacuation of the population in the face of a terrorist attack, by means of numerical simulations. The numerical results highlight that, depending on their respective size, intermediate places modulate the dynamics and the speed of flow of the crowd. In this sense, they become strategic places, both for the planners who must think about the organization of the area to host public events and festivals, and also for the terrorists who can use these strategic places to multiply the effect of their harmful actions by trapping the escape movements between two areas of action. Finally, in Section 3.5, a brief conclusion will be drawn.

### 3.2 Weighted PCR System: A Model for Analyzing the Dynamics of Human Behavior During a Disaster

#### 3.2.1 Network of Squares and Streets Modelling Spatial Urban Configurations

Just before a dramatic event like a terror attack in a city, the crowd is generally spread across several places, public squares and streets. In the aftermath of the initial shock, people rush through the streets to reach what they think will be more secure places, as one can see in Figure 3.3.

In this chapter, we define a city by a mathematical graph, where the places and public squares are called vertices or nodes and are denoted `N₁`, `N₂`, …, `Nₚ`, and the streets, escalators, doors, and stairs are the oriented edges (`Nᵢ → Nⱼ`) linking these nodes. They are oriented, because the flow from one place toward another is not symmetric during terrorist attacks. Our aim is to model the motion of the crowd through such edges. To achieve this, we must introduce some “geographical” particularities of the city, like the size of places, the narrowness of streets, and the number of people initially present in each place. This is why we need to upgrade the standard PCR model, into the Weighted PCR `WPCR` model, by introducing new data, with Weight standing for the relative sizes of crowd, places, and streets.

First, on each node `Nₖ`, `k=1, p` we call `rₖ(t)`, `cₖ(t)`, `pₖ(t)`, `qₖ(t)`, `bₖ(t)` the number of people being in reflex, control, panic, daily usual behavior, and return to normal life and `Vₖ(t)` the total number of people present at this node

`Vₖ(t) = rₖ(t) + cₖ(t) + pₖ(t) + qₖ(t) + bₖ(t)`  (3.1)

Second, in order to more precisely model the characteristics of the city, we introduce `Wₖ` the maximum capacity of the number of people who can be present in each node `Nₖ` (i.e. due to the size of the corresponding place). Each maximum capacity is a constant. Each time one must have

`Vₖ(t) ≤ Wₖ`  (3.2)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_67_0.png)

#### 3.2.2 Equations of the WPCR System on Each Node

The `WPCR` simulates human behavior, in one specific place, during a catastrophic event. As explained in the introduction, it is based on neuroscience studies. During the event, the switches from one behavioral state to another are caused by transitional dynamics, as schematized in Figure 3.2 due to:

- i. **Causal relationships** (`$B_1$`, `$B_2$`, `$C_1$`, `$C_2$`). Once the population is in the reflex behavior state, a part of it can evolve toward controlled behaviors at the rate `B₁`, while another part transitions towards panic behaviors at the rate `B₂`. Likewise, a part of the panicked population may switch to controlled behavior at the rate `C₁`. According to the evolution of the situation, individuals who have adopted a controlled behavior may switch back to panic behavior at the rate `C₂`. This process can be iterated many times.
- ii. **Processes of imitation and contagion**, which are well known in crowd psychology and have been termed “emotional contagion” (Hatfield et al. 1994). The imitation processes are modelled identically to epidemiological propagation (Provitolo 2005). The imitation is valid in both directions and is modelled by the function `F(r,c)` (see Equation (3.5)) for emotional contagion between reflex and controlled behavior (using the damping coefficients `α₁` and `α₂`), by the function `G(r,p)` (see Equation (3.6)) for emotional contagion between reflex and panic behavior (`δ₁` and `δ₂`), and by the function `H(c,p)` (see Equation (3.7)) for emotional contagion between controlled and panicked behavior (`μ₁` and `μ₂`).
- iii. **Domino effects**, which illustrate a succession of events (`s₁` and `s₂`) correspond, for example, to a new attack in an urban area or to a closed door during an evacuation. In the PCR model, the parameters `s₁` and `s₂` are either constant or built in a periodic form.

The `WPCR` model is defined on each node k by

```
Ẋ = Φ(t, X)  (3.3)
```

with `Ẋ = dX/dt`, `X = (r, c, p, q, b)^T ∈ ℝ^5` and `Φ` given by `Φ(t, X) = (Φ_i(t, X))^T`, `i = 1, ..., 5`, where the functions `Φ_i` are defined by

```
{ Φ₁(t, X_k) = ṙ_k(t) = γ(t) q_k(t)(W_k − r_k(t)) − (B₁ + B₂) r_k(t) + s₁(t) c_k(t) + s₂(t) p_k(t) + F(r_k(t), c_k(t)) r_k(t) c_k(t) + G(r_k(t), p_k(t)) r_k(t) p_k(t) Φ₂(t, X_k) = ċ_k(t) = −φ(t) c_k(t)(W_k − b_k(t)) + B₁ r_k(t) + C₁ p_k(t) − C₂ c_k(t) − s₁(t) c_k(t) − F(r_k(t), c_k(t)) r_k(t) c_k(t) + H(c_k(t), p_k(t)) c_k(t) p_k(t) Φ₃(t, X_k) = ṗ_k(t) = B₂ r_k(t) − C₁ p_k(t) + C₂ c_k(t) − s₂(t) p_k(t) − G(r_k(t), p_k(t)) r_k(t) p_k(t) − H(c_k(t), p_k(t)) c_k(t) p_k(t) Φ₄(t, X_k) = q̇_k(t) = −γ(t) q_k(t)(W_k − r_k(t)) Φ₅(t, X_k) = ḃ_k(t) = φ(t) c_k(t)(W_k − b_k(t)) } (3.4)
```

The parameters involved in Equation (3.4) are real positive coefficients:

```
B_i ≥ 0, C_i ≥ 0, i = 1, 2; α_i ≥ 0, δ_i ≥ 0, μ_i ≥ 0, i = 1, 2; s_i ≥ 0, i = 1, 2.
```

The imitation functions `F`, `G`, and `H` are real valued functions defined on ℝ × ℝ by

```
F(r(t), c(t)) = −α₁ f₁( r(t) / (c(t) + ε) ) + α₂ f₂( c(t) / (r(t) + ε) ) (3.5)
```

```
G(r(t), p(t)) = −δ₁ g₁( r(t) / (p(t) + ε) ) + δ₂ g₂( p(t) / (r(t) + ε) ) (3.6)
```

```
H(c(t), p(t)) = μ₁ h₁( c(t) / (p(t) + ε) ) − μ₂ h₂( p(t) / (c(t) + ε) ), (3.7)
```

where `ε` is a positive number and `f_i`, `g_i`, `h_i` for `i = 1, 2` are real valued functions defined on ℝ. They have a decreasing shape indicating that the behavior imitation is symmetric. Moreover they are normalized,

```
0 ≤ f_i(u) ≤ 1, 0 ≤ g_i(u) ≤ 1, 0 ≤ h_i(u) ≤ 1, ∀ u ∈ ℝ, i = 1, 2 (3.8)
```

Because this model does not take the mortality rate into account, the population remains constant. Therefore Equation (3.4) is considered when time is proceeding from an initial time `t₀ ≥ 0`, with initial condition

```
r_k(t₀) + c_k(t₀) + p_k(t₀) + q_k(t₀) + b_k(t₀) = V_k(t₀) = r_{k,0} + c_{k,0} + p_{k,0} + q_{k,0} + b_{k,0} = V_{k,0} ≤ W_k (3.9)
```

that satisfies the following properties

```
r(t₀) > 0, c(t₀) > 0, p(t₀) > 0, q(t₀) > 0, b(t₀) > 0  (3.10)
```

We suppose that the characteristic parameters `B₁`, `B₂`, `C₁`, `C₂`, of each node have the same value, because they depend on cultural and psychological factors specific to each individual rather than to spatial configurations and crowd context. It is why we use function `Φᵢ` instead of function `Φₖ,ᵢ`.

#### 3.2.3 Transitional Dynamics
