# 10.11 APPLYING THE STRATEGY – DEBUGGING AND TESTING

The module or system now has power applied and we can begin to execute our various test cases to confirm its operation. In the next several sections, we will begin by identifying some of the places to start to look for gross problems. Then we will move through some strategies for debugging combinational and sequential logic circuits.

# 10.11.1 The Reset System

Every system should incorporate a Power ON Reset (POR) signal. Starting any system in a known state is simply good engineering practice. During the debugging phase, every prototype module should provide manual access and control of the POR signal. On initial application of power, the unit being tested should be held in the reset state, and the initial values of the available state variables should be confirmed prior to further testing and debugging. Such a practice enables one to always start the process from a known point.

As testing starts to progress, the first step in debugging nonfunctioning sequential logic is to confirm that the POR signal is in the non-reset state.

# 10.11.2 The Clocks and Timing

During the debug phase, one may be using a bench function generator or an oscillator that is built into the system. When using a bench source, prior to connecting it to the circuit, make sure that it is configured properly. Always check the level and offset of the signal. One should always do this with an oscilloscope. The first measurement should be to verify where ground is set on the scope.

In either case, make certain that the clock is operational and that the frequency and amplitude are correct. Remember that a current limit (fan-out) applies to the clock as well. Check the rise and fall times to verify that they are within the desired limits. If the clock is too heavily loaded, the rise and fall times will be long and the risk that the parts will enter a metastable region during switching will increase. Finally, make certain that the clock is connected to all the appropriate parts.

# 10.11.3 The Inputs and Outputs

The next step is to move to the heart of the testing and debugging process, confirming the behavior of the system. The key to confirming system behavior is to fully understand what the behavior should be. Although such a statement may seem obvious to the system designer, this simple statement gives most people the greatest difficulty when debugging. What is meant here is that one must know what output value to expect for each selected input combination.

One cannot know whether or not the set of input signals accomplished anything meaningful without knowing what they were intended to demonstrate. Furthermore, any disagreement between the anticipated and actual results can provide the first clue toward identifying the root cause of the discrepancy.

Although the heuristic holds throughout the testing and debugging phase, the initial steps, in particular, should start with a small portion of the system using as simple an input or set of inputs as possible. Ideally, the input set should be DC signals, a repeating time-varying signal, or a known transient. One should remember that a failure during the debugging process should lead to a shift in strategy from ensuring behavior of the design to identifying the root cause of the fault.