then the proc nlp statements below can be used to find the maximum product concentration. The parms statement gives starting values of the factors in the center of the experimental region. The bounds statement gives the bounds on the experimental region.

```
proc nlp;
   max p;
   parms time Temp= 12.5 400;
   bounds 0 <= time <= 25,
           375 <= Temp <= 425;
   k1=.523*exp( -9847*((1/Temp)-(1/400)) );
   k2=2.*exp( -12327*((1/Temp)-(1/400)) );
   p=-132*(exp(-k1*time)-exp(-k2*time))*k1/(k1-k2);
run;
```

The results show the maximum product concentration, p, within the experimental region is p̂ = 82.88 at t = 18.16 hours and T = 375 degrees Kelvin. Since this problem only has two factors (time and temperature) the results can be visualized in the contour plot shown in Figure 10.21 which displays the maximum at the boundary of the experimental region.

# Figure 10.21 Maximum Product Concentration

![](bbox=[0.155, 0.505, 0.845, 0.805])

A rough approximation to numerical optimization can be made by doing a grid search. Create a fine grid of the experimental region in a SAS data step and then evaluate the response surface function at each grid point to get