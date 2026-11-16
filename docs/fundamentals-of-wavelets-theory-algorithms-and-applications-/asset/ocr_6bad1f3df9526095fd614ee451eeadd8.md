While the Wigner-Ville distribution is a time-frequency function that measures the energy density of the signal on the time-frequency plane, the ambiguity function is a distribution that measures the energy distribution over a frequency-shift ( Doppler) and time-delay plane. This is a very important function in radar signal processing, particularly in the area of waveform design. We shall see some applications of this function toward the end of this book.

Apart from a complex constant, we may express the AF in terms of the signal as

```
(4.80) \(\mathbf{A}_f(\tau, \zeta) = K \int_{-\infty}^{\infty} f\left(t - \frac{\tau}{2}\right) \overline{f\left(t + \frac{\tau}{2}\right)} e^{-j\zeta t} dt,\)
```

where \(K\) is a complex constant. The proof of this relationship can be found in [8]. For further information on the ambiguity function readers are referred to [9]. Figure 4.15 shows the AF for a chirp signal. This time-frequency representation will be revisited in Chapter 9, where the combination of *wavelet packets* and Wigner-Ville distribution is applied to radar signal detection.

# FIGURE 4.15: Ambiguity function of a chirp signal.