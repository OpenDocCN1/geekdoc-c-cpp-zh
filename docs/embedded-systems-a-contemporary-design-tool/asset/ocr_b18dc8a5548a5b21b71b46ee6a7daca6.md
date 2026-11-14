![](bbox=[0.27, 0.08, 0.63, 0.33])

Figure 3.47 Timing Diagram Illustrating the Accumulation of Delays in an Asynchronous Ripple Counter

# 3.8.1.2 Precision and Stability

The simplest kinds of clock sources use resistor and capacitor combinations to set their output frequency. Although such devices may be perfectly reasonable for controlling windshield wipers or a door bell, they should never be used in critical hard real-time applications. Capacitors have wide tolerances and are subject to humidity, brownout, or low-voltage levels, as well as a number of environmental effects.

Crystal-based sources are generally the best solution for stable and accurate timing signals. When using such devices, one can start either with the basic crystal and then design the analog electronics necessary to implement the desired oscillator or buy a prepackaged oscillator. Each crystal or oscillator has different stability and accuracy specifications. If the application demands greater accuracy and stability than are available with standard devices, the next step is to use temperature-compensated designs. Such sources utilize a small heater to minimize the effects of temperature variation of the oscillator.

# 3.8.2 Designing a Clock System

# 3.8.2.1 Single-Phase Clocks

A single-phase clock should start with the crystal oscillator. Such an approach gives stability and repeatability to any clocking and timing that need to be in the embedded application. Variations on the circuit in Figure 3.48 should never be used.

![](bbox=[0.28, 0.72, 0.5, 0.82])

Figure 3.48 A Simple Clock Generator

The design is trying to do a digital job with analog parts. Adding the R and C as shown can significantly affect the rise and fall times of the input signals to the buffer. As the transition times increase, so does the probability of the circuit becoming metastable.