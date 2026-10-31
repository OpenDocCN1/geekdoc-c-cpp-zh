
CPU chip. Apart from the challenge of cooling such devices, this is, quite simply, an excessive amount of energy for the computations.147

Increasing the clock frequency further to achieve higher computing power is not easy because the problem of heat removal gets increasingly worse.

Digital computers are plagued by other problems as well – one of the most important effects is the upper bound of parallelism that can be obtained by an algorithmic approach for a certain problem as described by Amdahl’s law. Only few problems are so well behaved that they can exploit the computing power of a highly-parallel supercomputer. The majority of programs can’t be scaled effectively over many processing units.

It is obvious that alternative approaches to classic digital computing are required to fulfill the ever increasing demands for computational power. Analog computers will be a central part of such novel systems where they will act as co-processors to speed up time-consuming or time-critical simulations, etc., as they do not suffer from the aforementioned problems.

Due to the continuous representation of values as voltages or currents and the continuous time of operation within an analog computer, all signals (with the exception of comparator and switch outputs) representing variables are continuous variables without any steps. This results in very little energy consumption due to charging and discharging parasitic capacitances within the system.

Giving up the idea of a central memory system which stores commands and data to be processed in favor of interconnecting individual computing elements in order to set up an analog computer for a given problem, there is nothing like a von Neumann bottleneck and no algorithm at all which would limit the amount of parallelism achievable within an analog computer setup.

A lot of development work is required in the future to turn the classic analog computer with its exposed patch panel into a useful, general purpose, reconfigurable integrated circuit.148 A main challenge will be the design and implementation of the configuration circuitry which would allow the elements of such an analog computer to be interconnected automatically under the control of a digital computer which would act as a host system. In addition to the hardware, a software ecosystem must be developed including a suitable (standardized) hardware description language to describe the required interconnections of a particular analog computer setup, libraries allowing the tight integration of the analog computer on chip into a hybrid computer, etc.

These challenges are formidable but the possibilities of analog computing are nearly endless and will more than justify all research and development expenses necessary.

Given the high energy efficiency of analog computers compared with digital approaches they will create new fields of application – such as medical implants which could consume so little electrical energy that they could be powered by thermocouples, thus making energy storage devices that must be changed or recharged at regular intervals superfluous. It will also find numerous applications in mobile and wearable devices for signal pre- and post-processing to save precious battery capacity. Even rather complex tasks such as trigger word detection for assistance systems can be implemented using analog computer techniques, thus saving power in standby mode.

Other applications will benefit from the fact that a system that is not controlled by a program stored in some volatile memory can not be “hacked” in a traditional way.149. This will make analog computers the systems of choice when it comes to control systems in critical infrastructure systems, systems on which human lives depend, etc.

Also, most branches of artificial intelligence, (AI), machine learning will benefit from the application of analog computing techniques. Spiking neurons can be directly implemented as analog circuits and the fact that neuronal networks are basically defined by their interconnection structure, together with their synaptic weights, fits well with the paradigm of analog computing.

Analog computing is a very promising approach for future high performance and/or low energy computing and will become part of future computing and communication systems.

Happy analog computing!

## APPENDIX A
### Solving the heat equation with a passive network

The two-dimensional heat equation as treated in section 6.22 can also be solved by means of a 2d grid consisting of a number of identical passive resistor/capacitor (RC) node as shown in the following.¹⁵⁰ The aim is to model the heat flow in a two-dimensional sheet of conductive material such as a thin metal plate as described by

$$\dot{u} = \alpha \nabla^2 u.$$ (A.1)

To model the behaviour of this equation by means of a discrete two-dimensional grid of passive elements, it is approximated by finite differences yielding

$$\dot{u}_{i,j} = \alpha (u_{i-1,j} + u_{i+1,j} + u_{i,j-1} + u_{i,j+1} - 4u_{i,j}) + q_{i,j}$$

a single grid node $u_{i,j}$ with $q_{i,j}$ denoting a heat in- or outflow to/from that node. Such a node is shown in figure A.1 and consists of four resistors and a capacitor with a common junction. Applying KIRCHHOFF's current law to the center node $u_{i,j}$ yields the following expression for the voltage at this node:

$$\frac{(u_{i,j-1} - u_{i,j}) + (u_{i,j+1} - u_{i,j}) + (u_{i-1,j} - u_{i,j}) + (u_{i+1,j} - u_{i,j})}{R} - \frac{\dot{u}_{i,j}}{C} + I_{i,j} = 0.$$

The terms in the first fraction's numerator are the currents flowing through the resistors, the second fraction describes the current through the capacitor, and the

![](img/91599d88757ed8c75960eb83f4f85a12_230_0.png)

axes of symmetry

equipotential boundary

quadrant to be solved

plate

Fig. A.2. 16 × 16 cm plate structure

![](img/91599d88757ed8c75960eb83f4f85a12_230_1.png)

α

u7,0

u7,7

β

I0,0

u0,0

u0,7

Fig. A.3. Passive network for one quadrant

![](img/91599d88757ed8c75960eb83f4f85a12_231_0.png)

Fig. A.4. Implementation of the two-dimensional RC-network

![](img/91599d88757ed8c75960eb83f4f85a12_231_1.png)

Fig. A.5. Steady state of the network and differences between adjacent nodes

temperature distribution across the plate quadrant. The graph on the right shows the heat flux densities which were obtained by measuring the voltages across the individual resistors which correspond to the heat flux between adjacent nodes. This yields the x- and y-components of the heat flux which allowed the heat flux magnitudes in between the nodes to be calculated.

Figure A.6 shows the time dependent voltages at the diagonal nodes u_{i,i} after injecting a pulse I_{0,0} at the corner grid node u_{0,0}. The diffusion of the temperature across the plate quadrant can clearly be seen as well as the eventual settling of the nodes along the diagonal to the boundary condition temperature as defined by the inputs α and β_i.

As inflexible as passive networks like this are with regard to their spatial structure, they can be used to solve partial differential equations of a given structure with varying boundary conditions very efficiently. [VOLYNSKII et al. 1965] contains a lot of practical examples and theoretical background.

![](img/91599d88757ed8c75960eb83f4f85a12_232_0.png)

Fig. A.6. Response to a step input at nodes u0,0, u1,1, ... u7,7 (from left to right and up/down)

## B.1 Basic functions

This section presents the derivation of the LAPLACE transforms for some basic functions.

### B.1.1 Step function

One of the most basic functions is the *step function*

$$f(t)=\begin{cases}0 & t<0\\a & t>0\end{cases}$$

with amplitude $a\in\mathbb{R}^+$. In the case of $a=1$ it is called *unit step function*, denoted $u(t)$ which is also known as *HEAVISIDE step function* after OLIVER HEAVISIDE.[^154] Its LAPLACE transform is[^155]

$$\mathcal{L}\{u(t)\}=\int_0^\infty ae^{-st}\,dt=a\int_0^\infty e^{-st}\,dt.$$  \tag{B.2}

Substituting $\varphi=-st$ yields $dt=-\frac{1}{s}\,d\varphi$, so (B.2) simplifies to

$$\mathcal{L}\{u(t)\}=\frac{a}{s}\int_0^\infty e^{\varphi}\,d\varphi=\frac{a}{s}\left[e^{-st}\right]_0^\infty=\frac{a}{s}.$$  \tag{B.3}

A variant of the step function is the *delayed unit step function*

$$u(t-T)=\begin{cases}0 & t<T\\1 & t>T\end{cases}$$

with the following LAPLACE transform

$$\begin{aligned}\mathcal{L}\{u(t-T)\}&=\int_0^\infty u(t-T)e^{-st}\,dt\\&=\int_0^T u(t-T)e^{-st}\,dt+\int_T^\infty u(t-T)e^{-st}\,dt\\&=\int_T^\infty e^{-st}\,dt=-\frac{1}{s}\left[e^{-st}\right]_T^\infty=\frac{e^{-sT}}{s}.\end{aligned}$$

[^154]: See [Yavetz 1995] for more information on Heaviside’s work.

[^155]: Note the lower bound of integration.
