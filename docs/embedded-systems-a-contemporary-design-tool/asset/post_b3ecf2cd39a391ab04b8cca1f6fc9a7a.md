
Now let's examine the conductor in Figure 2.34 that has a driven current I. If the current in a conductor changes, the magnetic flux changes thereby producing a voltage across length of conductor as indicated. The voltage induced across the wire is related to the inductance of the wire. Later we'll learn that how rapidly the current I is changing will be of significance.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_144_0.png)

We can compute induced voltage as shown in Eq. (2.28).

```
V = \frac{\Delta \Phi}{\Delta t} = \frac{\Delta LI}{\Delta t} = L \frac{dI}{dt} (2.28)
```

- L-Inductance expressed in Henrys
- \(\Phi\)-Magnetic flux in Webers
- I-Current through the conductor in Amps

As seen in Figures 2.32 and 2.33, if there is a second conductor in proximity to the first and if we have current in the second conductor, induced or driven, we will have a field from the second conductor encircling the first. Then, if the current in the second conductor changes, thereby resulting in a change in the magnetic flux, a voltage will be induced in the first conductor. Such an induced voltage is denoted cross talk or noise.

The induced voltage is computed, as we did in Eq. (2.28), with the self-inductance replaced by the mutual inductance, as shown in Eq. (2.29).

```
V = \frac{\Delta \Phi}{\Delta t} = \frac{\Delta MI}{\Delta t} = M \frac{dI}{dt} (2.29)
```

- M-Mutual inductance expressed in Henrys
- \(\Phi\)-Magnetic flux in Webers
- I-Induced current through conductor in Amps

## 2.6 INDUCTANCE IN ACTION

As noted earlier, inductance arises whenever there is an electric current in a conductor. Analogous to the behavior of a capacitor, the current creates a magnetic field and the energy in the magnetic field is supplied by the driving source. If a voltage is applied across an inductor, initially there is no current flow. Like a voltage across a capacitor, the current does not change instantly; a magnetic field is being created that builds up over time to a steady state value; think about an electromagnet.

Given the circuit in Figure 2.35 with the accompanying waveforms in Figure 2.36, if a voltage step V_s(t) is applied, initially no current flows, thus I(t) is 0. With no current flowing, the output voltage will be V_s(t). As a result, initially the inductor looks like an open circuit. As the current builds up, the current flow increase leads to a decrease in the output voltage. As a result, in the steady state, the inductor looks like short circuit as we learned earlier.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_145_0.png)

![](img/679b8d2d47f1bf86e17aca48f596f5cc_145_1.png)

### 2.6.1 Wires and Conductors

As we learned earlier, a wire or conductor is a special case of a resistor. Thus, our earlier analysis of a resistor applies to other conductors as well. Recall the basic discrete resistor model, repeated here as Figure 2.37. Our earlier analysis focused on resistive component and recognized the inductive and capacitive effects. We will now examine inductor in greater detail.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_145_2.png)

From our earlier discussion, current flowing in a conductor produces a magnetic field and the magnetic field leads to inductance. Now, consider the end view of a conductor depicted in Figure 2.38 and illustrated by the left hand circle. Let a current in the conductor

![](img/679b8d2d47f1bf86e17aca48f596f5cc_145_3.png)

flow into page. This will produce rings of flux as shown in the right hand diagram. Some of the flux will be inside conductor and some of flux will be outside conductor.

First, from fundamental electrical physics, we know that current is the movement of electrons. We now raise the question: where are those electrons? Are they uniformly distributed within the conductor?

Flux density is determined by the amount of enclosed current (flowing electrons). The flux outside of the conductor encloses all of the current flowing through the conductor; it does not depend upon the distribution or frequency of the current within the conductor. In contrast, inside the conductor, if the current distribution or frequency changes, the flux distribution will correspondingly change.

With a DC current moving through the conductor, the current (electrons) will be uniformly distributed through the body of the conductor. However, currents closer to the center of the conductor will have greater flux density per Amp of current and, therefore, higher self-inductance than those nearer the outside. At DC, the inductive impedance will be zero. With an AC current moving through the conductor, the picture changes – several things come into play:

- Because inductive impedance is a direct function of frequency, increasing frequency leads to increasing impedance.
- For a given frequency, paths with the highest inductance will have the highest impedance.
- From basic electromagnetic physics, current will seek to travel along path with the lowest impedance.
- Since the center of the conductor has the highest impedance, the current (the electron flow) will tend to migrate away from the center toward the periphery of the conductor, which will be a lower impedance.

As the signaling frequency increases, the difference in inductive impedance between the inner and outer paths increases. The current distribution changes such that the largest density is near surface of conductor. That is, the current flows mainly in what is called the *skin* of the conductor. Such a phenomenon called the *skin effect*.

The skin is region of the conductor between the conductor surface and an internal level called the *skin depth*, as illustrated in Figure 2.39. Such an effect can significantly alter the impedance of the conductor and also alter the self-inductance, but to a lesser extent.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_146_0.png)

Figure 2.39 Skin Depth

The above analysis tacitly assumes a sinusoidal (analog) signaling waveform. Such a signal has single frequency. In the digital world, the problem becomes more complex. Digital signals approximate square waves, which are *wide band signals*, i.e. they contain many frequency components. From Fourier analysis, the series expansion of a periodic 50% duty cycle square wave is given in Eq. (2.30).

f(x) = \frac{2}{\pi} \sum_{n=1,3,5,...}^{\infty} \frac{1}{n} \sin 2\pi n Fx
F is frequency
x is time
(2.30)

Observe that a square wave comprises components or harmonics of odd integer (n) multiples of a fundamental frequency. Each harmonic will see a different inductive impedance as it moves along the conductor. The consequences will potentially be an effect on the composite signal quality, specifically the rise times, fall times, and amplitude. Visualize an ideal digital signal entering a net. As the signal propagates, each harmonic will encounter a difference impedance and voltage drop. What will the original signal look like at its destination?

## 2.7 LOGIC CIRCUIT MODELS AND PARASITIC COMPONENTS

As embedded systems are becoming increasingly sophisticated and complex, the need to develop models that reflect and replicate real-world behavior and the supporting tools to analyze them is becoming increasingly important.

As an initial note, for the first-order models that follow, we cannot have any ringing. We will start by examining the effect of parasitic components on the behavior of a logic circuit. Our digital system, shown in Figure 2.40, comprises two black box logic circuits that we initially model using the two buffers shown. The source produces a typical digital signal such as one might find originating from a logic gate, a bus driver, or the output of a more complex device such as FPGA or microprocessor. The receiver of the signal is any similar such device

![](img/679b8d2d47f1bf86e17aca48f596f5cc_147_0.png)

### 2.7.1 First-Order RC Circuit Model

We will begin with a first-order model for the devices, the environment, and the wire interconnecting the two devices. Extending the basic logic circuit in Figure 2.40 to include parasitic resistance and capacitance, we have the circuit as shown in Figure 2.41. Because we are working with a first-order model, we are not including the parasitic inductance. Such a model plays a significant role in the first-order analyzes of typical digital circuit behavior. The results extend naturally to more complex circuits.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_147_1.png)
