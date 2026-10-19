Because all frequencies below the cutoff frequency ω_c are passed with unit amplitude, while all higher frequencies are blocked, we can see the importance of a sinc filter.

In practice, there are a number of problems in using sinc function as the filter. First, as formulated, the filter is noncausal; that is, there are coefficients at negative times, which is nonphysical because we do not start measuring the signal until t = 0. Second, in order to produce a perfect rectangular response, we would have to sample the signal at an infinite number of times. In practice, we sample at (M + 1) points (M even) placed symmetrically around the main lobe of sin(πt)/πt, and then shift times to purely positive values via

```
h[i] = sin[2π ω_c (i − M/2)] / (i − M/2) ,   0 ≤ t ≤ M .    (12.78)
```

As might be expected, a penalty is incurred for making the filter discrete; instead of the ideal rectangular response, we obtain some Gibbs overshoot, with rounded corners and oscillations beyond the corner.

There are two ways to reduce the departures from the ideal filter. The first is to increase the length of times for which the filter is sampled, which inevitably leads to longer compute times. The other way is to smooth out the truncation of the sinc function by multiplying it with a smoothly tapered curve like the Hamming window function:

```
w[i] = 0.54 − 0.46 cos(2π i / M) .    (12.79)
```

In this way, the filter's kernel becomes

```
h[i] = sin[2π ω_c (i − M/2)] / (i − M/2) [0.54 − 0.46 cos( 2π i / M )] .    (12.80)
```

The cutoff frequency ω_c should be a fraction of the sampling rate. The time length M determines the bandwidth over which the filter changes from 1 to 0.

Exercise Repeat the exercise that added random noise to a known signal, this time using the sinc filter to reduce the noise. See how small you can make the signal and still be able to separate it from the noise.