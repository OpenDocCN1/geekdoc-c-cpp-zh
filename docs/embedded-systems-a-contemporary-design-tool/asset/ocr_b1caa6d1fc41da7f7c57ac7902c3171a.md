Taking the inverse Laplace transform yields:

V_out(t) = e^(-1/RC t) (2.37)

which we plot as Figure 2.45. Plots of the first-order currents will have opposite waveforms.

![](bbox=[0.275, 0.18, 0.865, 0.355])

# 2.7.3 Second-Order Series RLC Circuit Model

We noted earlier that first-order circuits cannot ring. Second-order circuits, however, can. In the real world, such ringing is a side effect of parasitic inductance and capacitance. In analyzing such circuits, we will begin by following that for a first-order circuit. Once again, we will use a circuit model representing one signal path in a bus. The driver and interconnect network can now be modeled as shown in Figure 2.46.

![](bbox=[0.28, 0.54, 0.79, 0.57])

Now we extend the first-order interconnect model by adding a parasitic inductance. With the addition of the inductor, we now have a second-order circuit. Figure 2.47a shows the extended model and Figure 2.47b the resulting circuit model. The modeled capacitor

![](bbox=[0.28, 0.7, 0.815, 0.845])