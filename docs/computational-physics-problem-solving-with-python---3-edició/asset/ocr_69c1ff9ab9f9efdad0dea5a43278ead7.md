```
ax.set_ylabel('Time')
ax.set_zlabel('Disturbance')
p.show()                     # Show figure, close Python shell
print("That's all folks!")
```

The code SolitonAnimate.py produces an animation.

# 24.5.4

# Exploration: Solitons in Phase Space, Crossing

+   1. Explore what happens when a tall soliton collides with a short one.
+   a) Start by placing a tall soliton of height 0.8 at x = 12 and a smaller soliton in front of it at x = 26:
+   
+   $$u(x, t = 0) = 0.8\left[1 - \tanh^2\left(\frac{3x}{12} - 3\right)\right] + 0.3\left[1 - \tanh^2\left(\frac{4.5x}{26} - 4.5\right)\right].$$ (24.36)
+   
+   b) Do they reflect from each other? Do they go through each other? Do they interfere? Does the tall soliton still move faster than the short one after the collision (Figure 24.1)?
+   2. Construct phase-space plots (\dot{u}(t) vs. u(t)) of the KdeV equation for various parameter values. Note that only very specific sets of parameters produce solitons. In particular, by correlating the behavior of the solutions with your phase-space plots, show that the soliton solutions correspond to the separatrix solutions to the KdeV equation. In other words, the stability in time for solitons is analogous to the infinite period for a pendulum balanced straight upward.

# 24.6

# Solitons on Pendulum Chain

In 1955, Fermi, Ulam, and Pastu were investigating how a 1D chain of coupled oscillators disperses waves. Because waves of differing frequencies traveled through the chain with differing speeds, a pulse, which inherently includes a range of frequencies, broadens as time progresses. Surprisingly, when the oscillators were made more realistic by introducing a nonlinear term into Hooke's law

$$F(x) \simeq -k(x + \alpha x^2),$$ (24.37)

Fermi, Ulam, and Pastu found that even in the presence of dispersion, a sharp pulse in the chain would survive indefinitely. Your problem is to explain how this combination of dispersion and nonlinearity can combine to produce a stable pulse.

In Chapter 14, we studied nonlinear effects in a single pendulum arising from large oscillations. Now we go further and couple a number of those pendulums