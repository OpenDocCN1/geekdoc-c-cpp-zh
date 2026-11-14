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

# 6.6.4 Second-Order Butterworth LPF and HPF

Specify:

+   * \(f_c\), corner frequency

![](bbox=[0.15, 0.37, 0.85, 0.54])

Figure 6.23: Second-order BSF responses: \(f_c = 1\) kHz, bandwidth = 500 Hz (narrowest), 2 kHz, = kHz, and 10 kHz (widest).

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

# 6.6.5 Second-Order Butterworth BPF and BSF