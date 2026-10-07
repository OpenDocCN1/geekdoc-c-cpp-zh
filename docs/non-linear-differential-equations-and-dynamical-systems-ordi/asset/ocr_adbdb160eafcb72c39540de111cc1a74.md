# 4.6.8 Non-Linear Parametric Resonance by Forcing at the Second Harmonic

The forcing of a linear oscillator (4.329b) at an applied frequency (4.329a) close (4.302a) to the second harmonic of the natural frequency leads to the response (4.329c):

ωₐ = 3(ω₀ + ε):      ẍ₁ + ω₀²x₁ = fₐ cos(ωₐ t),    x₁(t) = − fₐ / (8 ω₀²) cos[3(ω₀ + ε) t]. (4.329a–c)

The first-order approximation for the damped, non-linear oscillator (4.303) is (4.330):

ẍ₂ + 2λ ẋ₂ + ω₀² x₂ + α x₂² + β x₂³ = −3β x₁ x₂² + … , (4.330)

where only the term linear in the first order and quadratic in the second order was retained. The reason is that for an oscillation (4.331b) close to the natural frequency (4.331a):

ω = ω₀ + ε:      x₂(t) = b cos[(ω₀ + ε) t] = b cos(ω t), (4.331a, b)

the forcing term on the r.h.s. of (4.330):

−3β x₁(t)[x₂(t)]² = 3β fₐ b² / (8 ω₀²) cos²[(ω₀ + ε) t] cos[3(ω₀ + ε) t]

= 3β fₐ b² / (16 ω₀²) {1 + cos[2(ω₀ + ε) t]} cos[3(ω₀ + ε) t] (4.331c)

= 3β fₐ b² / (32 ω₀²) {cos[(ω₀ + ε) t] + … } ,

+   (i) contains a triple frequency multiplied by the square of the frequency; (ii) the latter introduces a double frequency; (iii) the product of the double and triple frequency reintroduces the oscillation frequency that causes resonance; and (iv) the resonant term on the r.h.s. of (4.330) ≡ (4.331c) and the substitution of the l.h.s. of (4.330) as in (4.303) by the oscillation frequency (4.304a) as in (4.305) leads to:

ẍ₂ + 2λ ẋ₂ + ω² x₂ = 3β fₐ b² / (32 ω₀²) cos[(ω₀ + ε) t]. (4.332)