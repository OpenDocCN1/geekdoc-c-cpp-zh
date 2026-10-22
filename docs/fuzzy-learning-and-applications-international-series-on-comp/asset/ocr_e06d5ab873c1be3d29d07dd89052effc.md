was proposed for analog fuzzy design in [25]. Analysis of this circuit assuming equal differential pairs and using the square-law MOS transistor characteristics [26] yields:

```
s_ij = { 0 , ~x_ij- < -E_Q ; (1 + sqrt(2)/E_Q) I_Q ~x_ij- sqrt(1 - ~x_ij-^2 / (2 E_Q^2)) , -E_Q < ~x_ij- < E_Q ; 2 I_Q , otherwise ; (1 - sqrt(2)/E_Q) I_Q ~x_ij+ sqrt(1 - ~x_ij+^2 / (2 E_Q^2)) , -E_Q < ~x_ij+ < E_Q ; 0 , ~x_ij+ > E_Q } (2.6)
```

where ~x_ij- = (x_i - E_ij-), ~x_ij+ = (x_i - E_ij+) and E_Q = sqrt(I_Q / beta_N1), beta_N1 is the large signal transconductance factor of the transistors in the differential pairs¹ and we assume that the membership function width is large enough to allow the output current to reach the unit logic value (I_Q) at the center.

This membership function circuit shares the advantages of Fig.2.6(b) regarding the control of the centers and widths by applying voltages to high input impedance terminals,

```
2 Delta_ij = E_ij+ - E_ij-      2 E_ijC = E_ij+ + E_ij-   (2.7)
```

On the other hand, the slope at the crossover points zeta_ij is controlled by the large signal transconductance of the MOS transistor²,

```
zeta_ij = sqrt(2 I_Q beta_N1)   (2.8)
```

The main advantage of this membership function circuit is that it does not require any linearization circuitry – why linearize if the whole behavior is non-linear? Thus, it features a minimum area occupation and power consumption, and full usage of the transconductor input dynamic range. On the other hand, it has been shown that the shape in (2.6) can actually realize the universal

> 1. This equation shows the simplest case where the positive and negative input transistors are equal.
> 2. Using the bias current to control the slope is not convenient because the bias current sets the logical value "1".