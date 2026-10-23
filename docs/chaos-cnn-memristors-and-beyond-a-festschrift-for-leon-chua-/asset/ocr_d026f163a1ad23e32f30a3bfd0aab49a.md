![](bbox=[0.09, 0.09, 0.49, 0.44])

Fig. 18. I_L-V_C1 projection of chaotic attractor in the circuit of Fig. 16 with the parameter values in Table 9 (reproduced from [23]).

load line associated with the resistor R in at least two places. In addition, the resistor should be eventually passive, requiring that the characteristic lies in the first and third quadrants of the V-I plane. This can be achieved by means of a five-segment piecewise-linear characteristic as described thus far. It can also be realized with a cubic characteristic. In this case, the driving-point characteristic of N_R is defined by

```
f(V) = G_a V - (G_a / V_max^2) V^3    (20)
```

where G_a is the slope of the characteristic at the origin and ±V_max are the outer zeroes, as shown in Fig. 19.

In 1985, Matsumoto et al. simulated a Chua's circuit with a cubic nonlinearity [22]. Their double scroll attractor is shown in Fig. 20. A decade later, Zhong presented an implementation of Chua's circuit using a cubic nonlinearity [26]. The nonlinear resistor, shown in Fig. 21, contains two analog multipliers, an op amp, and five resistors.

This implementation requires a significant amount of circuitry and suffers from limited speed of operation due to the compensation capacitor in the op amp. An approximately cubic nonlinearity can be realized more simply using four cross-coupled MOSFETs, as shown in Fig. 22 [25]. The measured V-I characteristic of this subcircuit is shown in Fig. 23.

![](bbox=[0.51, 0.09, 0.9, 0.33])

Fig. 19. Cubic driving-point characteristic with V_max = 9 V.

Chua's circuit with a four-MOSFET approximately cubic nonlinear resistor is shown in Fig. 24. The resulting experimentally-measured double scroll attractor is shown in Fig. 25. This implementation of the nonlinear resistor has the advantage of very small parasitic dynamics, allowing it to behave resistively at relatively high frequencies. The circuit in Fig. 24 holds the record for the fastest reported Chua's circuit [25].

# 3.4. Asymmetric nonlinearity

Although most studies of Chua's circuit have considered the case when the nonlinear resistor has a symmetric driving-point characteristic, symmetry is not a necessary ingredient for complex behavior. In 1995, Kennedy studied the dynamics of Chua's circuit with a gross asymmetry and showed that the dynamics of the continuous two-region piecewise-linear Colpitts oscillator [16] may be mapped onto an equivalent asymmetric Chua's oscillator by choosing the breakpoints of an asymmetric Chua diode such that the resulting attractor is confined to two regions of the state space [18]. The dynamics of the circuits are equivalent in the sense that the vector field of the Colpitts oscillator is linearly conjugate to that of the asymmetric Chua's circuit.