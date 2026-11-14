
- (d) Can you explain why the circuit behavior has suddenly changed? Use your real-world timing diagram as necessary for illustration.

- (e) Can you determine the maximum frequency at which the circuit can be safely operated?

### 3.10
- (a) For the following circuit in Figure P3.4

![](img/679b8d2d47f1bf86e17aca48f596f5cc_220_0.png)

Figure P3.4

Please give a detailed timing diagram for signals A–F. You have the following specifications:
- Input clock 1 MHz
- Flip Flops
  - t_setup = 10 ns
  - t_hold = 0 ns
  - t_phl = 15 ns
  - t_plh = 10 ns
- Gates
  - t_phl = 7 ns
  - t_plh = 11 ns

At what input clock frequency will the circuit fail to properly generate the output signals E and F?

### 3.11
You have been asked to do a detailed analysis and design review of the counting circuit in Figure P3.5.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_220_1.png)

Figure P3.5

- (a) As part of the review you decide to determine the counting sequence for the circuit. Give a table showing the complete sequence of states the machine goes through starting at the initial state of 000.

- (b) As a next step toward analyzing the design, you draw the ideal timing diagram (no delays) for the circuit showing the signals at points A, B, C, the reset line, and the 2 MHz output – all with respect to the clock.

- (c) You next move to the vendor’s data sheets for the flip-flops containing the characteristics:
  - t_phl = 15 ns
  - t_plh = 30 ns
  - t_su = 35 ns

  The AND and NAND gates have the characteristics:
  - t_phl = 10 ns
  - t_plh = 5 ns

  Draw the actual timing diagram for the circuit showing signals at points A, B, C, the reset line, and the 2 MHz output with respect to the clock when the practical circuit parameters are considered.

- (d) Concluding your analysis, are there any states of flip-flops A, B, and C, the reset, or the 2 MHz clock that could be a problem? If so, what are they and why are they a problem? Is it important to be specific in a design review?

- (e) Can you recommend a change to the design to correct any problems you have discovered?

### 3.12
Design a four-stage Johnson counter.

- (a) Detect any of the illegal states and force the counter back to the 0000 state. You cannot do this by using the master reset or clear signal.

- (b) Detect all of the illegal states and force the counter back to the 0000 state. You cannot do this by using the master reset or clear signal.

- (c) Discuss the pros and cons of the two designs.

- (d) Under what circumstances would you select the first design? the second design?

### 3.13
A counting circuit has the output waveforms given in Figure P3.6.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_220_2.png)

Figure P3.6

- (a) Give the state table for a 3-bit counter that operates according to the timing diagram given in Figure P3.6. Assume that the machine starts in an initial state of 000.

- (b) What is the period of such a counter in input clock cycles? Why?

- (c) Design and draw the logic diagram for a counter, using D flip-flops, that operates according to the timing diagram and state table from part (a). Your flip-flops must reflect on which edge of the clock the transitions occur. Be sure to take into account any don't cares.

- (d) The vendor's data sheets show that the flip-flops and gates have the following characteristics:
  - t_pdl = 20 to 30 ns
  - t_pdh = 10 to 20 ns
  - t_su = 20 ns

  Draw the actual timing diagram, based on the data from the data sheet, for the circuit showing the signals at points A, B, and C with respect to the clock. Assume a 10 MHz clock.

## Timers and Time Bases

### 3.14
An application requires a timing signal with a 1 ms period. A 10 MHz crystal oscillator, from which the required signal can be derived, is available in the system.

- (a) Design the timing chain that will produce the required signal. Consider using a cascade of a ripple counter prescaler followed by a synchronous chain in your design.

- (b) Discuss the difficulties of designing the timer chain as a fully synchronous circuit.

- (c) Discuss the problems that can arise if the timer chain is fully asynchronous.

- (d) What is the error in the period of the 1 ms period contributed by the timer chain, excluding the oscillator error?

- (e) If the frequency of the oscillator is increased to 20 MHz, what is the effect on the error in the 1 ms period.

### 3.15
Design a timer that meets the following specifications: The timer supports the timing of two intervals, A and B. While in interval A, a high true output signal is generated signifying the interval. At the end of interval A, interval B starts, the interval A output goes false, and the interval B output goes true. At the end of interval B, both outputs go false. The timer can be started independently and can be set to count 1 to 255 input clock cycles. The input clock is a 20 MHz oscillator. The timer supports the modes Time, Stop, and Hold. When in the Time mode, the system is timing as specified. When in the Stop mode, the timer is held in its initial state. When the Hold mode, the timer is not advancing and is holding its current state.

### 3.16
An embedded application that you have been working on requires a timing generator that produces three periodic signals specified according to the timing diagram in Figure P3.7. Time units are in nanoseconds. The signals T0–T2 are not necessarily the Q outputs of flip-flops.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_221_0.png)

Figure P3.7

- In addition to the waveform specification, the specification requires that the time base will only generate the waveforms T0–T2 if the Enable input to the system is high. In executing the design,

- (a) What frequency do you choose for the clock? Why?

- (b) What is the period of your time-base unit? Why?

- (c) Please give the flip-flop equations for your time-base unit if it is implemented using D flip-flops.

- (d) Please give the logic output equations for the time-base unit to generate output signals T0–T2.

- (e) Develop and test a structural Verilog model of the time base you designed.

- (f) The vendor's specifications for the 74ALS74 D-type flip flop are given as
  - t_pdl = 15 ns
  - t_pdh = 20 ns
  - t_su = 15 ns

  The logic gates have the following delays.
  - t_pdl = 9 ns
  - t_pdh = 15 ns

  Please give a timing diagram for the signals T0–T2 that reflect the flip-flop and gate delays.

### 3.17
An embedded application requires a time base that produces a four-phase nonoverlapping periodic clock output. Each clock output must have a frequency of 10 MHz.

- (a) What input frequency do you choose? Why?

- (b) Design the time base that will produce the four outputs.

- (c) Develop and test a behavioral Verilog model of the time base for the design.

- (d) Select components for the design, and from the vendor's data sheets, identify all of the appropriate delays. Using the vendor information, give a timing diagram reflecting the operation of your design.

### 3.18
A technique called pulse width modulation (PWM) is commonly used in embedded applications as a method for controlling small motors. The PWM signal for driving the motor has a fixed frequency and a variable duty cycle. At a duty cycle of close to 0%, the motor is running at a slow speed; with a duty cycle close to 100%, the motor is running at close to full speed.

- (a) Design such a timer that can control the duty cycle of the output waveform in ± 5 % increments.

- (b) What frequency have you selected for the PWM signal? Why?

### 3.19
You have completed the design of most of a new embedded application; only the time-base unit remains to be designed. The time base has two inputs: select and clock and one output: sync. The unit has the following specifications:

- The input select clock has a frequency of 1 MHz.

- When select is a logical 0, the output signal, sync, is a 1-µsec-wide pulse with a period of 3 µsec. When select is a logical 1, the output signal, sync, is a 1-µsec-wide pulse with a period of 7 µsec.

- (a) Please draw a timing diagram for the output of the time-base unit showing its behavior when select is a logical 0.

- (b) Please draw a timing diagram for the output of the time-base unit showing its behavior when select is a logical 1. Be certain to label time units on your diagram.

- (c) Please give the flip-flop input equations if the time base is to be implemented using D flip-flops.

- (d) Please write a test behavioral Verilog model for your design.

- (e) Please show the logic diagram for your time-base unit based on your equations.

## Finite-State Machines

### 3.20
As part of a satellite system for locking on to an incoming data stream, we must design a synchronizer that operates as follows: A system accepts a serial data stream (one bit at a time) on its input and produces two outputs, Z1 and Z2. The two outputs are normally high.

The synchronizer is to operate as follows: If two consecutive input bits arriving at times t and t+1 have the values (01 or 10), output Z1 is to be in the logical 0 state. If the two consecutive input bits arriving at times t and t+1 have the values (11 or 00), output Z2 is to be in the logical 0 state. Otherwise, both outputs are to be in the logical 1 state.

When either pattern is detected, the system enters and remains in a locked state.

- (a) Draw a state diagram for such a system using a Mealy model.

- (b) Give the state and output table for such a system based on your state diagram and using a Mealy model.

- (c) Reduce the state and output table for such a system to their simplest form.

- (d) Provide a state assignment based on your reduced state and output table.

- (e) Give the equations for the two output signals, Z1 and Z2.

- (f) Write and test a behavioral Verilog model for the synchronization system.

### 3.21
A system has two inputs, serial data (DI) and a control signal (SEL), and a single output (Z) as shown in Figure P3.8.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_222_0.png)

Figure P3.8

The system has the following specifications:

- If the control input SEL is a logical 0, the system is to produce a logical 1 on the output Z at time t = t1; if the previous three input data bits had been the pattern 110. Otherwise it is to produce a logical 0 on the output.

- If the control input SEL is a logical 1, the system is to produce a logical 1 on the output Z at time t = t1; if the previous three input data bits had been the pattern 011. Otherwise it is to produce a logical 0 on the output.

- Draw a state diagram for such a system.

- Give the state and output table for such a system.

- Provide a state assignment for such a system.

- Write a test behavioral Verilog model for your design.

### 3.22
An error management system is needed as a subsystem in a new telecommunication system. As a proof of concept, we will design and build a prototype that works with 4-bit serial words. A partial block diagram for the subsystem is shown in Figure P3.9.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_222_1.png)

Figure P3.9

It operates as follows:

- Three bits of data are loaded into Register A using a load signal.
