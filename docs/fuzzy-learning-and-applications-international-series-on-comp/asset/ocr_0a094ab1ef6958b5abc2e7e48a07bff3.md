+   R1: IF error IS A11 AND derror IS A12 THEN u IS k1
+   R2: IF error IS A11 AND derror IS A22 THEN u IS k2
+   R3: IF error IS A11 AND derror IS A32 THEN u IS k3
+   R4: IF error IS A21 AND derror IS A12 THEN u IS k4
+   R5: IF error IS A21 AND derror IS A22 THEN u IS k5
+   R6: IF error IS A21 AND derror IS A32 THEN u IS k6
+   R7: IF error IS A31 AND derror IS A12 THEN u IS k7
+   R8: IF error IS A31 AND derror IS A22 THEN u IS k8
+   R9: IF error IS A31 AND derror IS A32 THEN u IS k9

The defuzzified controller output is computed as:

```
u* = (∑_{i=1}^9 μ_i * k_i) / (∑_{i=1}^9 μ_i)  (9.5)
```

where:
μ_i = min(A_{j1}(error), A_{k2}(derror)) for j, k, i = 1, 2, 3.

A classical genetic algorithm was used in order to minimize the sum of the quadratic error between the reference signal (which in this case is zero) and the output of the closed-loop controlled system when the considered set of disturbances is applied to the system for T_f = 0.1 sec.. The initial conditions are set to zero for each simulation. Each fuzzy set was coded by 2 binary substrings (8 bit per substring) which identify the 2 break points of a symmetric triangular membership function. A population of 40 individuals was selected. For the variable error the range is [−0.01, 0.01] while for the error derivative the bound is [−0.001, 0.001]. The output of each rule can belong to the set [−0.03, 0.03]. The maximum number of generations is MAXGEN = 45. The membership functions and consequents obtained are given in Fig. 9.8.

In Fig. 9.9 a comparison is made between the output of the system controlled with the classical PD regulator and the fuzzy controller when band-limited white noise disturbance acts on the system.

As can be observed from the figure, the controllers' performance is quite similar. Moreover, if the whole set of disturbances is considered, the classical PD controller outperforms the fuzzy controller. The proposed strategy, which for simpler systems usually gives good results, is therefore not suitable for the CD focusing system. In the following section it will be shown that, by using a slightly different optimization procedure, an efficient fuzzy controller can be built. The improvement introduced by the fuzzy controller is also discussed.