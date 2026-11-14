| Variable | LPF | HPF |
| :--- | :--- | :--- |
| \(\theta_c\) | \(\pi f_c / f_s\) | \(\pi f_c / f_s\) |
| \(\Omega_c\) | \(\tan(\theta_c)\) | \(\tan(\theta_c)\) |
| \(\kappa\) | \(\frac{\Omega_c}{\tan(\theta_c)}\) | \(\frac{\Omega_c}{\tan(\theta_c)}\) |
| \(\delta\) | \(\kappa^2 + \Omega_c^2 + 2\kappa\Omega_c\) | \(\kappa^2 + \Omega_c^2 + 2\kappa\Omega_c\) |
| \(a_0\) | \(\frac{\Omega_c^2}{\delta}\) | \(\frac{\kappa^2}{\delta}\) |
| \(a_1\) | \(2\frac{\Omega_c^2}{\delta}\) | \(\frac{-2\kappa^2}{\delta}\) |
| \(a_2\) | \(\frac{\Omega_c^2}{\delta}\) | \(\frac{\kappa^2}{\delta}\) |
| \(b_1\) | \(\frac{-2\kappa^2 + 2\Omega_c^2}{\delta}\) | \(\frac{-2\kappa^2 + 2\Omega_c^2}{\delta}\) |
| \(b_2\) | \(\frac{-2\kappa\Omega_c + \kappa^2 + \Omega_c^2}{\delta}\) | \(\frac{-2\kappa\Omega_c + \kappa^2 + \Omega_c^2}{\delta}\) |

All pass filters have interesting designs that yield equally interesting results. Their frequency responses are perfectly flat from DC to Nyquist. However, the phase responses are the same as those in first- and second-order LPFs. You get all of the phase shift but none of the frequency response change. These filters can be found in crossovers and reverb algorithms. They are also used for the phaser effect. APFs are designed with pole-zero pairs whose pole/zero radii are reciprocals of one another. For a first-order APF, the pole lies somewhere on the real axis inside the unit circle at radius R. The zero lies outside the unit circle at radius 1/R (Figure 6.25).

If you think about the geometric interpretation and analysis of the transfer function, as you move around the unit circle, your vector distances from the pole and zero will always be reciprocals, or 1/each other. The amplitude response is then flat but the phase response *does* change because it is not based on the distance to the point in question but rather on the angle of incidence of the ray line drawn from the analysis point to the pole or zero. The second-order APF has complementary poles and zeros also at reciprocal radii (Figure 6.26).

![](bbox=[0.14, 0.69, 0.86, 0.85])

Figure 6.24: A comparison between Butterworth and Linkwitz–Riley filters each with \(f_c = 1\) kHz; the Linkwitz–Riley filter is down –6 dB at \(f_c\).