
Since the input current $i_i$ of a typical operational amplifier is less than a few nA at most, it can be neglected, so that (2.2) simplifies to

$$\frac{e_i-e_{SJ}}{R_i}=-\frac{e_o-e_{SJ}}{R_f}.$$

Substituting (2.1) into this yields

$$\frac{e_i+\frac{e_o}{\mathcal{A}}}{R_i}=-\frac{e_o+\frac{e_o}{\mathcal{A}}}{R_f}.$$

Some rearranging results in

$$e_o\left(\frac{1}{\mathcal{A}R_i}+\frac{1}{R_f}+\frac{1}{\mathcal{A}R_f}\right)=-\frac{e_i}{R_i}$$

which can then be solved for $e_o$:

$$e_o=\frac{-\frac{e_i}{R_i}}{\frac{R_f+\mathcal{A}R_i+R_i}{\mathcal{A}R_iR_f}}$$

$$=\frac{-\frac{e_i}{R_i}\mathcal{A}R_iR_f}{R_f+\mathcal{A}R_i+R_i}$$

$$=\frac{-\frac{R_f}{R_i}e_i}{1+\frac{1}{\mathcal{A}}\left(\frac{R_f}{R_i}+1\right)}.\tag{2.3}$$

Since $\mathcal{A}$ is typically very large$^{15}$ and $R_f/R_i$ is typically $\leq 10$, the denominator of (2.3) can normally be neglected, yielding the simplified form

$$e_o=-\frac{R_f}{R_i}e_i.\tag{2.4}$$

describing the output voltage of the feedback circuit shown in figure 2.3.$^{16}$

$^{15}$ In fact, classical high-precision operational amplifiers used in analog computers had gains of up to $\mathcal{A}=10^9$.

$^{16}$ A more informal approach to the behaviour of such circuits is to assume that the open-loop gain of the operational amplifier is extremely large, therefore, the voltage at the summing junction is approximately zero. Since the input current of the amplifier is negligible, applying Kirchhoff's law to the currents at the summing junction shows that the current through the feedback element is minus the sum of the currents through the input resistors. Applying Ohm's law then readily yields the output voltage of the computing element.

![](img/91599d88757ed8c75960eb83f4f85a12_29_0.png)

Fig. 2.4. Summer with several inputs based on an operational amplifier with negative feedback

This shows that the behaviour of this circuit is basically determined by the resistors at the input and in the feedback path. If more input resistors are added as shown in figure 2.4, a useful summing circuit results whose overall behaviour is readily described by

$\sum_{i=1}^{n} \frac{e_i}{R_i} = - \frac{e_o}{R_f}$ (2.5)

The voltage at the output of this circuit is thus the negative of the sum of the voltages at its inputs. The ratios

$a_i = \frac{R_f}{R_i}$

define the weights of the various inputs. Typical values for $a_i$ are 1 and 10. If unusual values are required for a certain setup, the necessary resistors can be connected to the summing junction SJ, thus effectively extending the number of inputs of the summer.

### Summer basics:

The behaviour of an (ideal) summer is described by $e_o = - \sum_{i=1}^{n} a_i e_i$ with the weights $a_i$ being typically 1 or 10. It yields the negative sum of the weighted voltages applied to its inputs. Typical summers have about six inputs, three of which have input weight 1 while the remaining three inputs are weighted by 10.

In some cases it is necessary to disconnect the resistive feedback loop of a summer in order to introduce an external feedback circuit. This case is represented by the symbol shown in figure 2.5. This element is no longer called summer but *open amplifier* or *high gain amplifier* instead. This element always requires some external feedback in order to be stable.

![](img/91599d88757ed8c75960eb83f4f85a12_30_0.png)

![](img/91599d88757ed8c75960eb83f4f85a12_30_1.png)

Fig. 2.6. Computer setup according to equation (2.6)

To show the application of summers in a typical analog computer setup, consider the circuit shown in figure 2.6. It solves the equation

$$e_o=-\left(10\left(-\frac{e_1+e_2}{2}\right)+e_3\right)=5(e_1+e_2)-e_3. \tag{2.6}$$

The connection between the output of the first summer and one of its inputs[^17] introduces a second feedback resistor parallel to $R_f$, thus effectively doubling the effect of the feedback loop. This, in turn, halves all other input weights of the summer yielding

$$\frac{e_1+e_2}{2}$$

at the output of the left summer. This output is now connected to an input of the right summer, weighted with 10. Another input of this summer is fed with $e_3$ finally yielding $e_o=5(e_1+e_2)-e_3$.

Figure 2.7 shows the front panel of an Analog Paradigm SUM8. This module contains eight summers, each featuring five inputs, three of which have weight 1 and two have weight 10. The four summers in the top row have a special feature which allows their self-feedback resistor path to be opened by patching a connection between the two jacks labelled FB and ⊥ (this symbol denotes ground), thus turning a summer into an open amplifier.[^18] The summing junction SJ is also available on all eight summers.

![](img/91599d88757ed8c75960eb83f4f85a12_31_0.png)

Fig. 2.7. Analog Paradigm SUM8 module

## 2.3 Integrators

At first sight it is astonishing that an analog computer features integration as one of its basic operations. This makes it the ideal machine to solve problems that can be described by differential equations and systems thereof. But there is a catch: Integration on an analog-electronic analog computer is always with respect to time, so all integrations are basically of the form

$$e_o=-\left(\int_0^t\sum_{i=1}^{n}a_i e_i\,d\tau+e(0)\right) \tag{2.7}$$

with some constant $e(0)$ called the *initial condition*. In particular, this means that *partial differential equations*, i. e. differential equations in which derivatives with respect to more than one variable occur, cannot be handled directly on an analog computer without explicit discretization or other techniques!

Obviously, the output of an integrator depends on the history of its input values, so this computing element is a kind of memory. In contrast to a simple summer, this necessitates some control of its operation as an integration has

![](img/91599d88757ed8c75960eb83f4f85a12_33_0.png)

Fig. 2.8. Behaviour of a typical integrator

with time scale factors k_q = 10^n with n ∈ ℕ typically ranging from 0 to 3 although some large historic systems, such as the EAI 680,20 feature time scale factors up to 10^5.

By changing the time scale factors of the integrators in a computer setup it is possible to speed up a calculation or slow it down. This is known as time scaling. Consequently, it is necessary to distinguish between problem time t, the time scale the problem under investigation runs in, and machine time τ, the time scale the computer operates in, as determined by the time scale factors set on the integrators.

Figure 2.9 shows the graphical representation of an integrator as it is used in analog computer programming. It differs from the symbol for a summer by the addition of a rectangle on its left-hand side, with a vertical bar on its top to which the initial condition value e(0) is connected (this input is always drawn vertically). Like the summer it has a number of inputs with associated weights of typically 1 and 10.

Figure 2.10 shows the front panel of an Analog Paradigm INT4 quad integrator module. Each of its integrators can be set to a time scale factor of 1, 10, 100, or 1000 by a rotary switch and features three inputs weighted by 1 as well as three inputs weighted by 10. In addition to this, each integrator has an initial condition input labelled IC, and a jack yielding +1 or -1 in its vicinity as these values are often used as initial conditions.

![](img/91599d88757ed8c75960eb83f4f85a12_35_0.png)

Fig. 2.10. Quad integrator module

![](img/91599d88757ed8c75960eb83f4f85a12_35_1.png)

Fig. 2.11. Basic schematic of an integrator

IC: In IC-mode, the switch labelled OP connects the input resistor array to ground, thus effectively disabling all inputs, while the IC-switch is in the position shown in the figure. Accordingly, the operational amplifier operates basically as a summer with only one input, IC. The voltage over the temporary feedback resistor R_IC equals −IC which in turn precharges the capacitor to the negative value of what is present at the IC input jack. The time required to charge the capacitor in this mode of operation now depends on its capacity and the input resistor being active during this mode.
