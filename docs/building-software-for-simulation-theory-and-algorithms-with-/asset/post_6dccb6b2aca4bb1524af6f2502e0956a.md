
![](img/df6085a1b35edf9c9ea818a5c66ccad9_30_0.png)

**FIGURE 2.5**  Generating a voltage signal with the interrupt handler.

albeit indirectly, by the operator. If the counter is greater than or equal to the ON time, then the motor is turned off. If the counter is less than the ON time, then the motor is turned on. If, for example, the tank is operating at full power, then the ON time for both motors is 255 and the motors are always on; if the motors are turned off, then the ON time is zero.

In Figure 2.5, the counter is initially zero and the motors are turned off. The ON time is 128. The first call to the interrupt handler adds 32 to the counter, compares 32 < 128, and turns the motor on by connecting it to the tank’s 7.2-V battery pack. At call 4, the counter is assigned a value of 128, which is equal to the ON time, and the motor is shut off. At call 8, the counter rolls over and the motor is turned on again.

The code in the interrupt handler is short; it has 41 assembly instructions that require 81 machine cycles to execute. According to the computer’s manufacturer, there are 18.75 × 10⁶ machine cycles per second, which is one cycle every 0.0533 × 10⁻⁶ s (0.0533 μs). The interrupt handler, therefore, requires 0.432 × 10⁻⁶ s (0.432 μs) to execute. The frequency of the voltage signal is determined by how quickly the interrupt handler rolls the counter over. On average, eight calls to the interrupt handler complete one period of the voltage signal. The length of this period is 8 × (0.432 × 10⁻⁶ + 0.0533 × 10⁻⁶ × N). We can choose N and thereby select the period of the voltage signal; the frequency fₑ due to this selection is

$$f_e \approx \frac{10^6}{3.46 + 0.426N} \qquad (2.32)$$

The discrete-event model of the interrupt handler has two types of events: *Start interrupt* and *End interrupt*. The *Start interrupt* event sets the interrupt indicator to true and schedules an *End interrupt* to occur 0.432 × 10⁻⁶ s later. The *End interrupt* event increments the counter, sets the motor switches, sets the interrupt indicator to

![](img/df6085a1b35edf9c9ea818a5c66ccad9_31_0.png)

**FIGURE 2.6** Event graph for the interrupt handler.

false, and schedules a *Start interrupt* event to occur 0.0533 × 10⁻⁶ N s later. There are two software switches, one for each motor, and each switch has three positions. If the software switch is in the first position, then the motor is connected to the tank’s 7.2-V battery pack. If the switch is in the second position, then the motor is connected to the batteries but the positive and negative terminals are reversed and the motor runs backward. In the third position, the motor is disconnected from the batteries. At any given time, a new ON time and direction for either motor can be given to the interrupt handler, and it acts on the new settings when the next *End interrupt* event occurs.

An event graph for the interrupt handler is shown in Figure 2.6 (event graphs were introduced by Schruben [131]; Fishwick [42] describes their use in functional models). The model has nine state variables. Four of these are apparent in the diagram: the 8-bit counter c, the *interrupt* indicator, and the switches sₗ and sᵣ for the left and right motors. Events that change the ON time and direction of a motor are inputs to the model; these input variables are stored as the *left motor ON time*, *left motor direction*, *right motor ON time*, and *right motor direction*, bringing the count of state variables to eight. Implicit in the edges that connect the events is the time until the next event occurs, which is the ninth and final state variable for this system. The outputs from this model are the interrupt indicator and the left and right motor voltages. The output variables change immediately after the corresponding state variables. In the case that an event is scheduled at the same time that an input variable is changed, the event is executed first and then the corresponding variables are modified.

When the computer is not busy with its interrupt handler, it is processing commands from the operator. Every command arrives as a UDP packet with 10 bytes: two floating-point numbers that specify the direction and duty ratio of the left and right motors, and 2 bytes of information that are not relevant to our model. The computer
can receive data at a rate of about 40 kilobytes per second (kB). This estimate, which comes from the iGuru forum [120], agrees reasonably well with, but is slightly lower than, the maximum data rate given by the manufacturer. The computer talks to the 802.11b radio through an Ethernet (the radio is controlled by a separate microprocessor) that has a minimum packet size of 64 bytes, much larger than the 10-byte payload. Consequently, we can optimistically estimate that processing a packet takes 0.0016 s (1.6 ms, or 1600 µs). We will ignore packet losses and assume that the computer (or, at least, the radio) can store any number of unprocessed packets. This is modeled with a server that has a fixed service time and an infinite queue. When the interrupt handler is executing, the server is forced to pause. The server produces on times and directions for the motors when it finishes processing a packet.

Figure 2.7 is a DEVS graph (described by Zeigler et al. [159] and, more recently, by Schulz et al. [132]; these are sometimes called *phase graphs* [42]) for this model. It has three state variables: the packet queue q; the time σ remaining to process the packet at the front of the queue; and the model’s phase, which is *interrupted* or *operating*. It responds to two types of input: the interrupt indicator from the interrupt handler and packets from the network. The interrupt indicator moves the system into its *interrupted* phase where it remains until a second interrupt indicator is received, and this moves the system back to its *operating* phase. When the computer finishes processing a packet, it sets the on time and direction for the left and right motors and begins to process the next packet or, if there are no packets left, becomes *idle*. Each edge in the phase graph is annotated with the state variables that change when the phase transition occurs. Each phase contains its duration and the output value that is generated when the phase is left because its duration has expired.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_32_0.png)

**FIGURE 2.7** Phase graph showing how the computer processes a packet.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_33_0.png)

FIGURE 2.8  Block diagram of the tank’s computer.

The models of the interrupt handler and thread that processes packets are connected to create a model of the computer. The interrupt handler receives the motor on times from the thread that processes packets; the thread receives interrupt indicators from the interrupt handler and packets from the network. The output from the computer sets the voltage at the left and right motors. Figure 2.8 shows a block diagram of the computer with its inputs, outputs, and internal components.

The event graph and phase diagram are informative but not definitive. They do not specify when, precisely, output is produced or how to treat simultaneous events. These issues are deferred to Chapter 4, where state space models of discrete-event systems are formally introduced.

## 2.2.5 Complete Model of the Tank

The complete model of the tank comprises the computer and the tank’s physics. The output of the computer is connected to the input of the tank’s physics. The position and orientation of the tank are displayed for the driver. The driver closes the loop by sending packets with control information to the computer. This arrangement is shown in Figure 2.9. The tank’s operator is not a model; the operator controls the simulated tank with the same software and hardware that are used to control the real tank.

![](img/df6085a1b35edf9c9ea818a5c66ccad9_33_1.png)

FIGURE 2.9  Block diagram of the simulated tank and real operator.
