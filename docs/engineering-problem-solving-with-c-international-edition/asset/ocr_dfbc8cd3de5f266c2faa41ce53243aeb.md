During a test flight of an open-rotor aircraft, the test pilot has set the engine power level at 40,000 newtons, which causes the 20,000-kg aircraft to attain a cruise speed of 180 m/s (meters/second). The engines throttles are then set to a power level of 60,000 newtons, and the aircraft begins to accelerate. As the speed of the plane increases, the aerodynamic drag increases in proportion to the square of the airspeed. Eventually, the aircraft reaches a new cruise speed where the thrust from the engines is just offset by the drag. The equations used to estimate the velocity and acceleration of the aircraft from the time that the throttle is reset until the plane reaches its new cruise speed (at approximately 120 s) are as follows:

```
Velocity = 0.00001 time^3 - 0.00488 time^2
           + 0.75795 time + 181.3566,

Acceleration = 3 - 0.000062 velocity^2.
```

Plots of these functions are shown in Figure 2.8. Note that the acceleration approaches zero as the velocity approaches its new cruise speed.

Write a program that asks the user to enter a time value that represents the time elapsed (in seconds) since the power level was increased. Compute and print the corresponding acceleration and velocity of the aircraft at the new time value.

![](bbox=[0.26, 0.47, 0.89, 0.66])

![](bbox=[0.26, 0.68, 0.89, 0.86])

Figure 2.8 Aircraft velocity and acceleration.