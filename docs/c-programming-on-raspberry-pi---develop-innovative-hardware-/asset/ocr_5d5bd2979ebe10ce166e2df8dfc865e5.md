# Block diagram:

Figure 5.39 shows the block diagram of the project.

![](bbox=[0.35, 0.26, 0.75, 0.44])

Figure 5.39 Block diagram of the project

# Circuit diagram:

In this project, the DHT11 relative humidity and temperature sensor chip is used. The standard DHT11 is a 4-pin digital output device (only 3 pins are used) as shown in Figure 5.40, having pins +V, GND, and Data. The Data pin must be pulled-up to +V through a 10K resistor. The chip uses a capacitive humidity sensor and thermistor to measure ambient temperature. Data output is available from the chip approx. every second. The basic features of the DHT11 are:

+   - 3 to 5V operation.
+   - 2.5mA current consumption (during a conversion).
+   - Temperature reading in the range 0-50°C with an accuracy of ±2°C.
+   - Humidity reading in the range 20-80% with 5% accuracy.
+   - Breadboard compatible with 0.1-inch pin spacing.

![](bbox=[0.45, 0.9, 0.6, 0.98])

Figure 5.40 The standard DHT11 chip

In this example, the DHT11 module with a built-in 10K pull-up resistor, available from Elektor, is used. This is a 3-pin device with a pin layout shown in Figure 5.41.