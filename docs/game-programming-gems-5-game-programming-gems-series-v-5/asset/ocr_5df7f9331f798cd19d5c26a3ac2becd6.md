When the battle is over, 775 orcs remain in the Blue army ready to battle another army,

\( B_{B=0} = \sqrt{1000^2 - \frac{10}{1} 200^2} = 775. \)

# How Long Does the Combat Last?

The amount of time it takes for the losing army to be destroyed is given by one of these equations. The result is valid only for the winning army. One important thing to note is that if the two armies are equally matched, the combat will last forever.

```
\( t_{R=0} = \frac{\tanh^{-1} \left( \frac{R_0}{B_0} \sqrt{\frac{c_R}{c_B}} \right)}{\sqrt{c_R c_B}} \\
\( t_{B=0} = \frac{\tanh^{-1} \left( \frac{B_0}{R_0} \sqrt{\frac{c_R}{c_K}} \right)}{\sqrt{c_B c_R}} \) (3.3.10)
```

In this scenario, if nearly one quarter of the Red army is destroyed in three seconds with minimal losses to the Blue army, it is expected that the rest of the Red army is destroyed nearly as quickly. The actual duration of the battle is .236 minutes or 14 seconds.

```
\( t_{R=0} = \frac{\tanh^{-1} \left( \frac{200}{1000} \sqrt{\frac{10}{1}} \right)}{\sqrt{10 \cdot 1}} = .236 \) (3.3.11)
```

# Scenario 2: The Narrow Staircase

In this scenario, the orcs and humans instead meet on a staircase cut into the face of a cliff. Despite the size of the armies (200 humans versus 1,000 orcs), there is only room for two units to fight at a time. The difference between this scenario and the previous scenario is that only a fixed number of units (as opposed to all the units) are fighting in this scenario, so the rate that units are lost is proportional to the number of units units fighting rather than the total number of units. The following system of equations describes this scenario. The model assumes that an equal number of units fight