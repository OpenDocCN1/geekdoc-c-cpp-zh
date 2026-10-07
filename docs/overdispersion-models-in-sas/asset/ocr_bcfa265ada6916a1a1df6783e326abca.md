# Chapter 2 Generalized Linear Models 37

# Program 2.4: Estimation of the Normal and Logistic Cumulative Distribution Functions—nDosage-Mortality Data of Pyrethrins

```
-- Plotting
1)Estimated Logistic Curve and Observed Proportions
2)Estimated Probit Curve and Observed Proportions
temp:
    do dose=38 to 301 by 0.1; -- Dose range in increments of 0.1;
    x = log(dose);
    output;
end;
drop dose;
run;
data new;
    set pyrethrins temp;
run;
proc glimmix data=new;
    model t/m = x / link=probit;
    output=pred_out1(xlink)=pi_hat;
run;
proc glimmix data=new;
    model t/m = x;
    output=pred_out2(xlink)=pi_hat;
run;
data pred_out1;
    set pred_out1;
    label pi_hat = 'Predicted Probability'
    obs_pi =;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
data pred_out2;
    set pred_out2;
    label pi_hat = 'Predicted Probability'
    obs_pi =;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
 html;
ods graphics data=pred_out1;
proc sgplot;
    title "Estimated Probit Curve"
    title2 "Posage-Mortality of Pyrethrins on Male Flies, Murray (1938)";
    scatter x=x y=pi_hat;
    series x=x y=pi_hat / y2axis;
run;
proc sgplot data=pred_out2;
    title "Estimated Logistic Curve";
```

More, Jorge, and Nagaraj Neelchai. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary,
North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.