we can now write the difference equations in Eq. (21.18):

```
v(x + Δx) - v(x) = Δv(x) = -R(x)Δx(i(x) - joL(x)Δx(i(x)
i(x + Δx) - i(x) = -G(x)Δxv(x) - joC(x)Δxv(x)
```

Converting the difference equations in Eq. (21.17) into differential equations gives us Eq. (21.19):

```
dv(x)/dx = -Ri(x) - joLi(x)
di(x)/dx = -Gv(x) - joCv(x)
```

Solving these for separate equations in V and I gives Eq. (21.20):

```
d²v(x)/dx² - (R + joL)(G + joC)v(x) = 0
d²i(x)/dx² - (R + joL)(G + joC)i(x) = 0
```

The solutions now become Eq. (21.21):

```
v(x) = v₁e⁻γx + v₂eγx
i(x) = i₁e⁻γx + i₂eγx
γ = √((R + jo)(G + joC))
```

γ – the propagation constant (a unit-less constant that expresses the change per unit length of a quantity being measured).
v(x) – expresses the voltage at any point along the transmission line.

Both the current and voltage equations are phasors and reflect the signals as a function of distance along the signal path. With a little bit of math, we can write the characteristic impedance of transmission line as Eq. (21.22):

```
Z₀ = V/I = √((R + joL) / (G + joC))
```

Letting ω → ∞, in the limit, yields a lossless transmission line as given in Eq. (21.23):

```
Z₀ → √(L/C)
```

# 21.4.1 The Lossless Transmission Line

Looking at Eq. (21.21), if we assume a lossless transmission line from an impedance point of view, R and G will often be very small, thus,

```
Let R = G = 0
```

The transmission line will now be purely reactive. The characteristic impedance, once again, becomes Eq. (21.23).