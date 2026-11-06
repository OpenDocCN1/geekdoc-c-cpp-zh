time interval the velocity v is nearly constant, and we can compute the distance the ball moves as Δs = vΔt. In our program, we will simply set

```
```
const double DELTA_T = 0.01;
```
```

and update the position by

```
```
s = s + v * DELTA_T;
```
```

The velocity changes constantly—in fact, it is reduced by the gravitational force of the earth. In a short time interval, Δv = -gΔt, we must keep the velocity updated as

```
```
v = v - g * DELTA_T;
```
```

In the next iteration the new velocity is used to update the distance.

Now run the simulation until the cannonball falls back to the earth. Get the initial velocity as an input (100 m/sec is a good value). Update the position and velocity 100 times per second, but print out the position only every full second. Also printout the values from the exact formula \(s(t) = -\frac{1}{2}gt^2 + v_0t\) for comparison.

![](bbox=[0.612, 0.352, 0.923, 0.501])

*Note: You may wonder whether there is a benefit to this simulation when an exact formula is available. Well, the formula from the calculus book is not exact. Actually, the gravitational force diminishes the farther the cannonball is away from the surface of the earth. This complicates the algebra sufficiently that it is not possible to give an exact formula for the actual motion, but the computer simulation can simply be extended to apply a variable gravitational force. For cannonballs, the calculus-book formula is actually good enough, but computers are necessary to compute accurate trajectories for higher-flying objects such as ballistic missiles.*

# **Engineering P4.30** A simple model for the hull of a ship is given by

\[
|y| = \frac{B}{2}\left[1-\left(\frac{2x}{L}\right)^2\right]\left[1-\left(\frac{z}{T}\right)^2\right]
\]

where \(B\) is the beam, \(L\) is the length, and \(T\) is the draft.

![](bbox=[0.425, 0.742, 0.803, 0.928])