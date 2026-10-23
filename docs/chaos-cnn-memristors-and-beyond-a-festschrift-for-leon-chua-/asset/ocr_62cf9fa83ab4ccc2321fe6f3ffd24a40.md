Fig. 11. (a) A simple circuit with two dynamic devices. Parameters: ω = 200 Hz, C₁ = 1 μF, R₁ = 1kΩ, R₂ = 10¹⁴Ω, m₁ = 9.1·10⁵Ω/C. (b) The Volterra based pinched hysteresis loop (dashed) is in good agreement to the numerically calculated curve. Please note that the linear part of the memristor has been included in the linear part of the network and hence the hysteresis loop is aligned horizontally.

leads to the following equations

```
Z₂₁(ω₁) + Z₂₂(ω₁)H₁(ω₁) = 0.   (20)
→ H₁(ω₁) = − Z₂₁(ω₁)/Z₂₂(ω₁).   (21)
```

Collecting the c² terms for the second order, yields the equation

```
Z₂₂i₂₂ = −i₂₁m₁(∫ i₂₁(t′)dt′).   (22)
```

Similar to the first order, the amplitude of the response to e^{j(ω₁+ω₂)t} according to the multi tone-probing is i₂₂ = H₂(ω₁,ω₂). This allows the extraction of the second order kernel

```
→ H₂(ω₁,ω₂) = − m₁/(jω₂) · 1/Z₂₂(ω₁+ω₂) H₁(ω₂)H₁(ω₁).   (23)
```

And for the third order, we obtain in a similar way

```
Z₂₂i₂₃ = −( i₂₁m₁ ∫ i₂₂(t′)dt′ + m₂i₂₁ ∫ i₂₁(t′)dt′ ∫ i₂₁(t″)dt″ + m₁i₂₂ ∫ i₂₁dt′ )   (24)
```

```
→ H₃(ω₁,ω₂,ω₃) = − 1/Z₂₂(ω₁+ω₂+ω₃) [ m₁/(j(ω₂+ω₃)) H₁(ω₁)H₂(ω₂,ω₃) + m₂/(ω₂ω₃) H₁(ω₁)H₁(ω₂)H₁(ω₃) + m₁/(jω₃) H₂(ω₁,ω₂)H₁(ω₃) ].   (25)
```

In (23) and (24) antisymmetric kernels have been used to minimize the number of terms. Although the analytical expressions of the kernels become more complex with increasing order, their form remains the same, no matter which circuit is considered.

# 4.3. Examples

Results for the first case are given in Fig. 11. The inner part of the circuit which consists of resistors and a capacitor, can be represented by its impedance matrix Z

```
Z = ( R₁   R₁ ; R₁   R₁ + 1/(sC + 1/R₂) )   (26)
```

We assume a HP-type memristor which contains the first order memristance M(Q) = m₁·Q. The input signal is given by i₁ = î₁ sin(ω₀t). The output i₂(t) is determined first by a numerical simulation, using the Rosenbrock algorithm which is implemented in the ode23s-solver in Matlab, and