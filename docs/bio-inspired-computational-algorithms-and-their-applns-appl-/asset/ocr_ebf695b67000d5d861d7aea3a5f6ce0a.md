The choice of pump tanks material plays an important role, as its mass density and stress coefficients are the main keys in the pump design. The main tank pressure (about 300 kPa) and the area of the inlet valves set up the limits for the maximum inflow rate. If the inflow velocity is increased this can cause the propellant to be aerated, what is not desirable for the proper working of the engine. The extra volume of pressurized gas in the pump chamber should be small to minimize gas usage, but if it is too small, there will be a loss of propellant through the vent.

The primary parameters for the calculations are the state changing cycle, t_cy the volume flow determined by the rocket engine needs, Q, the specific impulse of the propellants, I_sp, at the fuel pressure, p_f, the fuel mass density, ρ_f, the thrust, T, and the material properties: the mass density, ρ_c, and stress coefficient, σ_c. From these parameters, considering the pump chambers are spherical, one can instantly obtain the diameter of one chamber:

D_c = sqrt(6 * ∫_0^{t_cy} Q dt / π) , (4)

where the integral results in the chamber volume, and for the simplest case of steady flow, it resumes to V_c = Q t_cy. Knowing the diameter and applying the stress formulae from Young (1989), the chamber walls thickness can be obtained by

t_w = p_f D_c / σ_c , (5)

and the total chamber mass by

M_c = π t_w D_c^2 ρ_c . (6)

To obtain the thrust, one can apply the momentum equation for the case of ideal expansion, and:

T = g Q I_sp ρ_f , (7)

where g represents the gravity acceleration.

Manipulation of these expressions and an estimative of the relative weight of the valves and other accessories lead to expression 7 from Harrington (2003), the pump thrust to weight ratio:

T/W = 0.43 g I_sp ρ_f σ_c / (p_f t_cy ρ_c) , (8)

that is to be optimized. The total pump mass is M_p =1.56 M_c, and the mass flow can be easily obtained by m_dot = Q ρ_f . The expressions (4)-(8) were coded in a program to test the feasibility of this set of equations as a model. Table 3 presents the results obtained for typical parameter values. These results are in agreement with rocket engine pump literature (Griffin and French 1991; Sutton 1986).