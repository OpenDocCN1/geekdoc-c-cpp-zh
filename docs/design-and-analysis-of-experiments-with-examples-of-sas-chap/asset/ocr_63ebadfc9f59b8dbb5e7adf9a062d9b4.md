# Figure 10.8 Variance Dispersion Graph for Roquemore 310 Design

![](bbox=[0.19, 0.16, 0.82, 0.4])

```
%adxgen
%adxff
%adxc
%adxinit
%adxccd(rs1,3,8,6,1,68,1)
```

The first argument in the call statement, %adxccd(rs1,3,8,6,1,68,1), is rs1: the file where the design will be stored in non-random order, the second argument 3: is the number of factors, the third argument 8: is the number of points in the factorial portion of the design, the fourth argument 6: is the number of center points in the design, the fifth argument 1.68: is the value of the axial extreme, and the last argument 1: is the number of blocks in the design.

However, the easiest and most versatile method of creating response surface designs in SAS is to use the automated design of experiments tool SAS ADX. For example, to create a three-factor central composite design, click on Solutions ▶ Analysis ▶ Design of Experiments to open the ADX system. Next, click on the icon for New Response Surface Design, or click File ▶ Create New Design ▶ Response Surface... To create a design for three factors, click the Define Variables... button. On the Factors tab, click on Add > and then define the variables. To create the uncoded design shown in Table 10.1, fill out the template as shown in Figure 10.9. The Low Levels and High Levels