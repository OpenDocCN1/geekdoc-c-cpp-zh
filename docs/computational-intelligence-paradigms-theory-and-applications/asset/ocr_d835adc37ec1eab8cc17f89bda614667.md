```
```matlab
x121=-6:0.1:6;

M=length(x121)

for i=1:M,
    z(i)=0.15*(rand-0.5)*2;
    % Define the auxiliary variable
    G121(i)=exp(-50*(x121(i)-1)^2)-0.5*exp(-100*(x121(i)
    -1.2)^2)+2)+atan(2*x121(i)+2.15+...
    0.2*exp(-10*(x121(i)+1)^2)-0.25*exp(-20*(x121(i)+
    1.5)^2)+0.1*exp(
    10*(x121(i)+2)^2)-0.2*exp(-10*(x121(i)+3)^2);
    if x121(i) >= 0
        G121(i)=G121(i)+0.1*(x121(i)-2)^2-0.4;
    end
    G121(i)=G121(i)+z(i);
    % Adds in the influence of the auxiliary variable
    % fpoly(i)=0.6+0.1*x(i);
end

% Next, plot the functions:

figure(1)
plot(x7,G7,'ko')
xlabel('x(i)')
ylabel('y(i)=G(x(i))')
title('M=7')
grid
axis([min(x7) max(x7) 0 max(G7)])

figure(2)
plot(x121,G121,'ko')
xlabel('x(i)')
ylabel('y(i)=G(x(i))')
title('M=121')
grid
axis([min(x121) max(x121) 0 max(G121)])

figure(3)
plot(x121,G121,'ko')
xlabel('x(i)')
ylabel('y(i)=G(x(i),z(i))')
```
```