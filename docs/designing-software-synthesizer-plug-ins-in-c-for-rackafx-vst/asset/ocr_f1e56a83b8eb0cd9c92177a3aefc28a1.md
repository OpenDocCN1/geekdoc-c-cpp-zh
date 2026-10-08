Look at the node u and verify that it is indeed:

u = α₀(y₁ + β₂s₂ + β₃s₃) (7.12)

Figure 7.15: The modified LPF structure now includes a feedback output path.

Figure 7.16: The completed Korg35 LPF model.

The sequence following the filter is:

+   * process x through LPF1 to get y
* form u alpha0*(y1 + feedback S2 and S3)
* add nonlinear processing to u if desired
* process through LPF2 to get y3
* calculate y = Ky3
* process through HPF1 (whose output appears to be nowhere)

![](bbox=[0.335, 0.253, 0.957, 0.808])

# 7.5 Korg35 HPF Model

The Korg35 HPF circuit results from an analog method of converting a LPF to HPF by grounding the input and driving the ground (Lindquist, 1977). When this is applied to the Sallen-Key topology, the resulting HPF has only 6 dB/octave of rolloff instead of 12 dB. Stinchcombe (2006) derived the resulting analog transfer function that revealed a BPF in parallel with the second order caused the first order rolloff phenomenon. By starting with the Sallen-Key HPF topology and adding a parallel BPF in the HPF input section, we can achieve the same result. Figure 7.18 shows the block diagram of the Sallen-Key

![](bbox=[0.335, 0.535, 0.957, 0.947])