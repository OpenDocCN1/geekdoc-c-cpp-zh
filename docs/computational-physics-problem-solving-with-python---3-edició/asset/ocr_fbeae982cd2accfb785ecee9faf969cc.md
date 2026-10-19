![](bbox=[0.17, 0.11, 0.75, 0.42])

Figure 14.8 A chaotic attractor for the 4D Lotka–Volterra model projected onto three axes.

which all species coexist:

```
p_i(t = 0) = ⎛0.3013⎞
                ⎜0.4586⎟
                ⎜0.1307⎟
                ⎝0.3557⎠ .  (14.45)
```

One way to visualize the solution to (14.43) is to make four plots of p₁(t), p₂(t), p₃(t), and p₄(t) vs. time. The results are quite interesting, and we leave that as an exercise for you. A more illuminating visualization would be to create a 4D phase–space plot of [p₁(tᵢ), p₂(tᵢ), p₃(tᵢ), p₄(tᵢ)] for i = 1, N, where N is the number of time steps used in your numerical solution. Even in the presence of chaos, the geometric structure so created may have a smooth and well-defined shape. Unfortunately, we have no way to show such a plot, and so in its stead we must project the 4D structure onto 2D and 3D axes. We show one such 3D plot in Figure 14.8. This is a classic type of chaotic attractor, with the 3D structure folded over into a nearly 2D structure (the Rossler equation is famous for producing such a structure).