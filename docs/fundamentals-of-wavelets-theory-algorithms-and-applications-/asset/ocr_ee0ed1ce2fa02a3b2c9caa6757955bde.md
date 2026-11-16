```
length(phi_new);
if(i ==== (Niter-1))
phi2 = phi;
end
end
%
dt = 1.0 / ( 2 * unit);
t = [1:length(phi)] * dt;
subplot(2,1,1), plot(t,phi)
title('Scaling Function ')
```

% Compute wavelet using 2-scale relation

```
for i = 1:ng1
a = (i-1) * unit + 1;
b = a + length(phi2) - 1;
psi2s(i,a:b) = phi2 * g(1); psi2s(1,n) = 0;
end
psi = sum(psi2s);
t = [0:length(phi)-1] * dt - (ng1 - 2) / 2;
subplot(2,1,2), plot(t,psi)
title('Wavelet')
```

# 6.8.2 Iteration Method

%