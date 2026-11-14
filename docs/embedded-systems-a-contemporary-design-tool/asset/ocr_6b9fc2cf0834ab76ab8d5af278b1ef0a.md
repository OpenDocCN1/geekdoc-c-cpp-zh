![](bbox=[0.26, 0.08, 0.73, 0.18])

Figure 21.37 Source Termination Reflections

# 21.5 DIFFERENTIAL SIGNALING

In contrast to single-ended signaling, differential signaling uses two wires rather than one to send the signal. The earlier analysis of the PCB environment developed for single-ended signaling applies to differential signaling as well. The main advantage of differential signaling is superior noise immunity.

# 21.5.1 Environment

The differential signaling environment appears as in Figure 21.38. Any noise will affect both of the two transmission lines with signals of the same polarity. The receiver, however, sees a voltage difference between the two transmission lines in the differential pair, thereby algebraically eliminating the noise. As a consequence, the differential configuration can reject such common mode signals as crosstalk, power supply noise, and certain kinds of switching noise.

+   - Crosstalk
+   - Power Supply Noise
+   - Switching Noise

![](bbox=[0.28, 0.5, 0.62, 0.55])

Figure 21.38 Differential Signal Model

The inherent noise immunity and high gain of the differential amplifier reduce the sensitivity to signal attenuation and permit lower signal levels. The approach improves switching speeds, reduces power consumption, reduces net magnetic flux fields radiated by opposite polarity signals, and cancels out reducing far-field EMI.

# 21.6 SIGNALS IN THE NONIDEAL (REAL) WORLD

The design of digital and embedded systems lives in the nonideal, real world. As we begin a design, we often work with ideal signals. Now let's identify and examine several basic metrics used to characterize signals in the nonideal, real world; that is, signals used in the design of high-speed digital systems. Violations of such metrics refer to waveform distortions severe enough to violate timing requirements and potentially physically damage or destroy input circuitry on receiving devices. We'll begin with four basic metrics defined as stubs, ringback, nonmonotonic edges, and return path discontinuities.