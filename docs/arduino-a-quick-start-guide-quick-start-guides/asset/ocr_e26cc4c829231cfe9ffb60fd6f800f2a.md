![](bbox=[0.14, 0.08, 0.47, 0.27])

![](bbox=[0.52, 0.08, 0.76, 0.3])

Figure 8.7: Top and bottom of a passive infrared sensor

Nearly every object emits infrared light, and a PIR sensor (see one in Figure 8.7) measures exactly this portion of light. Detecting motion is comparatively easy if you are already able to receive the infrared radiation emitted by objects in the sensor's field of view. If the sensor receives the infrared light emitted by a wall, for example, and suddenly a human being or an animal moves in front of the wall, the infrared light signal will change.

Off-the-shelf sensors hide these details, so you can use a single digital pin to check whether someone is moving in the sensor's field of view. The Parallax PIR sensor¹⁶ is a good example of such a device, and we'll use it as the basis of our burglar alarm.

The PIR sensor has three pins: power, ground, and signal. Connect power to the Arduino's 5V supply, ground to one of the Arduino's GND pins, and signal to digital pin 2 (see a circuit diagram in Figure 8.8, on the following page). The sensor also has a jumper that you can use for changing its behavior. For our project, it has to be in position H; that is, the jumper has to cover the pin next to the H (Lady Ada has an excellent tutorial on PIR sensors).¹⁷

Then enter the following code in the Arduino IDE:

16. http://www.parallax.com/Store/Sensors/ObjectDetection/tabid/176/ProductID/83/List/0/Default.aspx
17. http://www.ladyada.net/learn/sensors/pir.html