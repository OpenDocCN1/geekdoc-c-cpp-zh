```
pinMode(PING_SENSOR_IO_PIN, INPUT);
return pulseIn(PING_SENSOR_IO_PIN, HIGH);
}
```

The code is nearly a perfect merge of the programs we used to get the PING))) and the TMP36 sensors working. Only a few things were changed:

+   - The constant MICROSECONDS_PER_CM has been replaced by the microseconds_per_cm() function that determines the microseconds sound needs to travel 1 centimeter dynamically depending on the current temperature.
+   - Because the current temperature will usually not change often or rapidly, we no longer measure it permanently but only once a second. We use millis() in line 8 to determine the number of milliseconds that have passed since the Arduino started. From lines 15 to 19, we check whether more than a second has passed since the last measurement. If yes, we measure the current temperature again.
+   - We no longer transfer the sensor data as floating-point numbers on the serial port but use scaled integer values instead. This is done by the scaled_value() function that rounds a float value to two decimal digits and converts it into a long value by multiplying it by 100. On the receiving side, you have to divide it by 100 again.

If you upload the program to your Arduino and play around with your hand in front of the sensor, you'll see an output similar to the following:

```
1940,2818
2914,3032
3045,34156
3005,2843
3045,2476
3085,2414
```

The output is a comma-separated list of values where the first value represents the current temperature in degree Celsius, and the second is the distance to the nearest object measured in centimeters. Both values have to be divided by 100 to get the actual sensor data.

Our little project now has two sensors. One is connected to a digital pin, while the other uses an analog one. In the next section, you'll learn how to transfer sensor data back to a PC and use it to create applications based on the current state of the real world.