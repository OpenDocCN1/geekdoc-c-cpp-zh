# 3.8 PRACTICAL CONSIDERATIONS – PART 2: CLOCKS AND CLOCK DISTRIBUTION

# 3.8.1 The Source

The clock system or time base in a digital system is an essential component in ensuring proper operation. For certain hard real-time applications, having the proper time base is critical to meeting the timing specifications.

Four fundamental parameters should be considered when designing or selecting a clock system or time base. For the basic clock, these parameters are:

+   - Frequency and frequency range
+   - Rise times and fall times
+   - Stability
+   - Precision

# 3.8.1.1 Frequency.

Often we start out with a clock source that is a higher frequency than necessary. We then can use ripple counters to divide down the higher frequency to a number of lower frequencies. Remember: because ripple counters are asynchronous, one should never decode any of the state variable combinations to generate a specific frequency. Decoding spikes will occur and will have enough energy to clock flip-flops and latches at the wrong times.

phase locked loop (PLL)

Building a higher frequency from a lower one is done using a phase locked loop (PLL). The basic block diagram appears as drawn in Figure 3.44.

![](bbox=[0.2, 0.6, 0.8, 0.71])

Figure 3.44 Block Diagram for a Basic Phase Locked Loop

voltage-controlled oscillator (VCO)

The feedback signal is the output of a voltage-controlled oscillator (VCO) that is controlled by the output voltage. When the phase difference between the input signal and the output of the VCO is zero, the system has locked onto the input frequency. The output of the phase detector will be zero. A difference in phase appears as an error voltage that is filtered by the low-pass filter shown, amplified, and used to provide an input voltage to the VCO. The output of the VCO can now serve as the clock to the system time base.