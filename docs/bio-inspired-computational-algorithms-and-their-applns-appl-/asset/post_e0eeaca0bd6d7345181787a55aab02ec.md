
## 3. Test model

The power system considered is a single machine infinite bus (SMIB) system as shown in Fig. A.1 of Appendix 8.2.1. The generator is connected to the infinite bus through a double-circuit transmission line. The generator is modeled using a 6th order machine model, and is equipped with an automatic voltage regulator (AVR) which is represented by a simple exciter of first order differential equation as given in the Appendix 8.1.4. The block diagram of the AVR is shown in Fig. A.2 of Appendix 8.2.2. A supplementary controller also known as power system stabilizer (PSS) is to be designed to damp the system's oscillations. The block diagram of the PSS is shown in Fig. A.3 of Appendix 8.2.3.

The non-linear differential equations of the system are linearized around the nominal operating condition to form a set of linear equations as follows:

$$\begin{cases}\frac{d}{dt}x = Ax + Bu\\ y = Cx + Du\end{cases}$$ (3)

where:

A is the system state matrix, B is the system input matrix, C is the system output matrix and D is the feed-forward matrix.  
x is the vector of the system states, u is the vector of the system inputs and y is the vector of the system outputs.

In this work, x = [Δδ Δω Δψ_fd Δψ_1d Δψ_1q Δψ_2q ΔE_fd]^T ; u = [ΔT_m ΔV_ref]^T ; y = Δω; where, Δδ is the rotor angle deviation, Δω is the speed deviation, Δψ_fd is the field flux linkage deviation, Δψ_1d is d-axis amortisseur flux linkage deviation, Δψ_1q is the 1st q-axis amortisseur flux linkage deviation, Δψ_2q is the 2nd q-axis amortisseur flux linkage deviation, ΔE_fd is the exciter output voltage deviation. ΔT_m is the mechanical torque deviation and ΔV_ref is the voltage reference deviation.

Several operating conditions were considered for the design of the controllers. These operating conditions were obtained by varying the active power output, P_e, and the reactive power Q_e of the generator as well as the line reactance, X_e. However, for simplicity, only three operating conditions will be presented in this paper. These operating conditions are listed in the Table 1 together with the open loop eigenvalues and their respective damping ratios in % in brackets.

Table 1. Selected operating conditions with open-loop eigenvalues

| Case | Active Power P_e [p.u.] | Reactive Power Q_e [p.u.] | Line reactance X_e [p.u.] | Eigenvalues (Damping ratio) |
|------|-------------------------|---------------------------|---------------------------|------------------------------|
| 1 | 1.1000 | 0.4070 | 0.7000 | -0.2894 ± j5.2785 (0.0547) |
| 2 | 0.5000 | 0.1839 | 1.1000 | -0.3472 ± j4.3271 (0.0800) |
| 3 | 0.9000 | 0.3372 | 0.9000 | -0.2704 ± j4.7212 (0.0572) |

## 4. Fitness function

The fitness function is used to provide the measure of how individuals performed. In this instance, the problem domain was that the PSS parameters should stabilize the system simultaneously over a certain range of specified operating conditions. The PSS which parameters are to be optimized has a structure similar to the conventional PSS (CPSS) as shown in Fig. A.3 of Appendix 8.2.3. There are three parameters K_st, T1 and T2 that are to be optimized, where K_st is the PSS gain and T1 and T2 are lead-lag time constants. T_w is the washout time constant which is not critical and therefore has not been optimized.

The fitness function that was used is to maximize the lowest damping ratio. Mathematically the objective function is formulated as follows:

val = max(min(ζ_ij))  (4)

where i = 1, 2, ..., n, j = 1, 2, ..., m

ζ_ij = -σ_ij / sqrt(σ_ij² + ω_ij²)

ζ_ij is the damping ratio of the iᵗʰ eigenvalue of the jᵗʰ operating conditions. The number of the eigenvalues is n, and m is the number of operating conditions.

σ_ij and ω_ij are the real part and the imaginary part (frequency) of the eigenvalue, respectively.

## 5. PSS design

The following parameter domain constraints were considered when designing the PSS.

0 < K_s ≤ 20  
0.001 ≤ T_i ≤ 5

where K_s and T_i denote the controller gain and the lead lag time constants, respectively.

### 5.1 BGA-PSS

The following BGA parameters have been used during the design

- Population: 100
- Generation: 100
- Selection: Truncation selection (i.e., selected the best 15% of the population)
- Recombination: Line and volume
- Mutation initial R_nom: 0.01

The parameters of the BGA-PSS are given in Table A.1 of Appendix 8.2.3.

It should be mentioned that a maximum damping ratio of 50% was imposed on the BGA and GA, otherwise, their damping ratios could have been higher. If the damping of the electromechanical mode is too high this could negatively affect other modes in the system.

### 6.2 Large disturbance

A large disturbance was considered by applying a three-phase fault to the system at 0.1 seconds. The fault was applied at the sending-end of the system (near bus 1 on line 2) for 200ms. The fault was cleared by disconnecting line 2. Fig. 3 to Fig. 5 show the speed responses of the system.

Figure 3 shows the speed responses of the generator for case 1. When the system is equipped with GA-PSS and BGA-PSS it settles around 3 seconds. On the other hand, the settling time of the system equipped with the CPSS is more than doubled (6 seconds). In addition, the subsequent oscillations are larger than those of BGA and GA PSSs.

Figure 4 shows the speed responses for case 2. The system equipped with CPSS is seen to have bigger oscillations as compared to the system equipped with BGA-PSS and GA-PSS. With both BGA and GA PSSs, the system settled in approximately 3.5 sec., whereas CPSS takes more than 6 sec. to settle down. The performances of the BGA-PSS and GA-PSS are quite similar, even though the BGA-PSS performs slightly better than the GA-PSS.

Figure 5 shows the speed responses of the system for case 3. It can be seen that the system equipped with BGA and GA PSS settled in less than 4 sec compared to more than 6 sec. for the CPSS. With CPSS, the system has large overshoots and undershoots.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_321_0.png)

Fig. 3. Speed response of case 1 under three-phase fault

genetic parameters. In this work, adaptive mutation has been used to deal with the problem of premature convergence in BGA. The effectiveness of the proposed approach was demonstrated by the time and frequency domain simulation results. Eigenvalue analysis shows that the BGA based controller provides a better damping to the system for all operating conditions considered than a GA based controller. The conventional controller provides the least damping to all the operating conditions considered. The robustness of the BGA controller under large disturbance was also investigated by applying a three-phase fault to the system. Further research will be carried out in the direction of using multi-objective functions in the optimization and using a more complex power system model.

## 8. Appendix

### 8.1 Generator and Automatic Voltage Regulator (AVR) equations

#### 8.1.1 Swing equations

$$\frac{d}{dt}\Delta\omega = \frac{1}{2H}(T_m - T_e - K_D\Delta\omega)$$

$$\frac{d}{dt}\Delta\delta = \omega_0\Delta\omega$$

where

- $\delta$ is the rotor angle in rad
- $\omega$ is the synchronous speed in per-unit (p.u.)
- $\omega_0$ is the synchronous speed in rad/sec
- $H$ is the inertia constant in sec.
- $T_m$ is the mechanical torque in p.u.
- $T_e$ is the electrical torque in p.u.
- $K_D$ is the damping coefficient in torque/ p.u.

#### 8.1.2 Rotor circuit equations

$$\frac{d}{dt}\psi_{fd} = \omega_0\left(E_{fd} - \frac{R_{fd}}{L_{fd}}i_{fd}\right)$$

$$\frac{d}{dt}\psi_{1d} = -\omega_0 R_{1d}i_{1d}$$

$$\frac{d}{dt}\psi_{1q} = -\omega_0 R_{1q}i_{1q}$$

$$\frac{d}{dt}\psi_{2q} = -\omega_0 R_{2q}i_{2q}$$

### 8.2 Power system model, AVR parameters and PSS block diagram and parameters

#### 8.2.1 Power system model diagram

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_325_0.png)

Fig. A.1. System model — Single-Machine Infinite Bus (SMIB)

#### 8.2.2 Block diagram of the Automatic Voltage Regulator (AVR)

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_325_1.png)

Fig. A.2. Automatic voltage regulator structure

#### 8.2.3 Block diagram and parameters of the PSSs

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_325_2.png)

Fig. A.3. Power system stabilizer structure

In Fig. A.3, V_PSS is the output signal of the PSS, while Δω(s) is the input signal, which in this case is the speed deviation.

Table A.1. PSS parameters.

| PSSs | Ks | T1 | T2 | Tw |
|------|------|------|------|------|
| CPSS | 9.7928 | 1.1686 | 0.2846 | 2.5000 |
| GA-PSS | 13.7358 | 3.5811 | 1.2654 | 2.5000 |
| BGA-PSS | 18.8838 | 3.7604 | 1.7390 | 2.5000 |
