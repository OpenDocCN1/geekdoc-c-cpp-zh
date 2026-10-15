```
proc sgplot data=nitro_tox;
 ybox total / category=conc;
 xaxis label = "Nit rofen concentration";
 yaxis label = "Number of young (3 broods)";
 run;
```

The results of this code are shown in Display 3.22. The box is defined by the first quartile (25th percentile), median, and third quartile (75th percentile) with whiskers extending from the third quartile to the maximum value, and from the first quartile to the minimum value. (Variations of this construction are available. See the Help documentation.) The diamond in the center of the box indicates the location of the mean total number of young for each nit rofen concentration.

# Display 3.22 Side-by-side box plots for the young produced in different nit rofen concentrations

![](bbox=[0.09, 0.43, 0.83, 0.82])