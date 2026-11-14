
![](img/b54974d0a4317ec82d7ae02126d10a6f_179_0.png)

Figure 6.16: The pole at s = -1 and the zero at s = ±∞ plotted in the s-plane.

![](img/b54974d0a4317ec82d7ae02126d10a6f_179_1.png)

Figure 6.17: The bilinear transform maps real zeros at infinity to the Nyquist frequency in the z-plane.

Next consider the second-order analog low-pass filter transfer function:

```
H(s) = \frac{1}{s^2 + (1/Q)s + 1}

which factors as

H(s) = \frac{1}{(s - P)(s - P^*)} (6.25)
```

This transfer function has a pair of conjugate poles at locations P and P* or (a + bjω) and (a − bjω) as well as a pair of zeros at ±∞. The bilinear transform maps the poles on the left side of the s-plane to locations inside the unit circle. Once again, it maps the zeros at ±∞ to z = −1 or the Nyquist frequency (Figures 6.18 and 6.19).

There are several methods of overcoming this problem (Orfanidis 1997; Massberg 2011). The Massberg approach is discussed further in Section 6.9. Even with the error in the BZT, it is still an excellent tool for converting existing designs. You will notice that in the design methods, we start with the desired cutoff frequency (and Q, where applicable) and calculate the coefficients.

![](img/b54974d0a4317ec82d7ae02126d10a6f_180_0.png)

![](img/b54974d0a4317ec82d7ae02126d10a6f_180_1.png)

## 6.6 Generic Bi-Quad Designs

The following classical analog filters are converted to digital and implemented as bi-quad topologies:

- LPF (low-pass filter)
- HPF (high-pass filter)
- BPF (band-pass filter)
- BSF (band-stop filter)
- Second-order Butterworth LPF and HPF
- Second-order Linkwitz-Riley LPF and HPF (good for crossovers)
- First- and second-order all-pass filters (APF)

Low-pass and high-pass filters are characterized by their corner frequency $f_c$ and (for second-order and higher) their $Q$ or resonant peaking value. A $Q$ of 0.707 is the highest value $Q$ can assume before peaking occurs. It is called the Butterworth or maximally flat response. With a $Q$ of 0.707 the –3 dB point of the filter will be exactly at \(f_c\). For these designs, once the \(Q\) rises above 0.707, it will correspond to the peak frequency and not the –3 dB frequency. Equations 6.26 through 6.29 relate the \(Q\), peak frequency, –3 dB frequency, and the peak magnitude values.

\(f_{-3\text{dB}} = f_c \sqrt{\left(\frac{1}{2Q^2} - 1\right) + \sqrt{\left(\frac{1}{2Q^2} - 1\right)^2 + 1}}\) (6.26)

\(f_c = \frac{f_{-3\text{dB}}}{\sqrt{\left(\frac{1}{2Q^2} - 1\right) + \sqrt{\left(\frac{1}{2Q^2} - 1\right)^2 + 1}}}\) (6.27)

\(\text{Peak gain} = \frac{Q^2}{\sqrt{Q^2 - 0.25}} \quad (Q > 0.707 \text{ only})\) (6.28)

\(\text{Peak}_{\text{dB}} = 20 \log(\text{peak gain})\) (6.29)

Band-pass, band-stop, graphic, and parametric EQs are specified by their center frequency \(f_c\) and \(Q\) or bandwidth (Equation 6.30). Depending on the filter, the arithmetic (Equation 6.31) or geometric (Equation 6.32) mean is used to relate \(f_c\) and the band edges \(f_U\) and \(f_L\).

\(Q = \frac{f_c}{BW}\) (6.30)

\(\text{Arithmetic mean} = f_c = \frac{f_U - f_L}{2}\) (6.31)

\(\text{Geometric mean} = f_c = \sqrt{f_U f_L}\) (6.32)

![](img/b54974d0a4317ec82d7ae02126d10a6f_181_0.png)

Figure 6.20: Generic bi-quad structure.

The block diagram is shown in Figure 6.20.

The difference equation is as follows:

\(y(n) = a_0 x(n) + a_1 x(n-1) + a_2 x(n-2) - b_1 y(n-1) - b_2 y(n-2)\) (6.33)

### 6.6.1 First-Order LPF and HPF

Specify:

- *$f_c$, corner frequency; see Figure 6.21 for examples

The design equations are as follows:

LPF
\[\theta_c = 2\pi f_c / f_s\]
\[\gamma = \frac{\cos \theta_c}{1 + \sin \theta_c}\]
\[a_0 = \frac{1 - \gamma}{2}\]
\[a_1 = \frac{1 - \gamma}{2}\]
\[a_2 = 0.0\]
\[b_1 = -\gamma\]
\[b_2 = 0.0\]

HPF
\[\theta_c = 2\pi f_c / f_s\]
\[\gamma = \frac{\cos \theta_c}{1 + \sin \theta_c}\]
\[a_0 = \frac{1 + \gamma}{2}\]
\[a_1 = -\left(\frac{1 + \gamma}{2}\right)\]
\[a_2 = 0.0\]
\[b_1 = -\gamma\]
\[b_2 = 0.0\]

(6.34)

![](img/b54974d0a4317ec82d7ae02126d10a6f_182_0.png)

Figure 6.21: First-order LPF with $f_c = 100 \text{ Hz}, 250 \text{ Hz}, 500 \text{ Hz}, \text{ and } 1 \text{ kHz}$.

### 6.6.2 Second-Order LPF and HPF

Specify:

- $f_c$, corner frequency
- $Q$, quality factor controlling resonant peaking; Figure 6.22 shows the effect of Q and peaking

The design equations are as follows:

LPF
\(\theta_c = 2\pi f_c / f_s\)
\(d = \frac{1}{Q}\)
\(\beta = 0.5 \frac{1 - \frac{d}{2} \sin \theta_c}{1 + \frac{d}{2} \sin \theta_c}\)
\(\gamma = (0.5 + \beta) \cos \theta_c\)
\(a_0 = \frac{0.5 + \beta - \gamma}{2.0}\)
\(a_1 = \frac{0.5 + \beta - \gamma}{2.0}\)
\(a_2 = \frac{0.5 + \beta - \gamma}{2.0}\)
\(b_1 = -2\gamma\)
\(b_2 = 2\beta\)

HPF
\(\theta_c = 2\pi f_c / f_s\)
\(d = \frac{1}{Q}\)
\(\beta = 0.5 \frac{1 - \frac{d}{2} \sin \theta_c}{1 + \frac{d}{2} \sin \theta_c}\)
\(\gamma = (0.5 + \beta) \cos \theta_c\)
\(a_0 = \frac{0.5 + \beta + \gamma}{2.0}\)
\(a_1 = -\frac{(0.5 + \beta + \gamma)}{2.0}\)
\(a_2 = \frac{0.5 - \beta + \gamma}{2.0}\)
\(b_1 = -2\gamma\)
\(b_2 = 2\beta\)
(6.35)

![](img/b54974d0a4317ec82d7ae02126d10a6f_183_0.png)

Figure 6.22: Second-order LPF responses: \(f_c = 1\) kHz, \(Q = 0.707, 2, 5, 10\). Notice that as the \(Q\) rises above 0.707, \(f_c\) becomes the peak frequency.

### 6.6.3 Second-Order BPF and BSF

Specify:

- \(f_c\), corner frequency
- \(Q\), quality factor controlling width of peak or notch \(f_c\)/BW; Figure 6.23 shows the BSF version

Note: These filter coefficients contain the tan() function, which is undefined at \(\pi/2\) and then flips negative between \(\pi/2\) and \(\pi\). The argument is \(\theta_c/2Q\), so care must be taken with these filters to ensure that \(\theta_c/2Q\) does not fall on the range of \(\pi/2\) to \(\pi\). One solution is to clamp the value of \(\theta_c/2Q\) so that it never equals or exceeds \(\pi/2\).

The design equations are as follows:

BPF
\(\theta_c = 2\pi f_c / f_s\)
\(\beta = 0.5 \frac{1 - \tan(\theta_c/2Q)}{1 + \tan(\theta_c/2Q)}\)
\(\gamma = (0.5 + \beta)\cos \theta_c\)
\(a_0 = 0.5 - \beta\)
\(a_1 = 0.0\)
\(a_2 = -(0.5 - \beta)\)
\(b_1 = -2\gamma\)
\(b_2 = 2\beta\)

BSF
\(\theta_c = 2\pi f_c / f_s\)
\(\beta = 0.5 \frac{1 - \tan(\theta_c/2Q)}{1 + \tan(\theta_c/2Q)}\)
\(\gamma = (0.5 + \beta)\cos \theta_c\)
\(a_0 = 0.5 + \beta\)
\(a_1 = -2\gamma\)
\(a_2 = 0.5 + \beta\)
\(b_1 = -2\gamma\)
\(b_2 = 2\beta\)

(6.36)

### 6.6.4 Second-Order Butterworth LPF and HPF

Specify:

- *\(f_c\), corner frequency

![](img/b54974d0a4317ec82d7ae02126d10a6f_184_0.png)

Figure 6.23: Second-order BSF responses: \(f_c = 1\) kHz, bandwidth = 500 Hz (narrowest), 2 kHz, 4 kHz, and 10 kHz (widest).

Butterworth low-pass and high-pass filters are specialized versions of the ordinary second-order low-pass filter. Their Q values are fixed at 0.707, which is the largest value it can assume before peaking in the frequency response is observed.

The design equations are as follows:

LPF
\(C = \frac{1}{\tan(\pi f_c / f_s)}\)
\(a_0 = \frac{1}{1 + \sqrt{2}C + C^2}\)
\(a_1 = 2a_0\)
\(a_2 = a_0\)
\(b_1 = 2a_0(1 - C^2)\)
\(b_2 = a_0(1 - \sqrt{2}C + C^2)\)

HPF
\(C = \tan(\pi f_c / f_s)\)
\(a_0 = \frac{1}{1 + \sqrt{2}C + C^2}\)
\(a_1 = -2a_0\)
\(a_2 = a_0\)
\(b_1 = 2a_0(C^2 - 1)\)
\(b_2 = a_0(1 - \sqrt{2}C + C^2)\)

(6.37)

### 6.6.5 Second-Order Butterworth BPF and BSF

Specify:

- $f_c$, corner frequency
- $BW$, bandwidth of peak/notch = $f_c/Q$

Butterworth BPF and BSF are made by cascading (BPF) or paralleling (BSF) a Butterworth LPF and Butterworth HPF.

Note: These filter coefficients contain the tan() function, which is undefined at $\pi/2$ and then flips negative between $\pi/2$ and $\pi$. The argument is $\pi f_c BW/f_s$, so care must be taken with these filters to ensure that $\pi f_c BW/f_s$ does not fall on the range of $\pi/2$ to $\pi$. One solution is to clamp the value of $\pi f_c BW/f_s$ so that it never equals or exceeds $\pi/2$.

The design equations are as follows:

| BPF | BSF |
|---|---|
| $C = \frac{1}{\tan(\pi f_c BW/f_s)}$ | $C = \tan(\pi f_c BW/f_s)$ |
| $D = 2 \cos(2\pi f_c/f_s)$ | $D = 2 \cos(2\pi f_c/f_s)$ |
| $a_0 = \frac{1}{1 + C}$ | $a_0 = \frac{1}{1 + C}$ |
| $a_1 = 0.0$ | $a_1 = -a_0 D$ |
| $a_2 = -a_0$ | $a_2 = a_0$ |
| $b_1 = -a_0(CD)$ | $b_1 = -a_0 D$ |
| $b_2 = a_0(C - 1)$ | $b_2 = a_0(1 - C)$ |

### 6.6.6 Second-Order Linkwitz–Riley LPF and HPF

Specify:

- $f_c$, corner frequency (–6 dB)

Second-order Linkwitz–Riley LPFs and HPFs are designed to have an attenuation of –6 dB at the corner frequency rather than the standard –3 dB, shown in Figure 6.24. When these filters are placed in parallel with the same cutoff frequency, their outputs sum exactly and the resulting response is flat. They are often used in crossovers. We use them for the spectral dynamics processor later on.

The design equations are as follows:
