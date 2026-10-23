
like a nonlinear resistor with memory. By considering the three classical circuit elements, the capacitor, the resistor, the inductor and the “relationships” linking the variables involved, respectively: “Volta’s law” q = C v (Eq. (1)), “Ohm’s law” v = R i (Eq. (2)) and “Faraday’s law” φ = L i (Eq. (3)), he deduced, for the sake of completeness, that only one “relationship”, i.e. only one law, remained undefined.

## 4.1. Theoretical imperfections

The philosopher of sciences Dudley [34] distinguished three kinds of scientific problems, first, problems related to scientific domain concerning for example the clarification and extension of the field, then the theoretical problems that require that one accounts, in a more profound manner, for a certain theory of the domain, and finally the theoretical imperfections. These, arise eventually when the theory was developed in response to a given theoretical problem. The theory can be revealed as incomplete with respect to the considered domain, be a simplification, or cause problems that Shapere called incompleteness of the black box. In fact, these three types of theoretical imperfections are distinguished from each other starting from the domain considered by the theory and the observed correspondence between theory and reality. Thus, if we consider a scientific domain as a whole corpus of information that a theory must account, we can say that a theory can be revealed as incomplete with respect to the considered domain if, on one hand there is no reason to suppose that the theory is not fundamentally correct and, on the other hand there is no reason to suppose that this theory can not be completed so that it can account for an unexplained part of the corpus.

Following this idea of completeness, [6] postulated the existence of a fourth circuit element in addition to the three others that he called it memristor. Then, he established the “relationship” between the magnetic flux φ and the charge q:

```
φ = M q
(6)
```

We suggest to call this relationship: Chua’s law. At that time, he also proposed a symbol (see Fig. 10).

## 4.2. Memristor DC characteristics

In order to emphasize a strong analogy between the memristor properties and that of the singing arc let’s focus on the interesting properties 3-5

![](img/039e7d3c23390584a66737067db8b75b_515_0.png)

Fig. 10. The four fundamental two-terminal circuit elements, [36, p. 80].

established by Prof. Chua in his second publication on this subject [7, p. 211 and next].
Let’s begin with the:

> “Property 3-DC Characteristics
> A time-invariant current-controlled memristive one-port under dc operation is equivalent to a time-invariant current-controlled nonlinear resistor if f(x, I) = 0 has a unique solution x = X(I) such that for each value of I ∈ ℝ, the equilibrium point x = X(I) is globally asymptotically stable.”

[7, p. 211] then observed that a time invariant memristive one-port under dc operation behaves just like a nonlinear resistor and took as an example the dc characteristics of a short neon tube (Fig. 11).

![](img/039e7d3c23390584a66737067db8b75b_515_1.png)

Fig. 11. The dc characteristics of a short neon tube, [7, p. 211].

![](img/039e7d3c23390584a66737067db8b75b_516_0.png)

![](img/039e7d3c23390584a66737067db8b75b_516_1.png)

(a) Singing arc, [5, p. 250]

(b) Memristor, [24, p. 1574]

Fig. 12. The DC v_M − i_M curve for the singing arc and for the memristor.

Starting from 25 mA Fig. 6 resembles to Fig. 11. However, such similarity as been already pointed out by [42, p. 992] who stated that the neon tube was another example of relaxation oscillator as well as the singing arc and the triode.

If we compare now the singing arc static characteristic Fig. 6 with the DC v_M − i_M curve of the memristor (Fig. 12) plotted in a recent publication of [24, p. 1574] the comparison between both curves shape is obvious. Especially if you take into account the legend which specifies that the locally-active region highlighted in red on Fig. 12 begins far from the origin exactly like in the case of the singing arc (Cf. supra).

But, we can go further by comparing the equation of each DC v_M − i_M curve. For the singing arc it has been given by Eq. (5). In their paper [24, p. 1580] gave for the memristor the following equation:

```
v_M = i_M \left( -1 + \frac{i_M^2}{(i_M + \alpha)^2} \right) \beta \quad (7)
```

This Eq. (7) may be written as:

```
v_M = i_M \left( -1 + \frac{1}{\left(1 + \frac{\alpha}{i_M}\right)^2} \right) \beta
```

A Taylor series expansion of the ratio up to order three reads provided that α / i_M ≪ 1:

```
\frac{1}{\left(1 + \frac{\alpha}{i_M}\right)^2} = 1 - \frac{2\alpha}{i_M} + \frac{12\alpha^2}{i_M^2} + h.o.t.
```

Thus, we find for the DC v_M − i_M curve of the memristor:

```
v_M = -2\alpha\beta + \frac{12\alpha^2}{i_M} + \dots \quad (8)
```

Since Eqs. (5) and (8) are identical, we can conclude that the singing arc “static characteristic” corresponds exactly to Chua’s DC v_M − i_M curve of the memristor.

## 4.3. Memristor: An hysteretic system

According to [7, p. 209] memristive systems are hysteretic. In order to study this effect let’s focus on the

> “Property 4-Double-Valued Lissajous Figure Property A current-controlled memristive one-port under periodic operation with i(t) = I cos ωt always gives rise to a v − i Lissajous figure whose voltage u is at most a double-valued function of i

![](img/039e7d3c23390584a66737067db8b75b_517_0.png)

Fig. 13. Hysteretic effect, [7, p. 212].

Precisely, it has been stated for the singing arc “dynamic characteristic” that the rising voltage curve is different from the falling one. By plotting any parallel to the v − axis it is easy to check on Figs. 7–9 that such a curve is double-valued. Moreover, the closed curve used by [7, p. 212] to emphasize this property and plotted on Fig. 13 is analogous to the “dynamic characteristic” presented on Fig. 7.

Property 5 was summarized by [7, p. 2132] by saying that “the v − i curve is odd symmetric with respect to the origin.” It is the case of Fig. 6 if we model it with a cubic function.

Then, let’s compare now this sentence from Chua’s conclusions [7, p. 220]

> “Various generic properties of memristive systems have been derived and shown to coincide with those possessed by many physical devices and systems. Among the various properties of memristive systems, the frequency response of the Lissajous figure is especially interesting. As the excitation frequency increases toward infinity, the Lissajous figure shrinks and tends to a straight line passing through the origin-except for some pathological cases where the bibs10 stability property is not satisfied. The physical interpretation of this phenomenon is that the system possesses certain inertia and cannot respond as rapidly as the fast variation in the excitation waveform and therefore must settle to some equilibrium state. This implies that the hysteretic effect of the memristive system decreases as the frequency increases and hence it eventually degenerates into a purely resistive system.”

and that of [4, p. 900] in which he claimed that “hysteresis effect is decreasing quickly as the frequency increases”.

10 bounded-input bounded-state.

At last, let’s notice that the Duddell’s singing arc circuit in Fig. 5 can be proved via Circuit theory principles, to be equivalent to the simplest chaotic circuit as exemplified in [24] paper. Since one more state variable is needed, in addition to L and C in Duddell’s circuit and since one non-linearity is also needed to obtain chaos as in [24] article, and since Duddell’s circuit exhibits “hissing” sounds, and, “noise-like” chaotic waveforms as observed with an oscilloscope by [3], it follows that the Duddell’s singing arc circuit in Fig. 5 is experimentally a chaotic circuit, and hence the singing arc must be a memristor.

## 5. Discussion

In this work, we have first recalled the history of the three classical circuit elements namely capacitor, resistor, inductor and the relationships, i.e. Volta’s law, Ohm’s law and Faraday’s law involving the four fundamental circuit variables: the current, the voltage, the charge and the magnetic flux in order to highlight the incompleteness of the Circuit Theory which lead Professor Chua to postulate the existence of a fourth element he called memristor. Then, we focused on the properties of an old non-linear device called singing arc, originally used in Wireless Telegraphy before the invention of the triode. By comparing the singing arc to the memristor we have highlighted an analogy between some of their properties. The memristor DC characteristic curve has exactly the same hyperbolic profile and the same equation as the singing arc “static characteristic”. Moreover, both memristor and singing arc are hysteretic systems exhibiting the same kind of closed curve in order to describe the “hysteresis effect”. So, we conclude that the singing arc could be considered as the oldest memristor. We believe that the hysteresis characteristic in Fig. 7 should have intersected each other at the origin, forming a “pinched” hysteresisloop. We therefore conjectured that the slight discrepancy of the “almost pinched” characteristic near the origin is due on the one hand to the imperfection of instruments used in this measurement and, on the other hand to the great variability of the conditions of the experiments.

## Acknowledgments

Authors would like to thank Dr. Bharathwaj Muthuswamy for his helpful advices.
