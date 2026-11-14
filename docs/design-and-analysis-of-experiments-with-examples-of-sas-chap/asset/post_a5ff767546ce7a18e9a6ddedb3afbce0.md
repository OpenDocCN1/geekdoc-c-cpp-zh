
## 10.8 Blocked Response Surface (BRS) Designs

When experimental units are not homogeneous, it is always advantageous to group them into more homogeneous blocks and use a blocked experimental design. Earlier it was mentioned that the three-factor central composite designs could be run in two blocks; the factorial portion plus three center points in one block, and the axial portion and remaining center points in the other block. This is actually an example of an incomplete block design, like those described in Chapter 7, since not all the treatment combinations are represented in each block. It is possible to create an incomplete block design out of any response surface design so that the coefficients can be estimated more precisely.

Standard response surface designs such as the central composite designs (CCDs) and Box-Behnken designs (BBDs) have been blocked in a way that the blocks are orthogonal to the coded factor levels, squares of coded factor levels, and interactions among coded factor levels. In this way the least squares estimates of the parameters of the general quadratic model are not correlated with the block effects and these standard designs are 100% $D_s$ efficient as described in Section 7.8.1. The example described earlier, where the three-factor central composite design was blocked into two blocks with block sizes 11 and 9, is not 100% $D_s$ efficient. In order to achieve 100% efficiency, some additional restrictions must be made in terms of the number of blocks, the block sizes, and the axial radius. This will affect the distribution of the variance of a predicted value over the design region, and a compromise must be made. Table 10.7 shows the number of blocks and block sizes for orthogonally blocked CCDs and BBDs with $k = 2$ to 5 factors.

Table 10.7 Number of Blocks and Block Sizes for Orthogonally Blocked CCD and BBD Designs

| Number Factors | CCD No. Blocks | CCD Block Sizes | BBD No. Blocks | BBD Block Sizes |
| :--- | :--- | :--- | :--- | :--- |
| 2 | 2 | 7, 7 | | |
| 3 | 3 | 6, 6, 8 | | |
| 4 | 3 | 10, 10, 10 | 3 | 9, 9, 9 |
| 5 | 2 | 22, 11 | 2 | 23, 23 |

These designs can be created easily with the SAS ADX tool. It will automatically use the optimal block size and axial radius. To create a blocked response surface design, check the Blocking box on the ADX Select Design Template, as shown in Figure 10.22, and you will see the blocked designs available.

### Figure 10.22 Design Selection Template with Blocking Box Checked

![](img/878b651cdbe9da3d6d22e64d64b8a54f_436_0.png)

The number of blocks and block sizes available for orthogonally blocked CCD and BBD designs may be too restrictive for some applications. For example, Gilmour and Trinca (2000) presented the data from an experiment to determine how the characteristics of pastry dough depended upon parameters of the mixing process. In the experiment three factors were varied, the feed flow rate (FR), the initial moisture content (MC) and the screw speed (SS). One of the responses (y) measured light reflectance of the resulting dough in particular bands of the spectrum in order to see how the color of the dough was affected by the mixing parameters. Only four runs or experiments could be conducted on one day and the experimenters anticipated day to day variation. None of the designs in Table 10.7 have blocks of size four. Thus the experimenters ran the modified design shown in Table 10.8, with the coded factor values x1 = (FR - 37.5)/7.5, x2 = (MC - 21)/3, and x3 = (SS - 350)/50. This is an example of a face-centered cube design that is a special case of a central composite design with the axial points (in coded units) pulled in to the face of the cube at ±1. The 2^3 factorial portion of this design was replicated and there were six center points. The twenty-eight runs of this design were blocked into seven blocks (days) of four runs in a way that the main effects are orthogonal to the blocks. However, as Goos (2002) pointed out, the quadratic and interaction terms of the general quadratic model are not orthogonal to blocks and a better way of blocking the twenty-eight experiments design can be achieved using a $D_s$ optimal design. This can be done using proc optex. First create the face centered cube design using the %adxccd macro as shown in the code below Table 10.8 on the next page. This macro creates all twenty-eight design points shown in Table 10.8 and stores them in the SAS file fccd with the factors labeled t1, t2, and t3.

```
*adxgen
*adxfif
*adxcc
*adxinit
*adxccd(fccd,3,16,6,1.0,1)
```

Table 10.8 Design and Response for Pastry Dough Experiment

| Block | x1 | x2 | x3 | y |
|---|---|---|---|---|
| 1 | -1 | -1 | -1 | 12.92 |
| 1 | -1 | 1 | 1 | 13.91 |
| 1 | 1 | -1 | 1 | 11.66 |
| 1 | 1 | 1 | -1 | 14.48 |
| 2 | -1 | -1 | -1 | 10.76 |
| 2 | -1 | 1 | -1 | 14.41 |
| 2 | 1 | -1 | -1 | 12.27 |
| 2 | 1 | 1 | 1 | 12.13 |
| 3 | -1 | 1 | -1 | 14.22 |
| 3 | 0 | -1 | 0 | 12.35 |
| 3 | 1 | 0 | 0 | 13.5 |
| 3 | 0 | 0 | 1 | 12.54 |
| 4 | 1 | -1 | 1 | 10.55 |
| 4 | -1 | 0 | 0 | 13.33 |
| 4 | 0 | 1 | 0 | 13.84 |
| 4 | 0 | 0 | -1 | 14.19 |
| 5 | -1 | -1 | -1 | 11.46 |
| 5 | 1 | 1 | 1 | 11.32 |
| 5 | 0 | 0 | 0 | 11.93 |
| 5 | 0 | 0 | 0 | 11.63 |
| 6 | -1 | -1 | 1 | 12.2 |
| 6 | 1 | 1 | -1 | 14.78 |
| 6 | 0 | 0 | 0 | 14.94 |
| 6 | 0 | 0 | 0 | 14.61 |
| 7 | -1 | 1 | 1 | 12.17 |
| 7 | 1 | -1 | -1 | 11.28 |
| 7 | 0 | 0 | 0 | 11.85 |
| 7 | 0 | 0 | 0 | 11.64 |

Next use proc optex to group the runs into seven blocks of four runs as shown on the next page. The noexchange option on the blocks statement tells proc optex to keep all the runs in the file fccd in the design and arrange them into seven blocks of four in a way to maximize the $D_s$ efficiency.

To create a blocked response surface design that is a subset of the possible runs in a file of candidates, replace the file fccd in the commands above

```
proc optex data=fccd coding=orthcan seed=2347;
model t1 t2 t3 t1*t2 t1*t3 t2*t2 t3*t3;
blocks structure=(7)4 noexchange niter=10000 keep=10;
generate n=28 augment=fccd;
output out=bpastry blockname=block; run;
proc print data=bpastry;
run;
```

by the file of candidates and remove the noexchange option of the blocks statement. For example, to block the experiments in the QSAR example in Section 10.5 so that they could be run in five different labs (that may have differing measurements of bio-activity) modify the code from Section 10.5 as shown below.

```
proc optex data=qsar;
model HE DMz SOk HE*HE DMz*DMz SOk*SOk HE*DMz HE*SOk DMz*SOk;
blocks structure=(5)4;
generate n=20 iter=200 keep=5;
output out=design1;
proc print data=design1; run;
```

To analyze a blocked design with more than two blocks using proc rsreg, create dummy variables for the blocks as shown below for the pastry dough experiment shown in Table 10.8.

```
data pastry;
input Block x1 x2 x3 y;
b1=(Block=1);
b2=(Block=2);
b3=(Block=3);
b4=(Block=4);
b5=(Block=5);
b6=(Block=6);
b7=(Block=7);
datalines;
1 -1 -1 -1 12.92
proc rsreg;
model y=b1-b6 x1 x2 x3/covar=6;
run;
```

## 10.9 Response Surface Split-Plot (RSSP) Designs

When response surface designs contain factors from different process steps or some factors are hard to vary, it may be costly or inconvenient to completely randomize the runs in a standard response surface design. For example, consider a simple response surface design to identify the baking temperature and baking time that would result in the optimal moist cake. The design and data are shown in Table 10.9 where x1 = (bake temp. – 350)/25, x2 = (bake time – 31.5)/4, and y is the reading from a moisture tester.

Table 10.9 Data for Cake Baking Experiment

| Oven run | x1 | x2 | y |
|---|---|---|---|
| 1 | -1 | -1 | 2.7 |
| 1 | -1 | 1 | 2.5 |
| 1 | -1 | 0 | 2.7 |
| 2 | 1 | -1 | 2.9 |
| 2 | 1 | 1 | 1.3 |
| 2 | 1 | 0 | 2.2 |
| 3 | 0 | -1 | 3.7 |
| 3 | 0 | 1 | 2.9 |
| 4 | 0 | 0 | 2.9 |
| 4 | 0 | 0 | 2.8 |
| 4 | 0 | 0 | 2.9 |

The design is a face-centered cube design with three levels for each factor and three center points. The experiments were not performed in a random order. Once the oven temperature was set and the oven was preheated, as many as four cakes could be baked at once. Performing the experiments in a completely randomized order would have required eleven oven runs, but by baking as many as three cakes at the same time (as shown in the table) only four oven runs were required. The oven runs were performed in a random order with the two or three cakes for each run placed in random positions in the oven. The cakes in each run were withdrawn from the oven at different baking times except for oven run 4 when all cakes were baked for 31.5 minutes.

By running the experiments in this way, a response surface split-plot (RSSP) type design results, where x1, the baking temperature, is the whole-plot factor and x2, baking time, is the subplot factor. Since the same subplot treatment combinations are not run in each whole plot, Letsinger et al. (1996) show that the least squares estimates of the model parameters, which would be obtained by proc reg, will be unsatisfactory if the ratio of the whole-plot to subplot error variances is greater than one. They recommend using REML estimators, which can be computed in proc mixed.

Combining the coefficients for the linear, quadratic, and interaction terms in the same vector, the general quadratic model for a completely randomized response surface design can be written in matrix form as

```
y = Xβ + ε (10.16)
```

When the response surface design is run as a split plot, like the example in
