
large conglomerates of relatively small loads can, in principle, be used to regulate frequency. One mechanism, which is considered in this section, works as follows. Homes and businesses have two electric circuits; one provides uninterrupted power and the other can be disconnected at will by the power company or, possibly, by a load aggregation company that provides regulation services to the power company. Power is supplied through the interruptible circuit at a reduced rate. If, for instance, a water heater is connected to it, then you pay less for hot water in exchange for making the heater available to the power company as a regulation resource.

The power company (or an aggregator) has a communication link to each meter and can send it a request to energize or deenergize the interruptible circuit. The communication system that makes this possible might be owned wholly by the power company. Many companies already own extensive fiberoptic networks, and the last mile to the home can be affordably bridged with wireless technology. This service might also be leased from a communication company (e.g., a phone, cable, or Internet service provider). Regardless, the complete system provides, potentially, for direct control of the electrical load at thousands, perhaps millions, of households and businesses. Significantly, this electrical load can react to a disturbance more quickly than can generators. Thousands of water heaters, for instance, can be turned off in an instant to provide rapid relief from excess load. The major source of delay is the communication network; it must be able to deliver control data in fractions of a second to loads being used for frequency regulation.

Figure 6.10 illustrates the elements of the system that are relevant to this study, which is based loosely on a similar study by Trudnowski et al. [139]. Each generator

![](img/df6085a1b35edf9c9ea818a5c66ccad9_267_0.png)

**FIGURE 6.10** Elements of the power grid and its subsystem for load control.

transmits to the control center a measurement of its frequency: measurements are sent at points Δf away from the nominal frequency f_nom; that is, it transmits a new measurement whenever f − f_nom equals k Δf, k = ..., −2, −1, 0, 1, 2, .... The control center maintains the instantaneous values of measurements from all the generators, and directs the electrical loads to effect a percentage change in demand equal to K_f Δf, where K is a parameter of the control design.

The most difficult part to model is the communication network, and a very abstract approach is taken here. The movement of data from the generators to the control center to load aggregators is modeled with a first-in first-out server and infinite queue. This simple model lumps the data-processing capabilities of the control center and the aggregator into a component residing at each aggregator. The aggregators are further assumed to be identical, and so one more parameter is added to the model: the data rate R of the communication and control system.

This brings the total number of free parameters to three: K, Δf, and R. The purpose of the model is to determine, for a given electrical network, how these parameters affect the magnitude of the load reduction and frequency at the generators in response to a significant loss of supply. The electrical components of the system are modeled in a generally standard fashion; the details of the generators and transmission lines are described next. These descriptions are brief, highlighting only the necessary mathematical elements. Excellent overviews of the models and underlying theory can be found in textbooks by Nilsson [97] (for sinusoidal steady-state analysis), Glover et al. [52], and Arrillaga and Watson [6].

## 6.2.1 Generation

The generators are modeled as synchronous machines having six state variables: the deviation of the frequency from nominal, the phase angle, the excitation voltage, the mechanical power that drives the machine, the mechanical power control signal, and the status of the frequency protection breaker.¹ The model has one input variable and one output variable, and these govern its interaction with the transmission system.

The input variable is the voltage where the machine connects to the transmission network. The output variable is the current it injects into the network at the same point. Figure 6.11 illustrates the state variables with respect to the physical machine that they model. The model has 10 parameters; these are listed in Table 6.1.

The angular speed of the turbine, ω, is in radians per second; its frequency (in hertz) is

\[
f = (2\pi)^{-1}\omega
\tag{6.4}
\]

The synchronous reactance X_d is a complex impedance, and the terminal voltage V and excitation voltage E are phasors.² The state trajectory of the generator is

![](img/df6085a1b35edf9c9ea818a5c66ccad9_269_0.png)

**FIGURE 6.11** State variables in the synchronous machine model.

described by the equations

$E = E_f \angle \theta$  (internal machine voltage)  (6.5)

$I = \frac{E - V}{X_d}$  (current flow out of the machine)  (6.6)

$P_e = \Re\{VI^*\}$  (real electrical demand)  (6.7)

$\dot{\omega} = \frac{P_m - P_e}{M}$  (angular acceleration)  (6.8)

$\dot{\theta} = \omega$  (changing phase angle)  (6.9)

$\dot{c} = -T_1(c + R\omega + A_g\theta)$  (speed and phase angle control)  (6.10)

$\dot{P}_m = T_2(c - P_m + P_s)$  (mechanical power adjustment)  (6.11)

**TABLE 6.1  Synchronous Machine Parameters**

| Parameter | Definition |
|---|---|
| $T_1, T_2$ | Time constants of the speed controller |
| $T_e$ | Time constant of the excitation controller |
| $E_f$ | Maximum excitation voltage |
| $M$ | Angular momentum |
| $R$ | Gain for the droop control |
| $A_g$ | Gain of the area generation controller |
| $f_r$ | Frequency deviation tolerance (in hertz) |
| $X_d$ | Synchronous reactance |
| $P_s$ | Output power setpoint |

$$E_f=\begin{cases}0,&\text{if }E_f\ge E_{\mathrm{lim}}\land |V|<1\\\dfrac{1-|V|}{T_e},&\text{otherwise}\end{cases}\qquad\text{(excitation control)}\tag{6.12}$$

$$\text{Breaker status}\leftarrow\begin{cases}\text{closed},&\text{if breaker status = closed}\land |f|<f_t\\\text{open},&\text{otherwise}\end{cases}\qquad\text{(breaker logic)}\tag{6.13}$$

The generator output variable is

$$I_{\mathrm{inj}}=\frac{E}{X_d}\tag{6.14}$$

## 6.2.2 Transmission Network and Electrical Loads

The transmission network connects generators and loads. It is modeled with an admittance matrix $Y$, which is obtained by sinusoidal steady-state analysis. Every load attached to the network is represented by a Norton equivalent circuit: it has an injected current in parallel with an admittance. Passive loads inject no current, and active loads may have a negative or positive injected current. Generators are modeled in the same way, with an injected current calculated by Equation 6.14 and admittance $y$ that is the inverse of the machine’s synchronous reactance (i.e., $y=1/X_d$; see Table 6.1).

Figure 6.12 illustrates the main parts of a model that has generation, load, and transmission. The one line diagram of the two load, two line, single generator system

![](img/df6085a1b35edf9c9ea818a5c66ccad9_270_0.png)

**FIGURE 6.12**  Circuit diagram and one line drawing of a small power system.

is shown next to its equivalent circuit model. The node voltages and branch currents labeled in the figure are related directly to the input and output variables of the generators, which are described in Section 6.2.1. Specifically, the node voltage $V$ appears in Equations 6.6, 6.7, and 6.12; the generator output current $I$ is derived from its Thevenin equivalent circuit, and the electrical power demand is the product of the output current $I$ and terminal voltage $V$.

Given the network admittance matrix $Y$, the load and machine admittances $y_1, \ldots, y_n$, and the injected current vector $\bar{I}_{\mathrm{inj}}$, we calculate the voltages $V_1, \ldots, V_n$ appearing at the terminals of loads and generators by

$$\left(Y + \operatorname{diag}(y_1\ y_2\ \ldots\ y_n)\right)^{-1}\bar{I}_{\mathrm{inj}} = [V_1\ V_2\ \ldots\ V_n]^T$$

This formula is illustrated below using the vectors and matrices for the power system shown in Figure 6.12:

$$\left(\begin{bmatrix} Y_{2g}+y_{1g} & -y_{1g} & -y_{2g} \\ -y_{1g} & y_{1g} & 0 \\ -y_{2g} & 0 & y_{2g} \end{bmatrix} + \begin{bmatrix} 1/X_d & 0 & 0 \\ 0 & 1/y_1 & 0 \\ 0 & 0 & 1/y_2 \end{bmatrix}\right)^{-1}\begin{bmatrix} I_{\mathrm{inj}} \\ I_1 \\ I_2 \end{bmatrix} = \begin{bmatrix} V \\ V_1 \\ V_2 \end{bmatrix}$$

If a breaker at a generator opens, then the admittance for that generator is zero (i.e., $X_d = \infty$) and $I_{\mathrm{inj}}$ is zero. This disconnects the generator from the transmission network. Changes in load are modeled as discrete events that change the load admittance, load current, or both.

## 6.2.3 Frequency Monitoring and Load Actuation

A generator reports its frequency to the control center at threshold values $k\,\Delta f$, $k \in \mathbb{Z}$; these thresholds are described by event surfaces at $f-k\Delta f=0$. Reports from the generator are processed at the control center, which keeps the most recent report from each generator. On processing a report, the control center calculates a percentage adjustment for the load and, if the new adjustment differs from the previous one, it tells the loads to change their demands accordingly. The percentage adjustment $\alpha$ is limited to $\pm 30\%$, but within this range is calculated by multiplying the average of the reported frequencies by the control parameter $K$; in other words, if $N$ generators are connected to the network, the requested adjustment is

$$\alpha = \frac{K}{N}\sum_{j=1}^{N} f_j \tag{6.15}$$

where the $f_j$ is the frequency most recently reported by the $j$th generator. The new $\alpha$ is then placed into a queue for processing at each load. The loads make adjustments relative to their base demand $L$ to achieve an actual demand $(1+\alpha)L$. The transmission network closes the control loop; the diagonal elements in $Y$ change
