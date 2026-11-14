Low Shelving
\(\theta_c = 2\pi f_c / f_s\)
\(\mu = 10^{Gain(dB)/20}\)
\(\beta = \frac{4}{1 + \mu}\)
\(\delta = \beta \tan(\theta_c / 2)\)
\(\gamma = \frac{1 - \delta}{1 + \delta}\)
\(a_0 = \frac{1 - \gamma}{2}\)
\(a_1 = \frac{1 - \gamma}{2}\)
\(a_2 = 0.0\)
\(b_1 = -\gamma\)
\(b_2 = 0.0\)
\(c_0 = \mu - 1.0\)
\(d_0 = 1.0\)

High Shelving
\(\theta_c = 2\pi f_c / f_s\)
\(\mu = 10^{Gain(dB)/20}\)
\(\beta = \frac{1 + \mu}{4}\)
\(\delta = \beta \tan(\theta_c / 2)\)
\(\gamma = \frac{1 - \delta}{1 + \delta}\)
\(a_0 = \frac{1 + \gamma}{2}\)
\(a_1 = - \left( \frac{1 + \gamma}{2} \right)\)
\(a_2 = 0.0\)
\(b_1 = -\gamma\)
\(b_2 = 0.0\)
\(c_0 = \mu - 1.0\)
\(d_0 = 1.0\)

(6.41)

Shelving filters are used in many tone controls, especially when there are only two, bass and treble, which are almost always implemented as shelf types. The filters have a corner frequency and gain or attenuation value. Figure 6.28 shows a family of shelving filter response curves.

![](bbox=[0.15, 0.46, 0.85, 0.63])

Figure 6.28: Low and high shelving filter responses. The low shelf frequency = 400 Hz, high shelf frequency = 5 kHz, with a variety of boost/cut settings.

# 6.7.3 Second-Order Parametric/Peaking Filter: Non-Constant-Q

Specify:

+   - \(f_c\), center frequency
+   - \(Q\) quality factor
+   - Gain/attenuation in dB

Parametric EQs allow you to adjust the center frequency, \(Q\) and boost or cut creating any arbitrary bumps or notches in the frequency response (Figure 6.30). The parametric EQ is a variation on the ordinary band-pass and band-stop filters that generates symmetrical boost/cut curves and mixes in the dry signal to create the final response. A true digital parametric EQ not only has independent controls,