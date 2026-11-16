```
$$G_\phi f_0(b, \xi) = \int_{-\infty}^{\infty} f(t-t_0)\phi(t-b)e^{-i\xi t} dt$$
$$
= \int_{-\infty}^{\infty} f(t)\phi(t-(b-t_0))e^{-i\xi t}e^{-i\xi t_0} dt$$
$$
= e^{-i\xi t_0} G_\phi f(b-t_0, \xi).$$
(4.20)
```

Equation (4.20) simply means that if the original function \(f(t)\) is shifted by an amount \(t_0\) in the time axis, the location of STFT in the time-frequency domain will shift by the same amount in time while the frequency location will remain unchanged. Apart from the change in position, there is also a change in the phase of the STFT, which is directly proportional to the time shift.

# Frequency Shift:

Letting \(f(t)\) be the modulation function of a carrier signal \(e^{j\omega_0 t}\) such that

```
\(f_0(t) = f(t)e^{j\omega_0 t},\)
(4.21)
```

then the STFT of \(f_0(t)\) is given by

```
$$G_\phi f_0(b, \xi) = \int_{-\infty}^{\infty} f(t)e^{j\omega_0 t}\phi(t-b)e^{-i\xi t} dt$$
$$
= G_\phi f(b, \xi - \omega_0).$$
(4.22)
```

Equation (4.22) implies that both the magnitude and the phase of the STFT of \(f_0(t)\) remain the same as those of \(f(t)\),