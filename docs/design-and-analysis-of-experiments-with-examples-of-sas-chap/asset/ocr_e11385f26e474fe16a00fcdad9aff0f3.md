```
%adxgen
%adxlst
%addint
%adxexvert(exvert, x1 .124-.188/ x2 .064-.128/ x3 .374-.438/
x4 .374-.438,2)
proc print; run;
```

For many constrained mixture problems, the number of extreme vertices and edge centroids will be much greater than the number of coefficients in the Scheffe quadratic model. To reduce the number of mixtures and still allow fitting a quadratic model to the resulting data, a D-optimal subset can be selected using proc optex as shown in the example below. In this example, a D-optimal subset of 14 mixtures from the file work.exvert will be output to the file work.dmax.

```
proc optex data=exvert;
model x1 x2 x3 x4 x1*x2 x1*x3 x1*x4 x2*x3 x2*x4 x3*x4/
noint;
generate n=14 ;
output out=data-dmax; run;
proc print data=dmax; run;
```

If the constraint equations such as Equation (11.19) are inconsistent, there will be no feasible points within the constrained region. In that case, the SAS log will indicate the file exvert.test has zero observations.

The SAS ADX tool can also create a list of candidate design points for constrained mixture experiments composed of extreme vertices and centroids. To illustrate ADX, which can also graph the feasible region, consider the three-component mixture studied by Juan et al. (2006).

They studied consumer acceptance of polvoron composed of a mixture of x1: sugar, x2: peanut fines, and x3: butter. Polvoron is a Philippine ethnic dessert or candy usually composed of milk powder, toasted flour, sugar, and butter. Ground nuts can be added to vary its flavor and texture properties. If acceptable to consumers, utilizing peanut fines (which are usually a discarded byproduct of the roasted peanut process) in polvoron could reduce waste and create an additional product line. The constraints on the mixture space are shown in Equation (11.20).

```
0.00 <= x1 <= 0.80
0.10 <= x2 <= 0.95
0.05 <= x3 <= 0.50
```

Selecting three-mixture components and entering the constraints listed in Equation (11.20) into ADX, the constrained region is graphed as shown in Figure 11.20.

Table 11.4 shows data from the article. The response, overall liking, was the average ranking of 115 taste panelists who ranked the mixtures on a 9-point scale where 1 = dislike extremely, 5 = neither nor nor dislike, and 9 = extremely like. Three additional mixtures in the interior of the simplex (that