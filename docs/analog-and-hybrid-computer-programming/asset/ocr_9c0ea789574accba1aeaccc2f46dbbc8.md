# 6.6 Ballistic trajectory

The following example computes the two-dimensional ballistic trajectory of a projectile fired from a cannon taking the velocity-dependent drag, which slows down the projectile, into account. This drag causes the trajectory to deviate from a simple symmetric parabola as it will be steeper on its trailing path than on its leading part. The drag δ(v) is assumed to be of the general form

δ(v) = r v²  (6.17)

with v = √(x² + y²).

This is a bit oversimplified as, according to Siacci for example, a realistic drag function for a historic projectile has the form

δ(v) = 0.2002v − 48.05 + √(9.6 + (0.1648v − 47.95)²) + 0.0442v(v − 300) / (371 + (v/200)¹⁰).

Nevertheless, (6.17) will suffice for the following example.

The general equations of motion of the projectile in this two-dimensional problem are

ẍ = − δ(v)/m cos(φ) and  (6.18)  ÿ = −g − δ(v)/m sin(φ)  (6.19)

with g representing the acceleration of gravity, v denoting the projectile's velocity, and m being its mass. Accordingly, it is cos(φ) = ẋ / v and sin(φ) = ẏ / v.

Setting the mass m := 1 and rearranging (6.18) and (6.19) gives following set of differential equations:  ẍ = − δ(v)/v ẋ  ÿ = −g − δ(v)/v ẏ