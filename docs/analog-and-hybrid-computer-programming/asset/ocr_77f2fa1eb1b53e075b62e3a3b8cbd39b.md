![](bbox=[0.28, 0.1, 0.7, 0.28])

Fig. 5.22. Behaviour of the precision limiter circuit

not really "flat" – they exhibit some slope that may be detrimental to the overall setup using this limiting function.

A much better limiter circuit is shown in figure 5.21. At its heart is a diode bridge which is controlled by two voltages representing the upper and lower limits. The two resistors should be about a tenth of the value of the input resistor of the inverter following the bridge circuit. This circuit exhibits excellent flatness of its output signal in the limited state, as shown in figure 5.22, and is highly recommended.

A very simple, yet often practical limiter circuit just employs two suitable ZENER-Diodes with their cathodes (or anodes) connected between the output of a summer or integrator and its respective summing junction.

# 5.9 Dead-space

Many mechanical systems, such as gear trains, linkages etc., exhibit a phenomenon called backlash, which is caused by unavoidable gaps between moving parts. A dead-space circuit is used to model this behaviour on an analog computer.

The literature contains a plethora of such circuits – the basic idea is to use a pair of suitably forward-biased diodes feeding a summer. The simplest form of such a circuit consists of just two diodes, two free potentiometers and a summer. This simplicity comes at a cost because the setup of the potentiometers is not straightforward, and the diodes are far from being ideal.

The circuit shown in figure 5.23 replaces these two real diodes by idealized diodes as shown in section 5.6. The parameters r and l define the right and left break-point of the dead-space. It may be necessary to parallel the two diodes connected to the summing junctions of their associated open amplifiers with small capacitors to avoid unstable behaviour of the circuit.

Figure 5.24 shows the behaviour of this dead-space setup. A linear voltage ramp was used for input. The left and right gradient of the curve are determined by the weights w_r and w_l of the output summer's inputs.