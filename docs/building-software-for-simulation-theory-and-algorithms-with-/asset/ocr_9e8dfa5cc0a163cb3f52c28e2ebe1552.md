![](bbox=[0.242, 0.112, 0.792, 0.328])

**FIGURE 2.1** Bottom–up construction of a model from functional pieces: (a) input, output, and internal state of an atomic model; (b) a network model constructed from three atomic models.

These network models to create larger components, and repeating until the software is finished. This bottom-up approach to model construction is illustrated in Figure 2.1.

The simulation engine operates on software objects that implement atomic and network models. To build a simulator therefore requires the parts of a dynamic system to be expressed in this form. Functional models need not be built in a single step. Atomic and network models are more easily obtained by a set of steps that start with an appropriate modeling technique, proceed to a state space description of the model’s fundamental dynamics, combine these to create more sophisticated components, and end with a—possibly large—functional model that can be acted on by the simulation engine.

# 2.2  A ROBOTIC TANK

The robotic tank is simple enough to permit a thorough discussion of its continuous and discrete dynamics, but sufficiently complicated that it has features present in larger, more practical systems. The robot’s operator controls it through a wireless network, and the receipt, storage, and processing of packets is modeled by a discrete event system. An onboard computer transforms the operator’s commands into control signals for the motors. The motors and physical motion of the tank are modeled as a continuous system. These components are combined to create a complete model of the tank.

Our goal is to allocate the cycles of the tank’s onboard computer to two tasks: physical control of the tank’s motors and processing commands from the tank’s operator. The tank has four parts that are relevant to our objective: the radio that receives commands from the operator, the computer and software that turn these