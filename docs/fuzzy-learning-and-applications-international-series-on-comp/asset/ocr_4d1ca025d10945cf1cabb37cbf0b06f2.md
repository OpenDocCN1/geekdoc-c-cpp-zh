![](bbox=[0.28, 0.08, 0.72, 0.46])

# Figure 10.9 Node n_i^{(k)}.

linguistic variables of κ and δ. The SI’s work-load describing nodes, on the other hand, input linguistic variables of NAC, PAR and NCD. All nodes at layer L1 only transmit input values to the next layer directly, i.e.,

```
f_i^{(1)}(u_{ij}^{(1)}) = u_{ii}^{(1)} and a_i^{(1)} = f_i^{(1)} , (10.6)
```

where u_{11}^{(1)} = PAR, u_{22}^{(1)} = NAC, u_{33}^{(1)} = NCD, u_{44}^{(1)} = δ and u_{55}^{(1)} = κ.

+   Layer L2: The nodes at this layer function as fuzzifiers. From our experience with the scheduling problem under consideration, the following term sets are used.

```
T(NAC) = {VeryHigh(VH), High(H), Medium(M), Low(L), VeryLow(VL)}, T(x) = {High(H), Medium(M), Low(L)}, x ∈ {PAR, NCD, δ, κ}, T(y_i) = {Suitable(S), Unsuitable(U)}, y ∈ {1,2,3,4}.
```

Each node at this layer performs a bell-shape membership function defined as follows:

```
f_i^{(2)}(u_{ij}^{(2)}) = M_{z_n}^j(m_{jn}^{(I)}, σ_{jn}^{(I)}) = - (u_{ij}^{(2)} - m_{jn}^{(I)})^2 / (σ_{jn}^{(I)})^2 and a_i^{(2)} = e^{f_i^{(2)}}, (10.7)
```

where u_{ij}^{(2)} = a_j^{(1)}, 1 ≤ i ≤ k. The index k is given by:

```
k = |T(PAR)| + |T(NAC)| + |T(NCD)| + |T(δ)| + |T(κ)| = 17.
```

Here |T(x)| denotes the number of terms in T(x) and j = ⌈i+1/2⌉. Furthermore, m_{jn}^{(I)} and σ_{jn}^{(I)} are the mean and the standard deviation of the bell-shape