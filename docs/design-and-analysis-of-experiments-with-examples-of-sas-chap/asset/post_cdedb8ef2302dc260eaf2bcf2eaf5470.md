
illustrate these macros, consider a problem studied by Barbuta and Lepadatu (2008). They investigated mechanical properties such as compressive strength, flexural strength, and adhesion stress of polymer concrete. Polymer concrete (PC) has many uses: precast components for buildings, bridge panels, repair of structural members, waterproofing and decorative overlay of pavements. Polymer concrete is formed by binding aggregates together with a resin that reacts with a hardener. The relatively high cost of PC led Barbuta and Lepadatu (2008) to study ways of reducing the dosage of polymer in the mix without diminishing the mechanical properties. The mixture components they studied were x1: Epoxy resin, x2: Silica Fume (SUF), x3: Aggregate Sort I and x4: Aggregate Sort II. Constraints on the mixture components are shown in Equation (11.19) below.

0.124 ≤ x1 ≤ 0.188
0.064 ≤ x2 ≤ 0.128
0.374 ≤ x3 ≤ 0.438
0.374 ≤ x4 ≤ 0.438

The SAS code below shows how to create the file work.exvert containing the extreme vertices using the McLean-Anderson algorithm.

```
%adxgen
%adxmin
%adxinit
%adxvert(exvert , x1 .124-.188/ x2 .064-.128/ x3
.374-.438/ x4 .374-.438)
proc print; run;
```

Running this code results in a list of four extreme vertices.

| Obs | x1 | x2 | x3 | x4 |
|---|---|---|---|---|
| 1 | 0.188 | 0.064 | 0.374 | 0.374 |
| 2 | 0.124 | 0.128 | 0.374 | 0.374 |
| 3 | 0.124 | 0.064 | 0.438 | 0.374 |
| 4 | 0.124 | 0.064 | 0.374 | 0.438 |

By changing the '%adxmand' to '%adxvert' in the commands above, Snee and Marquardt's XVERT algorithm will be used instead of McLean and Anderson's algorithm to find the extreme vertices. The arguments for '%adxvert' are the same as those for '%adxmand', except for one optional argument at the end that specifies the maximum order of centroids to be generated. The '%adxvert' macro not only finds the extreme vertices using the XVERT algorithm but it also finds the centroids up to the order specified by the user, and, by default, it also finds the overall centroid. For example, the code at the top of the next page finds the four extreme vertices shown in the listing above, plus the six edge centroids and the overall centroid. To add two-dimensional facet centroids, change the last argument from 2 to 3.

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

Table 11.4 shows data from the article. The response, overall liking, was the average ranking of 115 taste panelists who ranked the mixtures on a 9-point scale where 1 = dislike extremely, 5 = neither like nor dislike, and 9 = extremely like. Three additional mixtures in the interior of the simplex (that are not shown in the table) were tested to help discriminate between possible models for the data.

Once the mixture components are defined and the constraints entered to ADX, clicking the Select Design button causes ADX to construct a list of candidates which includes the five vertices, four edge centroids, and the overall

### Figure 11.20 Constrained Region for Peanut Fine Polvoron Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_480_0.png)

### Table 11.4 Data from Polvoron Mixture Experiment

| Run | | x1 | x2 | x3 | overall liking |
|---|---|---|---|---|---|
| 1 | vertex | 0.800 | 0.150 | 0.050 | 5.33 |
| 2 | edge cent. | 0.400 | 0.550 | 0.050 | 5.87 |
| 3 | vertex | 0.000 | 0.950 | 0.050 | 3.69 |
| 4 | edge cent. | 0.000 | 0.725 | 0.275 | 3.83 |
| 5 | vertex | 0.000 | 0.500 | 0.500 | 3.85 |
| 6 | edge cent. | 0.200 | 0.300 | 0.500 | 5.23 |
| 7 | vertex | 0.400 | 0.100 | 0.500 | 5.68 |
| 8 | edge cent. | 0.600 | 0.100 | 0.300 | 5.88 |
| 9 | vertex | 0.800 | 0.100 | 0.100 | 5.75 |
| 10 | centroid | 0.400 | 0.360 | 0.240 | 6.54 |
| 11 | centroid | 0.400 | 0.360 | 0.240 | 6.82 |
| 12 | centroid | 0.400 | 0.360 | 0.240 | 6.41 |

centroid shown in Table 11.4. One additional edge centroid at the top of the constrained region (shown in Figure 11.20) was found that is not shown in Table 11.4.

Once a list of candidates is found there are different options for creating the design. A first option is to select the status variable for each run in the list of candidate points and choose to include or exclude the point from the design. By doing this, a design with the exact mixture combinations shown in Table 11.4 can be constructed. A second option is to select a D-optimal or A-optimal subset of the candidate list. When using either of these options, the user is prompted to select the model for the data, since the X matrix depends on the model, and the number of runs included in the design. By selecting the special cubic model and asking for nine points to be included in the design, ADX produces the design points shown in Figure 11.21. Once a design is selected, individual points can be replicated by selecting the customize button on the main ADX template.

Figure 11.21 Design Points for D-optimal Design for Special Cubic Model for Polvoron Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_481_0.png)

## 11.5.2 Analysis of Constrained Mixture Experiments

The models used to analyze constrained mixture experiments are the same as those used for unconstrained problems, unless one of the constraints is an equality (such as an ionic balance constraint). In that case the constraint must be incorporated into the model, resulting in a loss of dimension (see Schrevens and DeRijck, 2008, for an example).

Analysis of the data in Table 11.4 with standard Scheffé models will be illustrated in ADX. Figure 11.22 shows the results of fitting the special cubic model to the data in Table 11.4. Although two quadratic terms and the third order term are insignificant, the model fits the data well (shown in Figure 11.23). The reduced model that included only the terms x1, x2, x3, and x1x2 had an adjusted R2 of 0.754 compared to 0.9516 shown for the special cubic model in Figure 11.22, and it fit worse at three interior checkpoints that were made by the experimenters to check the model. These checkpoints are not shown in Table 11.4.

Figure 11.24 shows a contour plot over the constrained region produced by
