Fig. 5. The five segment piecewise-linear characteristic has three segments exclusively in the second and fourth quadrants. These correspond to the active region of the nonlinear resistor. In order to be physically realizable, notice that the nonlinear function eventually enters the first and third quadrants. Thus the nonlinear resistor is eventually passive. The linear resistor R has been plotted as a load and for particular values of R notice that we get three equilibrium points P+,0,P−.

![](bbox=[0.24, 0.09, 0.78, 0.26])

![](bbox=[0.09, 0.36, 0.48, 0.6])

Fig. 6. Physical realization of Chua's circuit including the nonlinear resistor N_R. Parameter values [12] are L = 7.14 mH, C2 = 50 nF, C1 = 5.56 nF, R = 1428 Ω. Parameter values for the nonlinear resistor N_R [9] are R1 = R2 = 220 Ω, R3 = 2.0 kΩ, R4 = R5 = 22 kΩ, R6 = 3.3 kΩ, B_p = 1 V. These values for the N_R realization lead to G_a = 1/R3 - 1/R6 (since R1 = R2), G_b = 1/R3 + 1/R4 (since R4 = R5). AD712 or equivalent operational amplifiers can be used, power supply for the op-amps are ±9 V. The op-amp power supplies have been omitted for clarity. There are a variety of other ways to realize N_R, such as cross-coupled [15] inverters. Also the inductor and capacitor values were chosen to match Matsumoto's original [12] paper. More realistic values [9] are L = 18 mH, C2 = 100 nF, C1 = 10 nF.

G_a, G_b < 0 in Eq.(7). Only the inner three segments in Fig. 5 are relevant for obtaining chaos in Chua's circuit. The outer two segments, or their nonlinear counterparts, will always be exhibited in any physical realization of the nonlinear resistor (also known in literature as the Chua diode). The outer two segments are a consequence of the law of conservation of energy. They play no role, however, in the state space region covered by Chua's attractor.

```
g(v_R) = G_b v_R + 1/2 (G_a - G_b)(|v_R + B_p| - |v_R - B_p|) (7)
```

Usually Eqs. (4) through (7) are scaled to be dimensionless via the following substitutions.

```
x ≡ v_C1 / B_p      y ≡ v_C2 / B_p      z ≡ i_L R / B_p, (8)
```

```
τ ≡ t / (R C2)      a ≡ G_a R ≈ -8/7      b ≡ G_b R ≈ -5/7, (9)
```

```
α ≡ C2 / C1 ≈ 9      β ≡ C2 R² / L ≈ 14 2/7 (10)
```

describing Chua's circuit in Fig. 6.

```
C1 dv_C1/dt = (v_C2 - v_C1)/R - g(v_C1) (4)
```

```
C2 dv_C2/dt = (v_C1 - v_C2)/R + i_L (5)
```

```
L di_L/dt = -v_C2 (6)
```

Eq. (7) defines a five-segment piecewise-linear function g(·) from Fig. 5, we emphasize that

Equations (11) through (14) are the dimensionless form of Chua's equation.

```
ẋ = α(y - x - f(x)) (11)
```

```
ẏ = x - y + z (12)
```

```
ż = -β y (13)
```

```
f(x) = b x + 1/2 (a - b)(|x + 1| - |x - 1|) (14)
```