186

Applied Time Series Analysis with R

```
$$\gamma_k = \frac{\Lambda_i^2}{2}\cos 2\pi f_i k, \quad k \neq 0$$
$$= \frac{\Lambda_i^2}{2} + \sigma_N^2, \quad k=0.$$\quad (4.11)$
```

Thus, $\rho_k$ is given by

```
$$\rho_k = \frac{(\Lambda_i^2/2)\cos 2\pi f_ik}{(\Lambda_i^2/2) + \sigma_N^2}, \quad k \neq 0$$
$$=1, \quad k=0.$$$
```

Since $H_i$ and $N_i$ are uncorrelated, it follows that the spectrum is given by

```
$$$P_Y(f) = \frac{\Lambda_i^2}{4}(\Delta(f-f_i) + \Delta(f+f_i)) + \sigma_N^2.$$$
```

and the spectral density is

```
$$$S_Y(f) = \frac{(\Lambda_i^2/4)\\Delta(f-f_i) + \Delta(f+f_i))}{\frac{\Lambda_i^2}{2} + \sigma_N^2}.$$
```

A realization from the model

```
$$$Y_i = 4.4\cos\left(\frac{2\pi t}{12} + U\right) + N_i.$$$quad (4.12)$
```

where $N_i$ is discrete white noise with unit variance was previously shown in Figure 4.1b. The autocorrelations and spectrum (not in dB) for this model are plotted in Figure 4.3 where it can be seen that the autocorrelations do not damp out, in this case, $max|\rho_k|=0.9$. The spectrum shows a finite spike of $\Lambda_i^2/4+\sigma_v^2=5.84$ at $f=1/12$ with a flat spectrum of $P_Y(f)=1$ for $f \neq 1/12$ associated with the white noise component. Spectra such as the one in Figure 4.3b are called mixed spectra, which are mixtures of the discrete and continuous spectra encountered up this point.

**Using R:** A realization from the model

```
$$$X_i = A_1\cos(2\pi f_1t) + A_2\cos(2\pi f_2t) + N_i.$$$quad (4.13)$
```

where $N_i$ is Gaussian noise can be obtained using the tsw function gen.sigplusnoise.w function that is described in Appendix 1B.