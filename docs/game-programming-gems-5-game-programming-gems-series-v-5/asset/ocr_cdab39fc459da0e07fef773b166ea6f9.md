The FDN is sort of a vectorized 1D-simulation that can develop an increasing echo density over time but not an increasing mode density over frequency, which results in artifacts like ringing tones.

# The Feedback Delay Network

See Figure 7.4.2 for a circuit diagram of an FDN with four channels.

![](bbox=[0.2, 0.25, 0.8, 0.51])

The heart of an FDN is a feedback loop with the n delay lines z and a square n x n feedback matrix A. In case you are unfamiliar with the z-transform: multiplication with z raised to the power -m stands equivalent to a delay of m samples, a notation common in digital audio. The elements aj of the feedback matrix control how much signal from line i is taken back to line j. The input signal, xk, is multiplexed prior to entering the feedback loop by the input matrix c. Likewise, the output signal, yk, is formed as a weighted sum over all channels by the output matrix d. Alternatively, you could directly access the four output channels to have four uncorrelated signals to place into the listener’s 3D space.

The key feature of an FDN is the signal traffic between the delay lines. An echo from the output of one delay line enters all other delay lines, being echoed by all of them, then each echo again enters all other delay lines, etc. Figure 7.4.3 shows the first second of the impulse response of a four-channel FDN. As you can see, the build-up of echo density is quite similar to that found in the rectangular room. The spectrum plot however reveals that the resonant modes are distributed uniformly over the frequency range and not packed as densely. This is the tribute to pay for the computational effectiveness.