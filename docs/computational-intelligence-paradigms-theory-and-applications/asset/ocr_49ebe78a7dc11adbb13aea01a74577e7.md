```
```matlab
phi=[phi1]';
Fmlp(i)=b+w'*phi;
end

figure(6)
plot(x121,G121n,'ko',x121,Fmlp,'k')
xlabel('x(i)')
ylabel('y(i)=G(x(i),z(i)), and perceptron output')
title('Neural network approximation, one neuron')
grid
axis([min(x121) max(x121) 0 max(G121)])

% Next, a single hidden layer perceptron, n1=2
w1=[1.5]';
b1=0;
w2=[1.25]';
b2=-6;
w=[3 1]';
b=0.4;

for i=1:M,
    phi1=inv(1+exp(-b1-w1*x121(i)));
    phi2=inv(1+exp(-b2-w2*x121(i)));
    phi=[phi1 phi2]';
    Fmlp(i)=b+w'*phi;
end
figure(7)
plot(x121,G121n,'ko',x121,Fmlp,'k')
xlabel('x(i)')
ylabel('y(i)=G(x(i),z(i)), and perceptron output')
title('Neural network approximation, two neurons')
grid
axis([min(x121) max(x121) 0 max(G121)])

% Next, we plot the premise membership functions for
% a Takagi-Sugeno fuzzy system approximator

c11=-3.5;
sigma11=0.8;

c12=-0.25;
sigma12=0.6;
```
```