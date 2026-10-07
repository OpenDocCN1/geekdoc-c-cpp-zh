(continued)

```
PROC SGPLOT DATA =MYSASLIB.CORONARY;
TITLE 'BUBBLE PLOT USING CORONARY DATA';
TITLE2 'Bubble is BMI';
BUBBLE X = AGE Y = SBP SIZE = BMI
 TRANSPARENCY = 0.5;
GRID;
RUN;
```

![](bbox=[0.248, 0.258, 0.843, 0.513])

Figure 18.20 Bubble plot created using SGPLOT

Information you might learn from this graph that SBP tends to increase with AGE that the bubbles get bigger towards the right and top meaning BMI might be associated with older subjects and higher SBP (which makes medical sense).

+   2. Change the transparency to 0.9 and run the code. Note how transparency changes the appearance of the plot.
3. Change the transparency back to 0.5. Add the option GROUP=INSURANCE after the TRANSPARENCY statement (and before the semicolon). Rerun and note the different colors by group. Does this provide any additional information about how people with insurance differ from those who don't have it?
4. Change the option in the BUBBLE statement to /TRANSPARENCY=0.5 FILLATTRS=(COLORS=GREEN) to change the color of the bubbles to green. Other possible options are listed in Appendix A, Section A.2.

# 18.9 OTHER WAYS TO CUSTOMIZE PLOTS

There are at least two other techniques you can use to customize plots: Annotation Data Sets and the Graph Template Language (GTL).