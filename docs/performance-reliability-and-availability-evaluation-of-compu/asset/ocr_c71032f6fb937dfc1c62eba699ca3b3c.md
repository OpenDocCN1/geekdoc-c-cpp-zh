# Performance, Reliability, and Availability of Computational Systems

Negating both sides, we get

$\Psi(B) = ((\overline{hw_1} \vee \overline{os_1}) \wedge (\overline{a_1} \wedge \overline{b_1})) \wedge (\overline{hw_2} \vee \overline{os_2}) \wedge (\overline{a_2} \wedge \overline{b_2})) \vee \overline{nw}$.$

The structure-function can be obtained by applying the transformation rules depicted in Table 18.3.

$\Phi(X) = (1 - x_{hw1} \times x_{os1}) \times (1 - x_{a1}) \times (1 - x_{b1})) \times$

$(1 - x_{hw2} \times x_{os2} \times (1 - x_{a2}) \times (1 - x_{b2})) \times x_{nw})$,

where $x_i$ is the respective structure variable and $X = (x_{hw1}, x_{os1}, x_{a1}, x_{b1}, x_{hw2}, x_{os2}, x_{a2}, x_{b2}, x_{nw})$ is the structure vector.

Considering the structure variables are independent, $R_i(t) = E(x_i)$, the system reliability

$R(t) = (1 - (1 - R_{hw1}(t) \times R_{os1}(t)) \times (1 - R_{a1}(t)) \times (1 - R_{b1}(t))) \times$

$(1 - R_{hw2}(t) \times R_{os2}(t) \times (1 - R_{a2}(t)) \times (1 - R_{b2}(t))) \times R_{nw}(t)$.

Similarly, the steady-state availability is obtained.

$A = (1 - (1 - A_{hw1} \times A_{os1}) \times (1 - A_{a1}) \times (1 - A_{b1}))$

$(1 - A_{hw2} \times A_{os2} \times (1 - A_{a2} \times (1 - A_{b2}))) \times A_{nw}$.

Consider the time to failure of each component $i$ is exponentially distributed with the respective rate $\lambda_i$, and assume the rates $\lambda_{hw1} = \lambda_{hw2} = 2.5 \times 10^{-5} f/h$, $\lambda_{os1} = \lambda_{os2} = 2.5 \times 10^{-4} f/h$, $\lambda_{a2} = 6.7 \times 10^{-4} f/h$, $\lambda_{b1} = 7.69 \times 10^{-4} f/h$, and $\lambda_{nw} = 2.2 \times 10^{-5} f/h$. The reliability in the interval (0,400h) is shown in Figure 19.13. The defects per million in 1000h is $DPM = (1 - R(1000h)) \times 10^6 = (1 - 0.21026) \times 10^6 = 789474.0$. Let us assume the time to repair of each component $i$ is exponentially distributed with the respective rate $\mu_i$. If the rates are $\mu_{hw1} = \mu_{hw2} = 2.5 \times 10^{-2} r/h$, $\mu_{os1} = \mu_{os2} = 0.25r/h$, $\mu_{a1} = \mu_{a2} = 1r/h$, $\mu_{b1} = \mu_{b2} = 0.667r/h$, and $\mu_{nw} = 0.25r/h$, the steady-state availability is $A = 0.999907$.

The reliability (Birnbaum) importance of each system component is obtained deriving reliability function by the reliability of each component.