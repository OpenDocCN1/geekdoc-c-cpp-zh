To obtain a rough estimate of the round-off error, we observe that differentiation essentially subtracts the value of a function at argument x from that of the same function at argument x + h and then divide by h: y′ ≃ [y(t + h) − y(t)]/h. As h is made continually smaller, we eventually reach the round-off error limit where y(t + h) and y(t) differ by just machine precision εₘ:

ε_ro ≃ ε_m / h. (5.14)

Consequently, round-off and approximation errors become equal when

ε_ro ≃ ε_app , (5.15)

ε_m / h ≃ ε_fd^app = y^(2) h / 2 ,   ε_m / h ≃ ε_cd^app = y^(3) h² / 24 , (5.16)

⇒ h_fd² = 2 ε_m / y^(2) ,      ⇒ h_cd³ = 24 ε_m / y^(3) . (5.17)

We take y′ ≃ y^(2) ≃ y^(3) (which may be crude in general, although not bad for e^t or cos t) and assume double precision, ε_m ≃ 10⁻¹⁵:

h_fd ≃ 4 × 10⁻⁸ ,          h_cd ≃ 3 × 10⁻⁵ , (5.18)

⇒ ε_fd ≃ ε_m / h_fd ≃ 3 × 10⁻⁸ ,   ⇒ ε_cd ≃ ε_m / h_cd ≃ 3 × 10⁻¹¹ . (5.19)

This may seem backward because the better algorithm leads to a larger h value. It is not. The ability to use a larger h means that the error in the central-difference method is about 1000 times smaller than the error in the forward-difference method.

The programming for numerical differentiation is simple:

```
FD = (y(t+h) - y(t)) /h;          // forward diff
CD = (y(t+h/2) - y(t-h/2)) /h;    // central diff
ED = (8*(y(t+h/4)-y(t-h/4)) - (y(t+h/2)-y(t-h/2)))/3/h; // extrap
```

+   1. Use forward-, central-, and extrapolated-difference algorithms to differentiate the functions cos t and e^t at t = 0.1, 1, and 100.
+   a) Print out the derivative and its relative error ℰ as functions of h. Reduce the step size h until it equals machine precision h ≃ ε_m.
+   b) Plot log₁₀ |ℰ| vs. log₁₀ h and check whether the number of decimal places obtained agrees with the estimates in the text.
+   c) See if you can identify regions where algorithmic (series truncation) error dominates at large h and the round-off error at small h in your plot. Do the slopes agree with our model’s predictions?