![](bbox=[0.18, 0.01, 0.82, 0.22])

Figure 11.3: The resonances of a room all contribute to create the final frequency response. When the bandwidths of the modes overlap, they fuse together. The dotted line represents the combined frequency response.

# Schroeder's rules for natural reverb:

+   - Echo density: At least 1000 echoes/sec (Greisinger: 10,000 echoes/sec)
+   - Modal density: At least 0.15 eigenfrequencies/Hz

In physical rooms we know that:

+   - Echo density increases with the square of time.
+   - Modal density increases with the square of frequency.

```
D_m = \frac{4\pi V_R f_m^2}{c^3} \quad (11.5)
```

where

$V_R = \text{volume of the room}$
$f_m = \text{modal frequency in question}$

The energy decay relief plot (or EDR) shows how the energy decays over both frequency and time for a given impulse response of a room. Figure 11.4 shows a very simple fictitious EDR.

In Figure 11.4, notice that the frequency axis comes out of the page; low frequencies are in the back. It also shows that this room has a resonant peak, which forms almost right away in time. In an EDR, the modal density is shown across the z-axis (frequency) while the echo density appears across the x-axis (time). This simplified plot shows just one resonance and no echo density build-up for ease of viewing. Figure 11.5 shows the EDR of an actual room, in this case a theater. The eigenfrequencies are visible as the ridges that run perpendicularly to the frequency axis.