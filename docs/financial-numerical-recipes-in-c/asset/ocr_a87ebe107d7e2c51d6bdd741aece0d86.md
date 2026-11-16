```
function P = findiff_exp_am_put(S,K,r,sigma,time,no.S_steps,no.t_steps)
sigma_sqr = sigma^2;
M=no.S_steps + rem(no.S_steps,2); # need no.S_steps to be even:
delta.S = 2*S/M;
S.values = delta.S * (0:M)';
N=no.t_steps;
delta.t = time/N;
r1=1/(1+r*delta.t);
r2=delta.t/(1+r*delta.t);
a=zeros(M-1,1);
b=zeros(M-1,1);
c=zeros(M-1,1);
for j=1:M-1,
aj = r2*0.5*sigma^2*(-j+sigma_sqr);
bj = 1+r1*(0.5-sigma_sqr)*delta.t;
c(j) = r2*0.5*(j+sigma_sqr);
endfor
f.next = max(0,K-S.values);
for t=N-1:-1:0
f = [K; a.*next(1:M-1)+b.*f.next(2:M)+c.*f.next(3:M+1); 0];
f = max(f,K-S.values);
f.next=f;
endfor
P=f(1+M/2);
endfunction
```

# Matlab Code 13.1: Explicit finite differences calculation of American put option