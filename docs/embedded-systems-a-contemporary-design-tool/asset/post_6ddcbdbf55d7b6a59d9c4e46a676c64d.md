
![](img/679b8d2d47f1bf86e17aca48f596f5cc_580_0.png)

![](img/679b8d2d47f1bf86e17aca48f596f5cc_580_1.png)

When working with passive electronic parts such as resistors, inductors, or small valued capacitors, one is generally not concerned with part orientation. Of major concern with these devices is making certain that the part with the correct value and proper power rating for the application is installed.

During design, make certain to do a wattage calculation in addition to a value calculation for each part. One must go beyond the familiar I²R calculation. A check of the vendor's data sheets will reveal that there are specifications for AC power, DC power, and pulsed power. These are different and one must use the appropriate specifications for the specific application.

Electrolytic capacitors are polarized; it is very important that they be installed in the circuit with the correct orientation. However, installing them backwards is definitely more interesting. Under such circumstances, and with a sufficiently high voltage applied, they will explode. Such a mistake generally does not impress people who are working around you. However, prior to exploding they are known to give off some marvelous smoke, the color of which depends on the type of dielectric used.

Electrolytic capacitors are marked with a + on the positive lead or a series of rings, or indentation near the negative end. Some of the larger devices will have a small cross on the top. Don't confuse this with the plus sign. This is a blowout hole in case the device has been installed improperly and the smoke demon manages to extricate itself. The capacitor internals vent through this port rather than allowing the device to send shrapnel throughout the laboratory or factory, which is even less impressive.

Make certain that the proper current limiting is provided for all LEDs used in the system. Without the proper current-limiting resistors, the devices may burn out shortly after power is applied.

## 10.10.2 Initial Tests and Measurements – Before Applying Power

We are almost ready to apply power to the circuit for the first time. Before doing so, however, we should check a couple of more things. It is assumed that before the circuit was actually built the impedance between any of the power rails and ground was measured and that these all showed open. That measurement is repeated after the parts have been installed.

One may get several possible results. The measurement could still yield an open or very high-valued measurement. If such is the case, power has not been properly connected to the components; that must be corrected before proceeding. If the measurement shows less than 5Ω, then there is a strong possibility of a short or very low-impedance path between the two rails. Once again must also be corrected prior to moving on. Applying the voltage and raising the current limit in hopes that the short will go away are challenging to the smoke demon. Don't do it. The measurement should be greater than approximately 10-15 Ω and less than 10 KΩ.

When making such a measurement, one may encounter an interesting phenomenon. The impedance initially reads 10-15 Ω and then begins to increase. Such behavior is easily explained. Most modern multimeters measure resistance by injecting a known current into the circuit and then making a voltage measurement across the port. By properly selecting the magnitude of the injected current, the voltage that read corresponds directly to the resistance. An increasing resistance value is reflecting the result of the measurement current charging capacitors inside the system.

Finally, when using bench supplies while debugging, remember to check the current limit and voltage settings on the supplies.

## 10.10.3 Initial Tests and Measurements – Immediately After Applying Power

Power is now on the system. What to look for first is smoke or fire, of course. If some wiring problems have escaped early scrutiny and are now causing problems, turn the power off quickly. With smoke and fire, there is generally a good indication of the source of the problem. Put the fire out and get the problem fixed first before proceeding.

Next, check the current that is being drawn. Use either the meter on the bench power supply or a separate instrument. The amount of current circuit is consuming gives a strong early indication of potential problems with the system. What should be a reasonable level?

“Reasonable” depends on the kind of logic being used (TTL or CMOS), how many parts are in the system, the voltage level, and whether or not there are clocks (unused) inputs among other things. Let’s establish a base line. Assume that the system has approximately 25-30 ICs comprising a mix of small-scale integrated (SSI), medium-scale integrated (MSI), and a couple of small programmable logic devices. For a TTL design, the current should be in the range of 1–2 A. For a CMOS design, one should measure less than 1 A. If the measurement shows a very low value (close to 0 A), then it can be assumed that power is not properly connected to the system. On the other hand, an excessive value indicates a potential wiring error, an improper part, or a part installed incorrectly.

For CMOS logic in particular, one should always define the inputs of unused gates. If the inputs are not defined, the unused gates may be partially turned on and actually draw more current than the remainder of the circuit. If circuit includes a number of LEDs or seven segment displays, each LED is going to draw about 5–15 mA. So, each seven-segment LED display may contribute around 100 mA or more to the power budget.

If the amount of current the circuit is drawing is within the range of what is expected, one should next check the temperature of the components. Feel the board and look for hot spots. These are an indication of incorrect wiring, incorrect parts, or a part that is improperly installed. Once again, it is important to have a heuristic feel for what the temperature of the components should be.

If you are working with a TTL board and it is cold, then there is a problem. It is most likely not powered or does not have power connected to all parts of the circuit. If a component feels as hot as a 20–40 W light bulb, then it is too hot. A normal CMOS board should feel about the same temperature as the surface of the laboratory bench. A TTL board should be a bit cooler than a morning coffee or tea cup.

## 10.11 APPLYING THE STRATEGY – DEBUGGING AND TESTING

The module or system now has power applied and we can begin to execute our various test cases to confirm its operation. In the next several sections, we will begin by identifying some of the places to start to look for gross problems. Then we will move through some strategies for debugging combinational and sequential logic circuits.

### 10.11.1 The Reset System

Every system should incorporate a Power ON Reset (POR) signal. Starting any system in a known state is simply good engineering practice. During the debugging phase, every prototype module should provide manual access and control of the POR signal. On initial application of power, the unit being tested should be held in the reset state, and the initial values of the available state variables should be confirmed prior to further testing and debugging. Such a practice enables one to always start the process from a known point.

As testing starts to progress, the first step in debugging nonfunctioning sequential logic is to confirm that the POR signal is in the non-reset state.

### 10.11.2 The Clocks and Timing

During the debug phase, one may be using a bench function generator or an oscillator that is built into the system. When using a bench source, prior to connecting it to the circuit, make sure that it is configured properly. Always check the level and offset of the signal. One should always do this with an oscilloscope. The first measurement should be to verify where ground is set on the scope.

In either case, make certain that the clock is operational and that the frequency and amplitude are correct. Remember that a current limit (fan-out) applies to the clock as well. Check the rise and fall times to verify that they are within the desired limits. If the clock is too heavily loaded, the rise and fall times will be long and the risk that the parts will enter a metastable region during switching will increase. Finally, make certain that the clock is connected to all the appropriate parts.

### 10.11.3 The Inputs and Outputs

The next step is to move to the heart of the testing and debugging process, confirming the behavior of the system. The key to confirming system behavior is to fully understand what the behavior should be. Although such a statement may seem obvious to the system designer, this simple statement gives most people the greatest difficulty when debugging. What is meant here is that one must know what output value to expect for each selected input combination.

One cannot know whether or not the set of input signals accomplished anything meaningful without knowing what they were intended to demonstrate. Furthermore, any disagreement between the anticipated and actual results can provide the first clue toward identifying the root cause of the discrepancy.

Although the heuristic holds throughout the testing and debugging phase, the initial steps, in particular, should start with a small portion of the system using as simple an input or set of inputs as possible. Ideally, the input set should be DC signals, a repeating time-varying signal, or a known transient. One should remember that a failure during the debugging process should lead to a shift in strategy from ensuring behavior of the design to identifying the root cause of the fault.
