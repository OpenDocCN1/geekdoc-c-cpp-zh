$$ Q = \iint_{A(s)} v_i \, dA . \qquad (20) $$

Then, the absolute positive head can be obtained by

$$ H_a = H_i + H_e - H_f \qquad (21) $$

and the net positive suction head or available suction head above vapor pressure can be obtained by

$$ H_s = H_i + H_e - H_f - H_v \qquad (22) $$

where $H_v$ is the combustible vapor pressure. The required suction head will be taken as 80% of the available suction head in order to provide a margin of safety for cavitation, or $H_{SR}=0.8H_v$. To avoid pump cavitation, $H_i$ has to be higher than $H_{SR}$. If additional head is required by the pump, the propellant may have to be pressurized by external means, such as by the addition of another pump in series (a booster pump) or by gas pressurization of the propellant tanks. A small value of $H_{SR}$ is desirable because it may permit a reduction of the requirements for tank pressurization and, therefore, a lower inert tank mass.

The shaft speed is given by

$$ N_{rpm} = \frac{S H_e^\phi}{u_{si}\sqrt{Q}} \qquad (22) $$

where $φ=3/4$ and $u_{si}=17.827459$ are constants. $u_{si}$ is necessary due to SI conversions (see Sutton & Biblarz 2001, eq. 10-7). This last expression allows us to obtain $N_{rpm}$, the shaft speed in radians per second.

The impeller vane tip speed is given by

$$ u_1 = \frac{1}{2} d_2 N_{rad/s} . \qquad (23) $$

With $u_1$ we can evaluate the head delivered by the pump

$$ \Delta H = \frac{u_1^2}{\psi g_0} , \qquad (24) $$

where $ψ$ has values between 0.90 and 1.10 for different designs. As for many pumps, $ψ=1.0$, we adopt this value.

At this point, we are able to obtain all the final results, Γ = {m_dot, P_1, P_2}:

$$ P_1 = H_1 g_0 \rho , \qquad (25) $$

$$ P_2 = (\Delta H + H_1) g_0 \rho , \qquad (26) $$

and

$$ \dot{m} = \rho Q . \qquad (27) $$