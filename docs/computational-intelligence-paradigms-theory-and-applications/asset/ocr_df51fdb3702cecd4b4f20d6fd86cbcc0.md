```
```matlab
(K/(tau_1*tau_2))*delta(index) ];

k1=step*F;
xnew=x+k1/2;

F=[ xnew(2) ;
    xnew(3) + (K*tau_3/(tau_1*tau_2))*delta(index) ;
    -((1/tau_1)+(1/tau_2))*xnew(3)
    + (K*tau_3/(tau_1*tau_2))*delta(index)-...
    (1/(tau_1*tau_2))*(abar*xnew(2)^3 + bbar*xnew(2))
    + (K/(tau_1*tau_2))*delta(index) ];

k2=step*F;
xnew=x+k2/2;

F=[ xnew(2) ;
    xnew(3) + (K*tau_3/(tau_1*tau_2))*delta(index) ;
    -((1/tau_1)+(1/tau_2))*xnew(3) +
    (K*tau_3/(tau_1*tau_2))*delta(index)-...
    (1/(tau_1*tau_2))*(abar*xnew(2)^3 + bbar*xnew(2))
    + (K/(tau_1*tau_2))*delta(index) ];

k3=step*F;
xnew=x+k3;

F=[ xnew(2) ;
    xnew(3) + (K*tau_3/(tau_1*tau_2))*delta(index) ;
    -((1/tau_1)+(1/tau_2))*xnew(3) +
    (K*tau_3/(tau_1*tau_2))*delta(index)-...
    (1/(tau_1*tau_2))*(abar*xnew(2)^3 + bbar*xnew(2))
    + (K/(tau_1*tau_2))*delta(index) ];

k4=step*F;
x=x+(1/6)*(k1+2*k2+2*k3+k4); % Calculated next state

t=t+step;  % Increments time
index=index+1;  % Increments the indexing term so that
% index=1 corresponds to time t=0.
counter=counter+1;  % Indicates that we computed one more
%       integration step

end % This end statement goes with the first ``while''
% statement in the program so when this is
```
```