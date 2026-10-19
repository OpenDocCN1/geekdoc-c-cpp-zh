as the area to the left of r = x on the plot of u(r) vs. r. It follows immediately from the definition (5.103) that W(x) has the properties

W(−∞) = 0 ;   W(∞) = 1 ,  (5.104)
 dW(x)/dx = w(x) ,   dW(x) = w(x) dx = u(r) dr .  (5.105)

Consequently, Wi = {ri} is a uniform sequence of random numbers, and we just need to invert (5.103) to obtain x values distributed with probability w(x).

The crux of this technique is being able to invert (5.103) to obtain x = W−1(r). Let us look at some analytic examples to get a feel for these steps (numerical inversion is possible and frequent in realistic cases).

# Uniform weight function w   We start with the familiar uniform distribution

w(x) = { 1/(b−a), if a ≤ x ≤ b,  0, otherwise.  (5.106)

After following the rules, this leads to

W(x) = ∫_a^x dx' 1/(b−a) = (x−a)/(b−a)  (5.107)
⇒  x = a + (b−a)W   ⇒   W−1(r) = a + (b−a)r ,  (5.108)

where W(x) is always taken as uniform. In this way, we generate uniform random 0 ≤ r ≤ 1 and uniform random a ≤ x ≤ b.

# Exponential weight   We want random points with an exponential distribution:

w(x) = { 1/λ e^{−x/λ}, for x > 0,  0, for x < 0,  W(x) = ∫_0^x dx' 1/λ e^{−x'/λ} = 1 − e^{−x/λ} ,  (5.109)
⇒  x = −λ ln(1−W) ≡ −λ ln(1−r) .  (5.110)

In this way, we generate uniform random r: [0,1] and obtain x = −λ ln(1−r) distributed with an exponential probability distribution for x > 0. Notice that our prescription (5.93) and (5.94) tells us to use w(x) = e^{−x/λ}/λ to remove the exponential-like behavior from an integrand and place it in the weights and scaled points (0 ≤ xi ≤ ∞). Because the resulting integrand will vary less, it may be approximated better as a polynomial:

∫_0^∞ dx e^{−x/λ} f(x) ≃ λ/N ∑_{i=1}^N f(xi) ,   xi = −λ ln(1−ri) .  (5.111)