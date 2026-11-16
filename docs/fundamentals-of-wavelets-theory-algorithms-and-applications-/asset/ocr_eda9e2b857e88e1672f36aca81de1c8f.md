\(\int_{-\infty}^{\infty} \phi(t) dt = 1.\)

# 13. Construct biorthogonal wavelets beginning with the two-scale sequence {g0[n]} for linear spline.

# 6.8 COMPUTER PROGRAMS

# 6.8.1 Daubechies Wavelet

```
%
% PROGRAM wavelet.m
%
% Generates Daubechies scaling functions and wavelets
g0 = [0.68301; 1.18301; 0.31699; -0.18301];
k = [0: 1: 2: 3];
g1 = flipud(g0).*(-1).^k;
ng1 = length(g1);
% Compute scaling funtion first
NIter = 10; % iteration time
phi_new = 1; % initialization
for i = 1:NIter
unit = 2^(i-1);
phi = conv(g0,phi_new);
n = length(phi);
phi_new(1:2:2*n) = phi;
```