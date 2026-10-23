
One further simplification for analysis is obtained by Eq. (15) from Eq. (14).

h(x) ≜ x + f(x)  
= m1 x + 1/2 (m0 − m1)(|x + 1| − |x − 1|)   (15)

Hence m0 = a + 1, m1 = b + 1. Thus the dimensionless form that will be used for a rigorous proof of chaos is given by Eqs. (16) through (19).

ẋ = α(y − h(x))      (16)  
ẏ = x − y + z        (17)  
ż = −β y            (18)  
h(x) = m1 x + 1/2 (m0 − m1)(|x + 1| − |x − 1|)      (19)

We will interchangeably use the words “Chua’s circuit” and “Chua’s system” to refer to Eqs. (16) through (19) from now on. From the parameter values in Fig. 6 we obtain {α, β, m0, m1} = {9, 14 2/7, −1/7, 2/7} [4]. The classic Double-Scroll Chua’s attractor obtained with these parameter values is shown in Fig. 7.

![](img/039e7d3c23390584a66737067db8b75b_340_0.png)

Fig. 7. The Double-Scroll Chua’s attractor. Recall that Chua’s circuit has three equilibrium points: P+, 0, P−. It turns out that the chaotic trajectory “wraps around” one of the outer equilibrium points, P+ or P−, and then moves through the equilibrium point at the origin, to the other equilibrium point.

A useful quantity (or measure) for a chaotic attractor is the dimension. We are familiar with the concept of a dimension for everyday objects: a solid sphere is three dimensional, the surface of a sphere is two dimensional etc. In the case of chaotic attractors, many definitions of dimension exist, we will examine the Lyapunov dimension [12]. We can actually predict the range of the Lyapunov dimension without any computation. Figure 7 seems to imply that the chaotic attractor is three dimensional. However this attractor is not a solid object, it is more a “sheet-like” structure. So, is the dimension less than two? The answer is no because of the Poincaré-Bendixson theorem. Can the dimension be greater than three? The answer again is no because the system of equations for Chua’s circuit is three dimensional. Thus intuitively the Lyapunov dimension of the Double-Scroll must be between two and three. It turns out that the Lyapunov dimension of the Double-Scroll is approximately 2.13 [12].

We conclude this section by discussing a subtle but very important concept that is often misunderstood: Chua’s circuit is not an analog computer.

### 2.1. Analog computer emulation of an ODE is not a physical circuit

A common misconception is to equate an “analog computer” emulation of a system of ODEs to a physical circuit. The reasoning employed is that analog computers are made of physical circuit elements like op-amps, resistors, capacitors and inductors. However, this reasoning can be understood as erroneous by considering this fact: digital computers are also made of circuit elements. Yet no one calls a digital computer emulation of a system of ODEs as a physical circuit!

The importance of this concept can be further understood by considering the mass-damper-spring system in Fig. 8 and the two circuit realizations shown. One is the analog computer emulation and the other is the LRC realization.

![](img/039e7d3c23390584a66737067db8b75b_341_0.png)

Fig. 8. The mass-damper-spring mechanical system and two electrical circuit versions. The voltages across the capacitors in the op-amp circuit correspond to the internal states of the mechanical system. However the analog computer version is an emulator whereas the LRC circuit is the actual physical electrical equivalent. Note that in deriving the analog computer, all mechanical parameters were assumed to have magnitude one. Moreover the analog circuit model actually requires one more inverting amplifier for producing x from −x.

It should be immediately apparent that the analog computer is simply a “signal flow” graph and cannot account for physical characteristics of the mass-damper-spring. For instance, the position and velocity of the mass are simply represented by the voltages across the two capacitors. Also, the transfer of energy between the mass and spring cannot be interpreted from the analog computer. This is because energy requires us to have the product of force waveform and the velocity waveform.^c^ This is unavailable in the analog computer emulation.^d^

In contrast, the LRC circuit is the true electrical analog of the mass-damper-spring. This is easily seen by simply comparing the differential equations. For the mass-damper-spring, we have Eq. (20).

M x¨ + D x˙ + K x = 0   (20)

For the LRC circuit, we have Eq. (21)

L_p q¨ + R_p q˙ + (1/C_p) q = 0   (21)

c. Scalar product of force and velocity gives instantaneous power. Time integral of instantaneous power gives work done or energy.

d. Although the potential energy of the spring is analogous to the energy stored in the second capacitor and the kinetic energy of the mass is analogous to the energy stored in the first capacitor, this is not readily apparent.

Comparing Eqs. (20) and (21), we can see that the mass has a one-to-one correspondence to the inductor, the dampener corresponds to the resistor and the spring corresponds to 1/C_p. Also note that the position is analogous to charge and velocity to current. Thus the LRC circuit is the electrical physical realization of the mass-damper-spring system.

By the same argument as above, Chua’s circuit in Fig. 6 is not an analog computer model but a physical realization of Eqs. (16) through (18). The fact that Chua’s circuit is a physical realization enables us to study interesting phenomenon such as local activity, that is essential [7] for chaos.

In concluding this section, note that the op-amp circuit is an “analog computer” simulation of the mechanical system, where the word “analog” is used, by tradition, to mean “continuous time” or “not digital”. This should not be interpreted as an “analogy” of the mechanical mass-damper-spring system. Indeed, the word “analog computer” is just a non-technical jargon to mean any systematic collection of basic components, such as op amps, integrators, resistors, inductors, capacitors, etc., packed inside a compact cabinet, with externally accessible switches, and other extra features to allow one to quickly interconnect a continuous-time circuit such that its state equation is the desired one. One can also observe the time evolution of the state variable dynamics via an oscilloscope, in real time. In this sense, the op amp circuit in Fig. 8 for simulating the mass-damper-spring mechanical system is just a “poor man’s analog computer”, tailored to simulate the state equations of only one physical system.

## 3. The Need for a Rigorous Proof of Chaos

In the previous section, we examined the classic parameter values in Chua’s circuit for obtaining Chua’s attractor. If we can realize Chua’s circuit and confirm chaos, why do we still need a rigorous proof? The answer is computer simulations have finite precision and experimental measurements have finite range for time or frequency. As a simple example, reconsider Chua’s circuit with the parameter values {α, β, m₀, m₁} = {10.75, 14 2/7, −1/7, 2/7}. Note that we only changed the α value. A simulation of the system for four time intervals is shown in Fig. 9.

![](img/039e7d3c23390584a66737067db8b75b_342_0.png)

**Fig. 9.** Trajectory of Chua’s circuit with α = 10.75 for (a): t = 30 units, (b) t = 35 units, (c) t = 45 units and (d) t = 70 units. Notice how in each case the dimensions of our axes are increasing. The transient attractor is not even visible in (d). In other words Chua’s circuit is unstable for this choice of parameter values. In the physical circuit we will quickly observe a large amplitude limit cycle due to amplifier saturation.

It is clear from Fig. 9 that we are observing chaos as a transient. If one were to consider only the first 30 time units, we would incorrectly conclude the system was exhibiting chaotic behavior. To address this issue a rigorous proof of chaos is necessary. We will now outline the approach for a rigorous proof of chaos in Chua’s attractor.

### 3.1. Piecewise-linear analysis of Chua’s circuit

The method employed in [4] was the very first rigorous proof of chaos in any physical, and not hypothetical, dynamical system. The essence of this approach is Shilnikov’s theorem.

**Theorem 1.** *Let ξ be a continuous piecewise-linear vector field associated with a third-order autonomous system* **ẋ = f(x), x ∈ ℝ³.** *Assume the*
