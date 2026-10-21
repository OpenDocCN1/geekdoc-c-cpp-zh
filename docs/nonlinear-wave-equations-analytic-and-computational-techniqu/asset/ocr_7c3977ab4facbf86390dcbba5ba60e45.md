β³γq_xyy(αt, βx, βy), and (qv)_x + (qw)_y = γ²β((sℜ(r))_x + (sℑ(r))_y). Assuming q is a solution to the NV equation (1.1), we find

4q_t = -u_xxx + 3q_yyy + 3(qv)_x + 3(qw)_y
⇒ 4/α γ s_t = -1/β³γ s_xxx + 3/β³γ s_xyy + 3/β²γ (sℜ(r))_x + 3/β²γ (sℑ(r))_y.

Multiplying by αγ leads to

(2.4) 4s_t = -α/β³ s_xxx + 3α/β³ s_xyy + 3α/βγ ((sr1)_x + (sr2)_y).

The table below shows the possible sign conventions possible for each term of the right hand side of equation (2.4).

| α | β | γ | Signs in (2.4) |
|---|---|---|---|
| + | + | + | -   +   + |
| - | - | + | -   +   + |
| - | + | + | +   -   - |
| + | - | + | +   -   - |
| + | + | - | -   +   - |
| - | - | - | -   +   - |
| - | + | - | +   -   + |
| + | - | - | +   -   + |

Thus, there is a fixed ratio of -3 of the coefficients of the linear spatial terms, and any other coefficient is possible by proper rescaling of independent and dependent variables.

We also consider under what rotations the Novikov-Veselov equation is invariant. Writing the NV equation as

(2.5) q_t = -∂³ q - ∂̄³ q + 3∂(qν) + 3∂̄(qν̄),

(2.6) ∂̄ν = ∂q,

it is easy to see by conjugating (2.5), that if q is real at time t0, then q stays real.

If the initial value q0(z) is invariant under rotations by ±2π/3, then the Novikov-Veselov evolution preserves this symmetry, see [46]. In particular, all radially symmetric initial values will lead to solutions with this three-fold symmetry.

Under such rotations, equation (2.5) becomes

(2.7) q_t = e^{iθ}∂_{z'}(ν' q) + e^{iθ}∂̄_{z'}(ν̄' q) - e^{3iθ}∂̄_{z'}^3 q - e^{-3iθ}∂_{z'}^3 q

where ν' = e^{-iθ}ν. The auxiliary equation becomes

e^{iθ}∂̄_{z'}ν = e^{-iθ}∂_{z'}q

or

∂̄_{z'}ν' = e^{-3iθ}∂_{z'}q,

and so we have invariant solutions under rotations of 2π/3 and 4π/3. This shows that if a solution to the NV equation has this symmetry, it must be preserved under the evolution. It does not mean that all solutions will display this type of symmetry.