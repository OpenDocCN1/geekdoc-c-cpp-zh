many frequency components. From Fourier analysis, the series expansion of a periodic 50% duty cycle square wave is given in Eq. (2.30).

f(x) = \frac{2}{\pi} \sum_{n=1,3,5,...}^{\infty} \frac{1}{n} \sin 2\pi n Fx
F is frequency
x is time
(2.30)

Observe that a square wave comprises components or harmonics of odd integer (n) multiples of a fundamental frequency. Each harmonic will see a different inductive impedance as it moves along the conductor. The consequences will potentially be an effect on the composite signal quality, specifically the rise times, fall times, and amplitude. Visualize an ideal digital signal entering a net. As the signal propagates, each harmonic will encounter a difference impedance and voltage drop. What will the original signal look like at its destination?

# 2.7 LOGIC CIRCUIT MODELS AND PARASITIC COMPONENTS

As embedded systems are becoming increasingly sophisticated and complex, the need to develop models that reflect and replicate real-world behavior and the supporting tools to analyze them is becoming increasingly important.

As an initial note, for the first-order models that follow, we cannot have any ringing. We will start by examining the effect of parasitic components on the behavior of a logic circuit. Our digital system, shown in Figure 2.40, comprises two black box logic circuits that we initially model using the two buffers shown. The source produces a typical digital signal such as one might find originating from a logic gate, a bus driver, or the output of a more complex device such as FPGA or microprocessor. The receiver of the signal is any similar such device

![](bbox=[0.28, 0.57, 0.88, 0.62])

# 2.7.1 First-Order RC Circuit Model

We will begin with a first-order model for the devices, the environment, and the wire interconnecting the two devices. Extending the basic logic circuit in Figure 2.40 to include parasitic resistance and capacitance, we have the circuit as shown in Figure 2.41. Because we are working with a first-order model, we are not including the parasitic inductance. Such a model plays a significant role in the first-order analyzes of typical digital circuit behavior. The results extend naturally to more complex circuits.

![](bbox=[0.28, 0.81, 0.88, 0.9])