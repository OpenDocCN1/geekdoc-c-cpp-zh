
embedded system. Building on these notions, we will evolve a formal FSM model. We will then briefly examine basic *registers* and *shift registers*, which are fundamental to the register transfer level (RTL) model of most contemporary computing cores and to error-detecting and error-correcting systems. Next, we will revisit fundamental *counters* and *dividers* and the critical role they play in the design of clock and time-base subsystems commonly used in embedded designs. Building on this theoretical basis, we will then examine the effects of nonideal behavior in real-world applications.

As we did with our studies of combinational circuits, we will conclude with an introduction to testing sequential circuits. Many of these techniques will subsequently be applied in our studies of debugging embedded designs in Chapter 10. Because they are built around memory devices, sequential systems are significantly more complex to test than combinational circuitry. Their behavior is time dependent and governed by the values of their input signals and the order in which they appear. Compounding the test problem in FSMs is the inherent cyclic nature of such systems. We will introduce and study several different methods for attacking the problems unique to sequential circuitry.

## 3.2 THE CONCEPTS OF STATE AND TIME

We begin the discussion of finite-state systems by examining the concepts of time and state.

### 3.2.1 Time

A combinational logic system has no notion of time or history. The present (static) output does not depend in any way on how the output values were achieved. Neglecting delays through the system, we find that the output is immediate and a direct function of the current input set. In contrast, the current output of a finite-state system depends both on the path the system took to reach the current state and, potentially, the present values of the input set. Time is an integral part of the behavior of such systems.

### 3.2.2 State

In an analog circuit, we define branch and mesh currents and branch or node voltages. The values these variables assume over time characterize the behavior of that circuit. If we know the values of the specified variables over time, we know the behavior of the circuit.

*state variables, state of a system*

Such variables are called *state variables*. We define the *state* of a system at any time as a set of values for such variables; each set of values represents a unique state. Figure 3.1 illustrates a collection of example states. When the value of any variable changes, the state of system changes.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_175_0.png)

Figure 3.1 A Collection of States

### 3.2.3 State Changes

In traditional logic, a simple memory device, represented by a single variable, has two states, binary 0 and binary 1. The device will remain in the state until changed. For a set of state variables, the state changes with time are called the *behavior of a system*. For simple systems, one can exhaustively name each state. For more complex systems, some form of algorithm or formula is often more efficient.

## 3.3 THE STATE DIAGRAM

**state diagram, graph** In the embedded world, the *state diagram*, or more formally a *graph*, is one means used to capture, describe, and specify the behavior of a system. In a state diagram, each state is represented by a circle, *node*, or *vertex*. We label each node to identify the state. The label should be simple and descriptive. A memory device has two states – its output is a logical 1 or a logical 0; thus, to express its behavior we will need two nodes as shown in Figure 3.2.

**arc, edge, head directed graph, edge final state, tail initial state** We show the transition between two states using a labeled directed line or arrow called an *arc* (or *edge* in graph theoretic language), as illustrated in Figure 3.3. Because the line has a direction, the state diagram is referred to as a *directed graph*. The *head* or point of the arrow identifies the *final state*, and the *tail* or back of the arrow identifies the *initial state*. Special arcs, such as the one labeled *initial*, reflect an external, overriding asynchronous event, such as a reset, which places the system into a designated state, here *state a*.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_176_0.png)

![](img/679b8d2d47f1bf86e17aca48f596f5cc_176_1.png)

**cyclic graph** Because the graph can contain cycles, it is further qualified as a *cyclic graph*. The label on each identifies what caused the change and the output(s) of system, if appropriate.

### EXAMPLE 3.1

We can use a state diagram such as that in Figure 3.4 to describe an evening’s entertainment. The diagram graphically expresses the same behavior that is described textually in Figure 3.5.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_176_2.png)

```
enter room
if in state awake
    Input boring event
    Change to state asleep
else if state asleep
    Input fall off chair
    Change to state awake
```

Figure 3.5 Textual Description of the Behavior Expressed in the State Diagram

In the embedded world, the state diagram is a very powerful tool for specifying and modeling the behavior of many different kinds of hardware and software systems from a high level, abstract point of view and, as the design progresses, from a detailed point of view.

## 3.4 FINITE-STATE MACHINES – A THEORETICAL MODEL

We can (in theory) express the behavior of an arbitrarily complex digital system using a state diagram. The diagram captures the states, the system inputs and outputs, and the transitions among those states in response to the inputs. Extensions to the basic diagram, such as we find in hardware/software co-design tools or the Unified Modeling Language (UML) state charts, support a rich set of system-modeling capabilities.

Unified Modeling Language(UML)

finite-state machine

A sequential circuit, or more formally, a finite-state machine, is the means by which we ultimately transform the behavior expressed in the state diagram into a hardware and/or software implementation. Such circuits also form the basis for the sophisticated computation and control algorithms that one finds at the core of most modern digital systems.

A hardware implementation of such machines can be effected utilizing:

- Large-scale integrated (LSI) or very large-scale integrated (VLSI).
- Arrayed logic.
- Programmable logic devices (PLDs) or (complex) programmable logic devices (CPLDs).
- Read only memory (ROMs).
- Discrete logic.

A software implementation will typically appear as the firmware that executes on any of the various pieces of hardware.

Simple FSMs as shown in Figure 3.6 have no inputs other than a clock and have only primitive outputs (we generally don’t show the clock). Such machines are referred to as autonomous clocks. As we move to more complex designs, we will introduce inputs as well as more sophisticated outputs. A high-level block diagram for a FSM begins with the diagram in Figure 3.7.

autonomous clocks

![](img/679b8d2d47f1bf86e17aca48f596f5cc_177_0.png)

![](img/679b8d2d47f1bf86e17aca48f596f5cc_177_1.png)

The outputs shown in the diagram may be the values of the state variables (as they will be in counting-type designs), combinations of the state variables, or combinations of the state variables and the inputs.

Refining the level of detail, the block diagram for the state machine appears as shown in Figure 3.8.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_178_0.png)

Figure 3.8 A High-Level Block Diagram for a Finite-State Machine

**state variables, outputs** We see first that the signals out of the FSM decompose into two sets: state variables and outputs. Observe that the state variables are fed back as inputs to the system. The diagram illustrates the essence of the strength of the machine. It has the ability to recognize the state that it is in and then to react based on the values of the state variables and (potentially) to the inputs to the system. The decision as to which state to go to next is determined from the current input and the state that the machine is currently in. The present state of a FSM inherently encodes the history of the path taken to get there.

If we continue increasing the level of detail in the model, we now include the storage elements comprising the machine and the combinational logic that implements the output functionality and the input equations to the storage elements. The block diagram now becomes that in Figure 3.9.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_178_1.png)

Figure 3.9 A High-Level Block Diagram for a Finite-State Machine

**n inputs, m outputs, p state variables** The model has n inputs, m outputs, and p state variables. A memory device is associated with each state variable, and each state variable is associated with a memory device. At this point no particular type of memory device is specified.

Working from this block diagram, we can begin to formalize our model of the FSM. That model must reflect the inputs, outputs (which may be a function of the inputs and the
