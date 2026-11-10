```
figure, plot(maxf), hold on, plot(meanf,'r-');
title('Maximum and Mean of the 1-D function');
xlabel('Population')
ylabel('Variable y')
%%%%%%%%%%%%%%%% End of Main %%%%%%%%%%%%%%%%

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Subprogram used
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
function y = multipeak(x)
% Demonstration evaluation function
% f(x)=x+10sin(5x)+7cos(4x) + 25

y = x + 10*sin(5*x)+7*cos(4*x) + 25;

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```

# Observations

Figure 12.7 shows the multi-peak of the given function which occurs at (6.4488, 44.3352) and Figure 12.8 shows the maximum and mean value of the given function.

![](bbox=[0.172, 0.579, 0.753, 0.878])

**FIGURE 12.7:** Multi-Peak for the Given Function