substantially more current than the standard gates and are available as either inverting or noninverting drivers.

Assume that the application specifies that an annunciation be given when a certain event is TRUE. If we assume the event is an active HIGH or HIGH TRUE signal, then the inverting device should be selected. The schematic in Figure 17.36 illustrates the design of the annunciator. The resistor is incorporated to limit the current through the LED, which ranges from 20 to 60 mA. With LEDs, as the current level is increased, the brightness does as well.

![](bbox=[0.28, 0.22, 0.45, 0.32])

Figure 17.36 Controlling an LED using Cathode Drive

# 17.11.2 Multi-LED Displays

The ubiquitous seven-segment or numeric display simply combines a number of individual LEDs into a package with an appropriate lens to enable the display of any of the 10 decimal digits (plus decimal points) when the proper LEDs are illuminated. A top view of the device and several possible digits is shown in Figure 17.37.

![](bbox=[0.25, 0.46, 0.65, 0.56])

Figure 17.37 A Three-Digit LED Display

The LEDs within the display are connected in either a common anode or a common cathode configuration. Simply put, either all the anodes are connected together and the drive signal is applied to the individual cathodes or vice versa as depicted in Figure 17.38 (omitting the decimal points).

![](bbox=[0.25, 0.67, 0.6, 0.75])

Figure 17.38 Seven-Segment LED Display Configurations

# BCD to Seven-Segment Decoder

To drive the device, a Medium-Scale Integrated (MSI) part called a Binary Coded Decimal (BCD) to Seven-Segment Decoder can be used. As the name suggests, the part takes four input signals, encoded as a BCD number, and produces seven output signals. If those signals are connected to a seven-segment display as shown in Figure 17.39, the proper LEDs will turn on to display the corresponding BCD number. The decimal points, if necessary, would be controlled separately.