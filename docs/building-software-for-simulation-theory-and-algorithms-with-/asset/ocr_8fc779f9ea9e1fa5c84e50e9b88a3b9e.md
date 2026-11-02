![](bbox=[0.05, 0.08, 0.95, 0.48])

FIGURE 5.9 Tank spinning in place with the duty ratios at 100% for each motor, but working in opposite directions.

windings, thereby reducing the torque acting on the tank. In the instant before the tracks stick, viscous friction opposes the motors with a counterforce of about 0.02 N. After the tracks stick, this friction vanishes, and so does the counterforce. The motors and gears, their energy undiminished by the sudden transition, now apply torque sufficient to again overcome the sticking friction of the tracks, causing the tank to turn. High-speed switching between turning and not turning continues for 0.75 s until resistance in the motors, gearbox, and tracks removes enough energy to end the cycle.

Is this rapid switching an accurate portrayal of a real turn? Probably not. A more comprehensive analysis will likely to reveal a better model in this respect (see, e.g., Mosterman’s and Biswas’s discussion of this issue [90, 91]). The validity of the model, however, is undiminished by this curious phenomenon. The real tank and its model handle so sluggishly that the slight prolongation of a turn is unnoticeable to the driver; and the efficiency calculations that relate the frequency of the voltage and the consumption of power are calculated for straight-line motion. The issue must be revisited, however, if the model’s scope of use is expanded at some later time.

# 5.6.2 A Simplified Model of the Motor

The corrected Euler integrator is adequate to construct the power-frequency plot shown in Figure 2.12 and for simulating single maneuvers like the ones above. However, the step size required for even a modest error tolerance of 10⁻² ranges over five orders of magnitude, from 10⁻⁹ when the tank is accelerating to 10⁻⁴ as it trundles along at constant speed. The small step required for maneuvering makes this simulator impractical for interactive use.