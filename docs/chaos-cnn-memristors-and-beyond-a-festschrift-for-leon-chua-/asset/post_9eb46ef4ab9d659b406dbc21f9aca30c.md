
considered, frequency modulation can be easily achieved through the switched capacitor technique [65]. This gives the possibility to easily control robots endowed with a number of different actuators, working at thoroughly different frequencies.

- **Oscillation period control**. In the case of this slow-fast limit cycle, a proper modulation of the bias term $i_2$, moves the nullclines within the phase portrait. There are critical values on $i_2$ such that the limit cycle collapses into a stable equilibrium point. Soon before the critical value, the slow part of the oscillator slows down. It means that the spiking characteristics of the signals are maintained, whereas the recovery time is slowed and the slow-fast ratio can be easily controlled. Being the slow part associated to the stance phase of the gait cycle, the period control is easily translated into a speed control in the locomotion pattern.

## 2.3. CPG in a reaction-diffusion CNN structure

The idea that inspired the RD-CNN approach for CPG, was to conceive locomotion as a complex spatial-temporal phenomenon, involving a large number of variables, whose dynamics is relevant in time and in space. Membrane-like dynamics are a classical example of this idea. Each node of the membrane cannot move alone: its dynamics depends heavily on that one imposed by its neighbors. This concept exactly matches with the electronic paradigm of the CNN, and is clearly related to the CPG, where each unit (leg or joint) motion is related to the motion of the neighboring units. Single activations (reaction), at the level of the single cell, imply energy dissipation (diffusion) which affects the neighbor dynamics, leading to the emergence of ordered spatial-temporal neural field dynamics over lattices of units, like the CNNs. The so-called Reaction-Diffusion paradigm was used in the last decades to model a huge quantity of natural phenomena in Chemistry, Morphogenesis, Neurobiology [77]. Typical emerging solutions of this complex dynamics are self-sustained oscillating phenomena, known as autowaves [67], as well as patterns arising in Morphogenesis, known as Turing patterns [97]. Both autowaves and Turing patterns were demonstrated to take place in CNN structures, called Reaction-Diffusion CNNs (RD-CNNs), and both phenomena were considered: the former

to address locomotion, the latter to face with perception, as discussed in the next sections. From our perspective it has to be underlined that, from the one side, the neural firing possesses all the characteristics of an Autowave front [41], and on the other side, autowaves were demonstrated to take place in a RD-CNNs endowed with the cells (1) and with the following templates:

```
$A_{11} = \begin{pmatrix} 0 & D_1 & 0 \\ D_1 & -4D_1 + \mu + \epsilon + 1 & D_1 \\ 0 & D_1 & 0 \end{pmatrix}; \quad (2)$
```

```
$A_{22} = \begin{pmatrix} 0 & D_2 & 0 \\ D_2 & -4D_2 + \mu - \epsilon + 1 & D_2 \\ 0 & D_2 & 0 \end{pmatrix}; \quad (3)$
```

```
$A_{12} = \begin{pmatrix} 0 & 0 & 0 \\ 0 & -s_1 & 0 \\ 0 & 0 & 0 \end{pmatrix}; A_{21} = \begin{pmatrix} 0 & 0 & 0 \\ 0 & s_2 & 0 \\ 0 & 0 & 0 \end{pmatrix}. \quad (4)$
```

where $D_1 = 0.1$ and $D_2 = 0.1$ represent the synaptic diffusion coefficients and the other parameters are the same as specified in Sec. 2.2.

These templates include both the dynamics of the single cell and the synaptic activity, modelled as a diffusion effect, coherently with the concept of electrical synapse. The so-called Zero-Flux (Neumann) boundary conditions were assumed. Moreover the robustness of this CNN model to parametric uncertainties and noise was assessed and a discrete component hardware implementation was also achieved [2].

Different RD-CNNs configurations were employed to work as CPGs for a number of Biorobots that were designed and built in our laboratory. It is to be emphasised that the focus is here more on the design and realization of the locomotion controller than on the robotic structure. On the other side, excellent work on the mechanical aspects of Biomimetic robots was already performed [70, 88]. Instead, in the present approach, the robot has to be viewed as the test bed in which the efficiency of the locomotion control can be appreciated, as the visible solution of the neural lattice where the nonlinear dynamics take place. The robot joints were, in most cases, implemented by using simple servomotors: so the trajectories shown by the cells are translated in sequences of position set points for the robot actuators. In Fig. 2 the circuit realization is depicted for a particular ring configuration of the

![](img/039e7d3c23390584a66737067db8b75b_74_0.png)

Fig. 2. A gallery of robots controlled by the RD-CNN CPG approach.

RD-CNN used as the CPG in a worm-like walking machine and in a hexapod robot [3], as well as in a lamprey-like robot [10]. These are also sketched in Fig. 2.

In the basic implementation referring to legged prototypes, each leg had two degrees of freedom, which span a 2D plane in the robot workspace in an elevator-protraction way, whereas they act as a flexor-extensor couple in each segment of the lamprey robot. So each joint in every structure was driven by one output variable of a CNN cell (see Eq. (1)). This hardware structure, joined to the simple implementation of local feedback strategies on each single cell, as outlined above, results in an efficient locomotion controller. In fact, besides the control strategies on each single cell outlined above, the overall dynamics in the neural lattice can be easily controlled in terms of speed of the travelling wave: this can be realised varying the number of cells in the ring, with the consequent variation of the slow part of the limit cycle for each cell [2]. Moreover, a transition among different gaits, typical of hexapods, can easily achieved by modulating the connections among the CPG and the legs, with a consequent variation of the phase among the moving legs, which varied from

the slow (tetrapod) to the medium, to the fast (tripod) gait.

A typical characteristics of neural systems is *graceful degradation*: if some neurons die, the overall organization of the neural field dynamics is only slightly affected. This was experimentally observed in a hexapod robot: cutting a neuron out of the ring caused the partial loss of the phases among the oscillators, so locomotion control was affected, but nevertheless the structure was indeed able to move.

More sophisticated locomotion capabilities can be obtained by increasing the dexterity of the legs from two to three joints. This was done in Rexabot III [5] and in the Gregor series of hexapod robots [20]. Here each leg was controlled by two identical cells of the type reported in Eq. (1), from which three controlling variables were extracted to drive the joint servomotors. In Rexabot III the problem of attitude control was also taken into consideration and solved with the design and implementation of another CNN structure, acting concurrently with the CNN-CPG, where each cell was a nonlinear PD controller, designed to maintain a set point in the roll-pitch plane. In this case the robot was controlled by the combination

![](img/039e7d3c23390584a66737067db8b75b_75_0.png)

(a)

(b)

Fig. 3. Attitude control: (a) Rexabot III with the analogic attitude controller for roll and pitch; (b) Gregor III controlled through a reflex-based approach.

of the signals coming from the CPG and those ones coming from the attitude controller. A relevant characteristics of the approach is that the set points used for the attitude control come from only one double axis accelerometer, placed in the abdominal part of the robot. It derives that the feedback signal acts on the whole network controller. This causes each of the controllers to cooperate for compensating errors in the attitude that could not be caused by the corresponding leg. For example, if one of the legs is overloaded, or is broken, it was experimentally shown that legs self-organise in such a way as to try to recover from overload or to attain the requested attitude even in presence of a broken leg. It is to be emphasised that this approach is analog, space distributed and characterised by a local connectivity, with the consequent characteristics of a real time efficiency and modularity that allows a

direct extension to a larger number of actuators. In Fig. 3(a) Rexabot III is depicted in really sloped grounds, maintaining the horizontal attitude; moreover the Gregor robot controlled through a reflex-based strategy is also shown in Fig. 3(b) when facing with a uneven terrain.

Various locomotion patterns can be implemented using such a structure. The way to change the locomotion pattern is to use a different number of cells constituting the RD-CNN and to enroll or discard (by activating or inhibiting some synaptic inputs) some neurons in the structure to adapt the phase and the speed of the travelling wave front. Suitable commands (a few indeed) are therefore supposed to come down from the higher control regions to solve this task. The synchronization of the leg phases thus depends on the neural organization within the CPG. One advantage in terms
