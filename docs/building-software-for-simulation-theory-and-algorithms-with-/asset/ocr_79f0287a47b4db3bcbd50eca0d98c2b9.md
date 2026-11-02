A useful fact is that if the trajectories are decomposable into generator segments, then a homomorphism constructed on that set of generators implies a homomorphism of the complete system (see, e.g., Ref. 157). The primitive segments for discrete-time and discrete-event systems satisfy this requirement. For instance, every trajectory of a discrete-time system can be constructed by concatenating trajectories of unit length. Hence, these constitute generators for the system. The functions $h$ and $g$ can now be applied to the single-step transition function $\delta$ as follows, where $x'$ is now a generator segment:

$h(\delta(q,g(r')))=\delta'(h(q),r')$ \hfill (C.3)

Equation C.3 implies Equation C.1 and is often a more practicable tool for constructing homomorphisms.

# C.2  SINUSOIDAL STATE-STEADY ANALYSIS

Changes in the speed, output power, and excitation voltage of an electric generator occur much more slowly than do the changes in voltages and currents in transmission wires, capacitor banks, and other electrical equipment. It is therefore convenient in the analysis of generator dynamics to avoid dynamic models of purely electrical devices and use instead simpler algebraic models. For this purpose, it is assumed that these devices always see a sinusoidal voltage and current characterized by $A\sin(\omega t+\theta)$. The amplitude $A$ and phase angle $\theta$ may vary with time, but the frequency $\omega$ is fixed. Justification for these assumptions can be found in almost any textbook on power systems engineering or the analysis of electric circuits (see, e.g., Ref. 52 or 97). This assumption simplifies the calculation of currents and voltages in the transmission network by considering only instantaneous changes in amplitudes and phase angles. We proceed as follows:

+   1. Each sinusoidal source is replaced by a *phasor* $A\cos\theta + jA\sin\theta$. With a slight abuse of notation, this is abbreviated $A\angle\theta^1$.
+   2. Inductors $L$, resistors $R$, and capacitors $C$ are replaced with complex impedances $j\omega L$, $(j\omega C)^{-1}$, and $R$, respectively. This produces a network containing only complex impedances $Z$ that satisfy Ohm’s law when the currents $I$ and voltages $V$ are phasors: $V=IZ$. The complex power at a device is $S=VI^*$. The real part of $S$ is called *real power* and the imaginary part, *reactive power*.
+   3. Voltages at nodes and currents in branches are calculated using the mesh current or node voltage method.

$^1$In fact, $A\angle\theta=A\cos(\omega t+\theta)$ and $A\cos\theta+jA\sin\theta$ is the phasor transform of that sinusoid. In most cases, the use of $A\angle\theta$ for the phasor does not cause confusion.