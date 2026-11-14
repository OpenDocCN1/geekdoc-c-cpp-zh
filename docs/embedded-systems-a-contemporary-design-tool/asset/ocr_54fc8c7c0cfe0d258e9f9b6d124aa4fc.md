Now let's examine the conductor in Figure 2.34 that has a driven current I. If the current in a conductor changes, the magnetic flux changes thereby producing a voltage across length of conductor as indicated. The voltage induced across the wire is related to the inductance of the wire. Later we'll learn that how rapidly the current I is changing will be of significance.

![](bbox=[0.25, 0.19, 0.8, 0.31])

We can compute induced voltage as shown in Eq. (2.28).

```
V = \frac{\Delta \Phi}{\Delta t} = \frac{\Delta LI}{\Delta t} = \frac{\Delta LI}{\Delta t} = L \frac{dI}{dt} (2.28)
```

+   - L-Inductance expressed in Henrys
+   - \(\Phi\)-Magnetic flux in Webers
+   - I-Current through the conductor in Amps

As seen in Figures 2.32 and 2.33, if there is a second conductor in proximity to the first and if we have current in the second conductor, induced or driven, we will have a field from the second conductor encircling the first. Then, if the current in the second conductor changes, thereby resulting in a change in the magnetic flux, a voltage will be induced in the first conductor. Such an induced voltage is denoted cross talk or noise.

The induced voltage is computed, as we did in Eq. (2.28), with the self-inductance replaced by the mutual inductance, as shown in Eq. (2.29).

```
V = \frac{\Delta \Phi}{\Delta t} = \frac{\Delta MI}{\Delta t} = M \frac{di}{dt} (2.29)
```

+   - M-Mutual inductance expressed in Henrys
+   - \(\Phi\)-Magnetic flux in Webers
+   - I-Induced current through conductor in Amps

# 2.6 INDUCTANCE IN ACTION

As noted earlier, inductance arises whenever there is an electric current in a conductor. Analogous to the behavior of a capacitor, the current creates a magnetic field and the energy in the magnetic field is supplied by the driving source. If a voltage is applied across an inductor, initially there is no current flow. Like a voltage across a capacitor, the current does not change instantly; a magnetic field is being created that builds up over time to a steady state value; think about an electromagnet.