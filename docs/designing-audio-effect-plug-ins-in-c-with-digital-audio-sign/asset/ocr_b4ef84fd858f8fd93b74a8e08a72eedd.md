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

![](bbox=[0.15, 0.37, 0.85, 0.54])

Figure 6.22: Second-order LPF responses: \(f_c = 1\) kHz, \(Q = 0.707, 2, 5, 10\). Notice that as the \(Q\) rises above 0.707, \(f_c\) becomes the peak frequency.

# 6.6.3 Second-Order BPF and BSF

Specify:

+   - \(f_c\), corner frequency
+   - \(Q\), quality factor controlling width of peak or notch 51/BW; [Figure 6.23](#) shows the BSF version

Note: These filter coefficients contain the tan() function, which is undefined at \(\pi/2\) and then flips negative between \(\pi/2\) and \(\pi\). The argument is \(\theta_c/2Q\), so care must be taken with these filters to ensure that \(\theta_c/2Q\) does not fall on the range of \(\pi/2\) to \(\pi\). One solution is to clamp the value of \(\theta_c/2Q\) so that it never equals or exceeds \(\pi/2\).

The design equations are as follows: