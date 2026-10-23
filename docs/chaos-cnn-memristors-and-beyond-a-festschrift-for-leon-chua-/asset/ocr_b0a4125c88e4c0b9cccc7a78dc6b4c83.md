![](bbox=[0.13, 0.07, 0.42, 0.22])

the resulting system has an attractive fixed point Q_FP = 0 for V_S(t) ≡ 0. Thus, for sufficiently small Q(0), the circuit with Q_C(t) = Q(t) and no excitation has unique asymptotic behavior. We assume that is true for the excited circuit. Consequently, we disregard the transient response, and calculate the steady state current only. (However, if Q(0) − Q_C(0) was nonzero, Q(t) would follow Q_C(t) with a constant offset, i.e. it would act as a “shadow state”. The analysis of the system therefore would be slightly different.)

# First order circuit:

First, the circuit elements in the above mentioned circuit have to be replaced by their individual first order models, which can be taken from Table 1. The resulting first order circuit is shown in Fig. 7.

As the first order circuit is linear, the first order current I1(t) can be determined directly. For a sinusoidal excitation V_S(t) with the angular frequency ω0, the current I1(t) = Î1,ω0 cos(ω0t + φI1,ω0) must be sinusoidal, too. Employing the transfer function G1(jω) = I1/V_S = 1/(M0 − j 1/(ωC)),

the amplitude Î1,ω0 and the phase φI1,ω0 of the first order current follow as Î1,ω0 = V̂S |G1(jω0)| = V̂S / sqrt(M0² + (1/(ω0C))²) and φI1,ω0 = φVS + arg G1(jω0) = φVS + arctan 1/(ω0 M0 C).

Integrating I1(t) with respect to time, we get Q1(t) = (Î1,ω0 / ω0) cos( ω0t + φI1,ω0 − π/2 ).

# Second order circuit:

The second order circuit contains a new independent voltage source, which is a part of the memristor model. (Fig. 8.) The voltage V_E2(t) of this source has to be determined by using the results for the first order circuit.

![](bbox=[0.58, 0.07, 0.88, 0.25])

With the abbreviation A = ω0t + φI1,ω0, V_E2(t) can be written as V_E2(t) = M1 Q1(t) I1(t) = M1 Î1,ω0²/ω0 cos(A) cos(A − π/2) = (M1 Î1,ω0²)/(2ω0) [ cos(2A − π/2) + cos π/2 ] = V̂_E2,2ω0 cos(2ω0t + φV_E2,2ω0).

The sole excitation of the second order circuit therefore is a sinusoidal voltage with the angular frequency 2ω0, and the amplitude/phase V̂_E2,2ω0 = (M1 Î1,ω0²)/(2ω0); φV_E2,2ω0 = 2 φI1,ω0 − π/2.

Again, a transfer function G2(jω) = −G1(jω) is used to calculate the current I2(t). The amplitude of the second order current is Î2,2ω0 = V̂_E2,2ω0 / sqrt(M0² + (1/(2ω0 C))²); and it has a phase of φI2,2ω0 = φV_E2,2ω0 + arctan 1/(2ω0 M0 C) + π.

Q2(t) can be obtained by integrating I2(t).

# Third order circuit:

The only difference between the second and the third order circuit is the time dependent voltage source that belongs to the memristor model. Both V_E3(t) and I3(t) can be written as the sum of two sinusoidal components with the angular frequencies ω0 and 3ω0 respectively.

# Results:

To get an approximation of the current I(t) in the original circuit, we just add the current