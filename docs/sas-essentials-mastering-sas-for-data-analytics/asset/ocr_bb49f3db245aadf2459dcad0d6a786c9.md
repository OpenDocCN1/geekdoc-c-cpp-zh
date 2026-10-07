# 426 CHAPTER 18: CREATING CUSTOM GRAPHS

(continued)

```
PROC SGPLOT DATA =ANCOVA;
SCATTER X=PRETEST Y=POSTTEST;
TITLE "SGPLOT Scatter Plot";nRUN;
```

![](bbox=[0.246, 0.219, 0.747, 0.493])

2. Change the SCATTER statement by adding a GROUP option:

```
SCATTER X=PRETEST Y=POSTTEST/GROUP=METHOD;
```

Resubmit the code and observe that the groups are displayed in different colors.

3. Change the SCATTER statement by adding Marker Attributes using the following code:

```
SCATTER X=PRETEST Y=POSTTEST/GROUP=METHOD
MARKERATTRS=(symbol=trianglefilled size=10px);
```

> Other symbol types for SGPLOT are listed in Appendix A, Section A.6).
Note that no color option is used here as we want each group to be represented by a unique color. Resubmit this code and note how the "dots" are changed to triangles.

4. Add these lines just before the RUN; statement to control the legend and labels:

```
KEYLEGEND / LOCATION=INSIDE POSITION=TOLEFT ;
XAXIS LABEL="Pre Test Results";
YAXIS LABEL="Post Test Results";
```

Submit this code and observe the results.