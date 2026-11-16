![](bbox=[0.28, 0.08, 0.79, 0.3])

FIGURE 4.4.2 A pipe has been put inside of the object with an initial pressure, $P_b$ of zero. It is connected to a container of a gas under pressure $P_c$ in an environment with atmospheric pressure $P_a$.

# An Ideal Gas Approximation

Because of the macroscopic size of the simulated object and microscopic size of the particles in the gas, we can neglect the interactions between gas particles and use an approximation of an ideal gas with non-colliding particles [Callen85]. This means that we will be able to use the familiar ideal gas law, shown in Equation 4.4.1.

```
$PV = nRT$ (4.4.1)
```

where:

+   - $P [\frac{N}{m^2}]$ is the pressure of the gas.
+   - $V [m^3]$ is the volume occupied by the gas.
+   - $n$ is the number of moles of the gas.
+   - $R$ is the gas constant.
+   - $T$ is the gas temperature.

In this expression, we assume that $n$, $R$, and $T$ are constant and will not change during the simulation. We also assume that we know how to calculate the volume of the body. As a result, we will get a simple expression for the calculation of the pressure inside of the object that changes only according to changes in the volume, as shown in Equation 4.4.2.