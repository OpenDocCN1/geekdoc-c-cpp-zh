A simple example project is given in the next section using 3 threads to flash 3 LEDs at different rates.

# 12.9 • Project 6 – Multi-threading - flashing 3 LEDs at different rates

# Description:

In this project, 3 LEDs named LEDA, LEDB, and LEDC are connected to the Raspberry Pi.

The LEDs flash concurrently at the following rates:

+   - LEDA: every second
+   - LEDB: every 500ms
+   - LEDC: every 250ms

# Block diagram:

Figure 12.14 shows the block diagram of the project.

![](bbox=[0.3, 0.55, 0.75, 0.78])

Figure 12.14 Block diagram of the project

# Circuit diagram:

The circuit diagram of the project is shown in Figure 12.15. LEDA, LEDB, and LEDC are connected to GPIO 16, GPIO 20, and GPIO 21 respectively through 470 Ohm resistors.

![](bbox=[0.35, 0.7, 0.65, 0.9])

Figure 12.15 Circuit diagram of the project