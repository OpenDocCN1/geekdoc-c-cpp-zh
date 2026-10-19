of the initial conditions. Note how the phase–space plot spirals inward to a single close limit cycle, on which it remains, with little variation in prey number. This is “control,” and we may use it to start a chemical-free pest control business.

# 14.11.3

# LVM with Predation Efficiency

An additional unrealistic assumption in the original LVM is that the predators immediately eat all the prey with which they interact. As anyone who has watched a cat hunt a mouse knows, predators spend some time finding prey and also chasing, killing, eating, and digesting it (all together called handling). This extra time decreases the rate b p P at which prey are eliminated. We define the functional response p_a as the probability of one predator finding one prey. If a single predator spends time t_search searching for prey, then

```
p_a = b t_search p  ⇒  t_search = p_a / (b p) .  (14.48)
```

If we call t_h the time a predator spends handling a single prey, then the effective time a predator spends handling a prey is p_a t_h. Such being the case, the total time T that a predator spends finding and handling a single prey is

```
T = t_search + t_handling = p_a / (b p) + p_a t_h  (14.49)
```

```
⇒  p_a / T = (b p) / (1 + b p t_h) ,  (14.50)
```

where p_a / T is the effective rate of eating prey. We see that as the number of prey p → ∞, the efficiency in eating them → 1. We include this efficiency in (14.46) by modifying the rate b at which a predator eliminates prey to b / (1 + b p t_h):

```
dp/dt = a p (1 - p/K) - (b p P) / (1 + b p t_h) ,  (LVM-III) .  (14.51)
```

To be more realistic about the predator growth, we also place a limit on the predator carrying capacity but make it proportional to the number of prey:

```
dP/dt = m P (1 - P/(k p)) ,  (LVM-III) .  (14.52)
```

Solutions for the extended model (14.51) and (14.52) are shown in Figure 14.10. Observe the existence of three dynamic regimes as a function of b:

+   - small b: no oscillations, no overdamping,
+   - medium b: damped oscillations that converge to a stable equilibrium,
+   - large b: limit cycle.

The transition from equilibrium to a limit cycle is called a phase transition.