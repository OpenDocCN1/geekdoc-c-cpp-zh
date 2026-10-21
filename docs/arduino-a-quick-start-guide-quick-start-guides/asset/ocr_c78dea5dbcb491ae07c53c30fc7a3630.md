![](bbox=[0.24, 0.06, 0.66, 0.51])

Figure 6.3: How to connect an ADXL335 sensor to an Arduino

Our test program is as simple as it can be. We define constants for the three analog pins and initialize the serial port in the setup() function. Note that we did not set the analog pins to INPUT explicitly, because that's the default anyway.

In the loop() function, we constantly output the values we read from the analog pins to the serial port. Open the serial monitor, and move the sensor around a bit—tilt it around the different axes. You should see an output similar to the following:

```
344 331 390
364 276 352
388 286 287
398 314 286
376 332 289
370 336 301
379 338 281
```