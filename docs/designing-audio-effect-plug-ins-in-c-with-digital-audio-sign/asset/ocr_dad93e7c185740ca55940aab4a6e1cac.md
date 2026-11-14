# 6.6.1 First-Order LPF and HPF

Specify:

+   * $f_c$, corner frequency; see Figure 6.21 for examples

The design equations are as follows:

LPF
\[\theta_c = 2\pi f_c f_s\]
\[\gamma = \frac{\cos \theta_c}{1 + \sin \theta_c}\]
\[a_0 = \frac{1 - \gamma}{2}\]
\[a_1 = \frac{1 - \gamma}{2}\]
\[a_2 = 0.0\]
\[b_1 = -\gamma\]
\[b_2 = 0.0\]

HPF
\[\theta_c = 2\pi f_c f_s\]
\[\gamma = \frac{\cos \theta_c}{1 + \sin \theta_c}\]
\[a_0 = \frac{1 + \gamma}{2}\]
\[a_1 = -\left(\frac{1 + \gamma}{2}\right)\]
\[a_2 = 0.0\]
\[b_1 = -\gamma\]
\[b_2 = 0.0\]

(6.34)

![](bbox=[0.14, 0.41, 0.86, 0.58])

Figure 6.21: First-order LPF with $f_c = 100 \text{ Hz}, 250 \text{ Hz}, 500 \text{ Hz}, \text{ and } 1 \text{ kHz}$.

# 6.6.2 Second-Order LPF and HPF

Specify:

+   * $f_c$, corner frequency

+   * $Q$, quality factor controlling resonant peaking; Figure 6.22 shows the effect of Q and peaking

The design equations are as follows: