Initial conditions:
y(n - 1) = sin(ωnT)
y(n - 2) = sin(ω(n - 1)T)
(9.4)

Our problem is that we do know the new frequency, ω, and since the sample rate is also known, then we also know ωT, but we don't know what sample interval n we are on. However, we can figure it out as follows:

+   * Take the inverse sin of the y(n - 1) delay element.
+   * Find the value of n by dividing it by ωT.
+   * arcsine() returns a value between -π/2 to +π/2 which is the rising edge of the sinusoid like the original initial conditions.
+   * If we are on the rising edge, calculate the new y(n - 2) value as sin((n - 1)ωT).
+   * If we are on the falling edge, calculate the new y(n - 2) value as sin((n + 1)ωT).

It is simple to change in the cookFrequency() function as follows, so make the change in your code. Note the use of commenting out the original initial condition code in case you want to refer to it later. Also note the logic to see if we are rising or falling. We need this because the arcsine() function only returns the angle for half a sinusoid. If you think about it, this makes sense. If you give it a value of 0.707, it can't tell if the angle is 45 degrees or 135 degrees, both of which produce a sine of 0.707.