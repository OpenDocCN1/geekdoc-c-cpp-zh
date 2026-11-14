```
data decrip; set trebuchet;
run;
proc reg Data=ArmLength B=CounterWeight C=MissileWeight ;
proc print; run;
ods graphics on; imagemft=png border=off;
ods listing style=journal2 image_dpi=250;
proc rsreg data=decrip plots(unpack)=(surface (at
Counterweight = 20));
model Distance=ArmLength CounterWeight MissileWeight;
run;
ods graphics off;
```

The resulting contour plot at a slice with B: counterweight = 20lbs. is shown in Figure 10.17. In this plot it can be seen that with a counterweight of 20lbs., the predicted maximum distance will be achieved using a missile weight of about 2.375 ounces and an arm length of about 7.5 inches. The predicted distance at these conditions is about 115 feet, with a standard error of about 1.5 feet.

# Figure 10.17 Contour Plot of Predicted Trebuchet Distance with Counter-weight=20lbs.

![](bbox=[0.11, 0.52, 0.88, 0.88])