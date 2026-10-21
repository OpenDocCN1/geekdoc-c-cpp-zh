![](bbox=[0.21, 0.11, 0.66, 0.61])

# Figure 5.5: Photo of PING))) basic circuit

+   - *timeout*: Timeout measured in microseconds. If no pulse could be detected within the timeout period, pulseIn() returns 0. This parameter is optional and defaults to one second.

Note that in the whole process only one pin is used to communicate with the PING))). Sooner or later, you will realize that IO pins are a scarce resource on the Arduino, so it's really a nice feature that the PING))) uses only one digital pin. When you can choose between different parts performing the same task, try to use as few pins as possible.