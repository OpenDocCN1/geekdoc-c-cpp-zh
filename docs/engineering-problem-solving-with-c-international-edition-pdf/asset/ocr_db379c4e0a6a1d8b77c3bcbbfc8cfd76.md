| Time, s | Temperature, degrees F |
|---|---|
| 0.0 | 0.0 |
| 1.0 | 20.0 |
| 2.0 | 60.0 |
| 3.0 | 68.0 |
| 4.0 | 77.0 |
| 5.0 | 110.0 |

Assume that we want to interpolate a temperature to correspond to the value 2.6 seconds. We then have the following situation:

| a | 2.0 | f(a) | 60.0 |
| b | 2.6 | f(b) | ? |
| c | 3.0 | f(c) | 68.0 |

Using the interpolation formula, we have

```
f(b) = f(a) + \frac{b-a}{c-a} [f(c) - f(a)]
= 60.0 + \frac{2.6 - 2.0}{3.0 - 2.0} [68.0 - 60.0]
= 64.8.
```

In this example, we used linear interpolation to find the temperature that corresponds to a specified time. We could also interchange the roles of temperature and time so that we plot temperature on the x-axis and time on the y-axis. In this case, we can use the same process to compute the time that a specified temperature occurred, assuming that we have a pair of data points with temperatures below and above the specified temperature.

# Practice!

Assume that we have the following set of data points, which is also plotted in Figure 3.9:

| Time (s) | Temperature (degrees F) |
|---|---|
| 0.0 | 72.5 |
| 0.5 | 78.1 |
| 1.0 | 86.4 |
| 1.5 | 92.3 |
| 2.0 | 110.6 |
| 2.5 | 111.5 |
| 3.0 | 109.3 |
| 3.5 | 110.2 |
| 4.0 | 110.5 |
| 4.5 | 109.9 |
| 5.0 | 110.2 |