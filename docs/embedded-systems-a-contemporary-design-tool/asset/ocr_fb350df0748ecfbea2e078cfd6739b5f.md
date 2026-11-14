V = L_{psw} \frac{di}{dt} \quad (20.7)
V_{noise} = L_{psw} (\frac{di}{dt})_{max} = (186 \text{ nH})(1.5 \times 10^7 \text{ amps/second}) = 2.8 \text{ V}

Looking at Eq. (20.7), three factors contribute to the noise voltage:

+   1. L_{psw}
+   2. di
+   3. dt

The current and time are inherent in the design. Little can be done with these two terms. Reducing the parasitic inductance of the PSW appears to offer the best opportunity. Since that inductance is a function of the wire length, if we can reduce the length of the path through which the switching currents have to flow, we should be able to reduce the corresponding path inductance and, thus, the level of the noise voltage.

We can reduce the path length several ways. We can simply shorten the wire between the power supply and the system. Such an approach is often impractical. Alternatively, we can provide a source of current closer to the demand.

From our basic electronics, we know that a capacitor can store charge and can be made to release that charge. Thus, to bring the source of current closer to the demand, we will install a capacitor, C_2, as shown in Figure 20.7, to meet the short-term switching current demands from the components on the PCB. We assume that the power supply is not on the PCB and that C_2 is installed on the PCB, generally at the card edge.

![](bbox=[0.25, 0.5, 0.75, 0.7])

Figure 20.7 Board Level Capacitor.

Observe in Figure 20.7 that by installing the board level bypass capacitor C_2, we have split the original current path and thus the parasitic inductor, L_1, into two pieces. The path to the switching device is now substantially shorter and the L_1A piece must be smaller than the original L_1. Therefore, we will have a smaller inductor to deal with and a smaller inductive noise voltage drop.

If the impedance of C_2 is lower than that of the PSW, from Kirchoff's current law (KCL), as illustrated in Figure 20.8, the majority of charging current for C_1 will flow from C_2, along a shorter path rather than through the longer system PSW.