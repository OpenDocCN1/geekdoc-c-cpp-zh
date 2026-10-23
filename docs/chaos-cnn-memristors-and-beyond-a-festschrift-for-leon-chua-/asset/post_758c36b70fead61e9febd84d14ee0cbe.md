
(a) B = 0.18: quasi-periodic regime

(b) B = 0.15: metastable toroidal chaos

Fig. 8. (a) Quasi-periodic regime and (b) metastable toroidal chaos solution to the piecewise-linear van der Pol equation (7). Parameter values: ε = 0.1825, ω = 1, R = 1, and x₀ = 1.

capacitor driven by a sinusoidal voltage source (Fig. 9) was investigated by Matsumoto, Chua and Tanaka [49]. A detailed study of the bifurcation diagram was then completed in a slightly different R-L-diode circuit [Fig. 9(b)] [50]. A two-dimensional map was proposed to reproduce “all essential features of the experimentally observed bifurcation phenomena.”

In the R-L circuit as well in the two-dimensional map [50]

```
⎧ xₙ₊₁ = yₙ − 1 + | +α₁ xₙ   if xₙ ≥ 0
                  | −α₂ xₙ   if xₙ < 0
⎨
⎩ yₙ₊₁ = b xₙ,   (9)
```

they observed that the ultimate scenario consists of three kinds of bifurcation: (i) saddle-node

![](img/039e7d3c23390584a66737067db8b75b_232_0.png)

![](img/039e7d3c23390584a66737067db8b75b_232_1.png)

(a) With a nonlinear capacitor

(b) With a diode 3CC13

Fig. 9. Two simple nonautonomous circuits producing chaotic regimes, one with a nonlinear capacitor (a) as studied in Ref. [49], and one with a diode 3CC13 (b) as investigated in Ref. [50].

![](img/039e7d3c23390584a66737067db8b75b_232_2.png)

Fig. 10. Bifurcation diagram of the two-dimensional map (9) for reproducing the essential feature of the simplest nonautonomous chaotic electronic circuit. Parameter values: b = −0.13 and α₁ = 0.7.

bifurcations, (ii) period-doubling cascades, and (iii) crisis. Using b = −0.13, and α₁ = 0.7, a bifurcation diagram similar to the one observed in the experimental R-L-diode circuit was obtained (Fig. 10).

## 2.5. Devil staircase in an experimental van der Pol-like circuit

With Michael Kennedy, Chua examined a simple experimental circuit with a negative resistance

device, as presented by van der Pol and van der Mark [51], which displays a transition to chaos through an alternating periodic-chaotic sequence, and described a nonlinear circuit model of the physical circuit which faithfully reproduces the observed period-adding phenomenon [52]. Van der Pol and van der Mark described an experiment in which by tuning the capacitor in a neon bulb R-C relaxation oscillator, driven by a sinusoidal voltage source, currents and voltages appear in the system which are whole submultiples of the driving frequency. To reproduce this, Kennedy and Chua considered a sinusoidally-driven neon bulb relaxation oscillator (Fig. 11). A high-voltage dc supply E ≈ 100-V with large source resistance R ≈ 1 MΩ was attached to a shunt connection of neon bulb and capacitor C, forming the basic relaxation oscillator. In series with the neon bulb was inserted a sinusoidal voltage source E₀ sin ωt (a small current sense resistor Rₛ, was also inserted in series with the neon bulb to detect the current flowing in it).

The natural frequency of the undriven oscillator was set to 1 kHz by tuning capacitance C to C₀. Then a sinusoidal signal E₀ sin ωt was applied as shown in Fig. 11. The resulting frequency of the voltage pulses measured across R, was recorded as the value of the bifurcation parameter C was brought gradually from C₀, to a much larger value. As the capacitance is increased, the system at first continues to oscillate at 1 kHz over a wide range of C, until the frequency suddenly drops to 1000/2 Hz, to maintain that value over a further range of capacitance. If C is increased still more, the frequency drops to 1000/3 Hz, then 1000/4 Hz, 1000/5 Hz,

![](img/039e7d3c23390584a66737067db8b75b_232_3.png)

Fig. 11. Sinusoidally-driven neon bulb relaxation oscillator as investigated by Kennedy and Chua [52].

![](img/039e7d3c23390584a66737067db8b75b_233_0.png)

Fig. 12. Frequency of the oscillations produced by the sinusoidally-driven neon bulb oscillator investigated by Kennedy and Chua [52], and showing coarse staircase structure as observed by van der Pol and van der Mark [51].

and so on up to 1000/20 Hz (Fig. 12), exactly as reported by van der Pol and van der Mark in 1927 [51]. Such type of investigations was extended to other simple electronic circuits [53].

## 3. The Chua Circuit

### 3.1. Discovery

The first simple autonomous circuit with a chaotic attractor was proposed during a stay of Chua at Waseda University (Tokyo) from October 1983 to January 1984. Chua visited Takashi Matsumoto with whom he already published few papers

[28,54,55]. As Chua wrote himself [56], Matsumoto was trying to perform an electronic circuit realization of the Lorenz equations. But, as Rössler failed in his trials to perform a chemical reaction with a Lorenz dynamics, Matsumoto failed in his attempt to design an electronic “Lorenz” circuit. In fact, a design for an electronic circuit which models the Lorenz equations was only proposed by F. N. H. Robinson in 1990 [57]. With the know-how Chua had in the use of piecewise-linear electronic elements, Chua quickly suggested a new circuit with a piecewise-linear resistor (Fig. 13). Chua was convinced that the use of a piecewise-linear function is convenient for realizing electronic circuits producing rich dynamics as well as facilitating analysis and programming. This is true for designing circuits, true for some type of analysis but has no deep consequence for computing. Very quickly, Matsumoto was able to produce a double-scroll attractor by using numerical integrations. Thus, the double-scroll attractor was observed in this electronic circuit on October 1983 [58], that is, at the beginning of Chua’s stay at Waseda University.

But they apparently preferred to first complete the paper about the simplest non autonomous circuit [49] which was submitted on March 28, 1984. Then, Matsumoto sent a paper by fax to Chua who was back at the University of California at Berkeley. This paper was written by Matsumoto alone and was entitled “A chaotic attractor from Chua’s circuit”. This fax is dated on April 17, 1984 in Ref. [59] where it is quoted as a memorandum [60]. With Chua’s agreement, Matsumoto submitted his paper on April 20, 1984 [61]. In this paper, Matsumoto presented himself the circuit consisting of “only one nonlinear element; a 3-segment R piecewise-linear

![](img/039e7d3c23390584a66737067db8b75b_233_1.png)

(a) Simplified Chua circuit

![](img/039e7d3c23390584a66737067db8b75b_233_2.png)

(b) Characteristic of the nonlinear resistor

Fig. 13. Circuit with a nonlinear resistor proposed by Chua and simplified by Matsumoto.

resistor. It is a simplified version of a circuit suggested by Leon Chua.” This was made without explicit reference to the original circuit. Matsumoto designated himself the circuit by Chua’s name as seen from the title of the paper. The circuit investigated is described by the set of equations:

```
\begin{cases}
C_1 \dot V_{C_1} = G(V_{C_2} - V_{C_1}) - g(V_{C_1}) \\
C_2 \dot V_{C_2} = G(V_{C_1} - V_{C_2}) + I_L \\
\dot I_L = -V_{C_2}
\end{cases} \tag{10}
```

where $V_{C_1}$, $V_{C_2}$ and $I_L$ denote voltage across $C_1$, voltage across $C_2$, and current through $L$, respectively. Using notations adopted later [58], the piecewise-linear characteristics reads as:

```
g(V_{C_1}) = m_0 V_{C_1} + \frac{1}{2}(m_1 - m_0)|V_{C_1} + B_p| \\
\qquad + \frac{1}{2}(m_0 - m_1)|V_{C_1} - B_p| \tag{11}
```

where $m_0 = -0.1$, $m_1 = -4$ and $B_p = 1$. From his numerical computations (Fig. 14), Matsumoto emphasized the role of phase portrait. He found the attractor structure different from the structure of the attractors solution to the Lorenz and Rössler equations, respectively. He wrote:

> “The origin of the Lorenz equations [...] is a saddle, i.e. all eigenvalues are real. Another

difference is that (10) is symmetric with respect to the origin while the Lorenz equation is symmetric with respect to the $z$-axis. It is known that the Rössler attractor [62] does not contain any equilibrium. Hence, it is different from ours.”

This claim was only supported by a fixed point analysis — and one wrong statement about the Rössler system — and some considerations about the symmetry inherent to the different systems.

With Chua’s help (as it appeared in references quoted by Ref. [59]) and stimulated by Mastumoto’s fax, F. Ayrom (University of California at Berkeley and, consequently, one of Chua’s colleague) and one of his collaborator, Guo-Qun Zhong (Academia Sinica, Guangzhou, People’s Republic of China), designed an electronic circuit with a 5-segment odd-symmetric $V$-$I$ characteristic. It thus appears that the simplification mentioned by Matsumoto was to reduce the characteristic curve to three branches since the three central branches of the original characteristic can easily be approximated by a single branch as done by Matsumoto. The two-scroll chaotic attractor was thus observed by Zhong and Ayrom in a real electronic circuit. Their paper was submitted on July 20, 1984 and published in 1985, once Matsumoto’s paper was published (December 1984). Note that the first chaotic

![](img/039e7d3c23390584a66737067db8b75b_234_0.png)

(a) $V_{C_1}$-$I_L$ plane projection

![](img/039e7d3c23390584a66737067db8b75b_234_1.png)

(b) $V_{C_1}$-$V_{C_2}$ plane projection

Fig. 14. Two-scroll chaotic attractor obtained by Matsumoto using a numerical integration. Parameter values: $G = 0.7$, $C_1 = 1/10$, $C_2 = 1/0.5$, $m_0 = -0.1$, $m_1 = -4$, $B_p = 1$ and $L = 1/7$.
