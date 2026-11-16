```
(10.70)
\frac{dH_z}{dt} = \frac{1}{\mu} \left[ \frac{dE_x}{dy} - \frac{dE_y}{dx} \right]
```

represent the 2D TEz mode of Maxwell's equations for source-free, lossless, isotropic media. The expansion of the \(E_x\) field in (10.68) in terms of Haar scaling and wavelet functions is

```
(10.71)
\(E_x(x, y) = \sum_{n_{i,j,l}} h_{n_{l(i)}} \left[ n E_{i,j}^{X,\phi\phi} \phi_i(x) \phi_j(y) \right.\)
\(\left. + \sum_{r=0}^{r_{max}} \sum_{p=0}^{2^r-1} n E_{i,j,r,p}^{X,\psi\psi} \Psi_{i,p}^{r,f}(x) \phi_j(y) \right.\)
\(\left. + \sum_{r=0}^{r_{max}} \sum_{p=0}^{2^r-1} n E_{i,j,r,p}^{X,\phi\psi} \phi_i(x) \Psi_{j,p}^{r,f}(y) \right.\)
\(\left. + \sum_{r=0}^{r_{max}} \sum_{p=0}^{2^r-1} \sum_{s=0}^{2^s-1} \sum_{q=0}^{2^q-1} n E_{i,j,r,p}^{X,\psi\psi} \Psi_{i,p}^{r,f}(x) \Psi_{j,q}^{r,f}(y) \right]\)
```

where \(n E_{i,j}^{X,\phi\phi}\) is the coefficient corresponding to scaling function in x and y that represents the electric field in the \(i, j\) cell at time step \(n\); \(\Psi_{i,p}^{r,f}\) denotes a wavelet of resolution \(r\) at the \(p\)-position \([(p - 0.5)/2^r]\) of the \(j\) cell. Other coefficients have similar definitions. The time dependence is assumed to be constant for each time step using the