```
0% of the particles escaped

Enter the thickness of the shield, the limit on the
number of collisions, and the number of neutrons:
4 5 100

3% of the particles escaped

Enter the thickness of the shield, the limit on the
number of collisions, and the number of neutrons:
8 10 500

0.2% of the particles escaped
```

In the four sample runs of the program, the first two are test cases. In the first test case, the neutron will move only once because each first move is interpreted as a collision and the limit on the number of collisions is 1. Because each of the four possible moves is equally likely, we would expect 25 percent of the neutrons to escape on the average, and the result produced by the program is consistent with this value. In the second test case, the shielding is 100 units thick and the limit on the number of collisions is small, so we expect almost none of the neutrons to escape through the shield.

# 7.6.4 Normal Distributions

Most random number generators generate random numbers having a **uniform distribution**, but they can also be used to generate random numbers having other distributions. The **normal distribution** is especially important because it models many physical processes. For example, the heights and weights of people, the lifetime of lightbulbs, the tensile strength of steel produced by a machine, and, in general, the variations in parts produced in almost any manufacturing process, have normal distributions. The normal distribution has the familiar bell-shaped curve.

![](bbox=[0.311, 0.694, 0.707, 0.811])

where μ is the mean of the distribution, σ is the standard deviation, and approximately two-thirds of the area under the curve lies between μ − σ and μ + σ. A normal distribution having μ = 0 and σ = 1 is called a **standard normal distribution**, and random numbers having approximately this distribution can be generated quite easily from a uniform distribution with the following algorithm: