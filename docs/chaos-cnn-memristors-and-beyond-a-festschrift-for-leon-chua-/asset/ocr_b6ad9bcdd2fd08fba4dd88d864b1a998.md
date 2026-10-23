![](bbox=[0.08, 0.08, 0.48, 0.21])

Fig. 1. Chua’s five-element circuit consists of a linear inductor L, two linear capacitors (C1, C2), a linear resistor R, and a voltage-controlled nonlinear resistor N_R, called a “Chua diode” [14]

![](bbox=[0.09, 0.31, 0.48, 0.48])

Fig. 2. The driving-point characteristic of the nonlinear resistor N_R in Chua’s circuit has breakpoints at ±E and slopes G_a and G_b in the inner and outer regions, respectively.

analytically as follows:

```
f(V) = { G_b V + (G_b - G_a)E   if V < -E
         G_a V                if -E ≤ V ≤ E
         G_b V + (G_a - G_b)E   if V > E }
```

where E > 0, G_a < 0, and G_b < 0.

# 2. History

While on a visit to Japan in October 1983, having witnessed a futile attempt at producing chaos in an electrical analog of Lorenz’s equations, Prof. Leon Chua was prompted to develop a chaotic electronic circuit [4]. He realized that chaos could be produced in a piecewise-linear circuit if it possessed at least two unstable equilibrium points — one to provide stretching, and the other to fold trajectories. With this insight, he systematically identified those third-order piecewise-linear circuits containing a single voltage-controlled nonlinear resistor that could produce chaos. Specifying that the driving point characteristic of the voltage-controlled nonlinear resistor

N_R should be chosen to yield at least two unstable equilibrium points, he invented the circuit shown in Fig. 1 [4].

Let the nonlinear resistor N_R in Chua’s circuit have a symmetric piecewise-linear DP characteristic as shown in Fig. 2. Imagine that the values of the parameters are chosen such that the circuit possesses three equilibrium points (one at the origin where N_R has a locally negative slope or conductance G_a, and two in the outer regions where N_R has a locally negative conductance G_b) and that all three equilibrium points are unstable. There are three eigenvalues associated with each equilibrium point [15]. We assume that the equilibrium point at the origin has an unstable real eigenvalue and a stable pair of complex conjugate eigenvalues. In addition, suppose that the outer equilibrium point P_- has a stable real eigenvalue and an unstable complex conjugate pair. Two trajectories starting close together on the eigenplane in the outer region would be stretched apart as they spiralled away from the equilibrium point. If they could be folded back by the dynamics in the inner region and reinjected toward P_- along the stable real eigenvector, a homoclinic orbit would be produced, and chaos would result.

Figure 3 shows the structure of a spiral chaotic attractor in Chua’s circuit [15]. The piecewise-linear state space is divided (by N_R) into an inner region (denoted D_0) and two outer regions (D_-1 and D_1). There are equilibrium points in each of the three

![](bbox=[0.53, 0.62, 0.88, 0.85])

Fig. 3. Stretching and folding mechanism of chaos generation in Chua’s circuit. A trajectory spirals away from the equilibrium point P_- along the eigenplane E^c(P_-) until it enters the D_0 region, where it is folded back into D_-1 and returns to the unstable eigenplane E^r(P_-) close to P_- (reproduced from [15]).