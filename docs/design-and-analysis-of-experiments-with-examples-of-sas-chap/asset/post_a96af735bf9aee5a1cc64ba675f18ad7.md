
were to be made for each of these experiments (as suggested in exercise 1 of Chapter 2), a total of 56 experiments would be required.

![](img/878b651cdbe9da3d6d22e64d64b8a54f_68_0.png)

If the objective were to find the combination with the longest flight time, the classical approach would be to complete the experiments with one factor first. Next one would calculate the cell means and then select the level with the highest mean. Finally, the second factor would be varied while holding the first constant at its optimal level, not the lowest level as shown in Figure 3.1. However, Fisher's caution to randomize would tell you that this is a bad strategy. If any unknown forces changed after the first set of experiments, the results could be biased. Additionally, the optimal level of one factor may depend upon the level of the other factor. Therefore, by varying one factor at a time, the overall optimum may be missed.

The diagram on the right side of Figure 3.1 represents a factorial plan for the helicopter experiments. Here it can be seen that experiments are run at all combinations of the levels of the two factors. In this plan, if two replicates of each cell are completed, there will be eight replicates of each level of wing length, and eight replicates of each level of body width which is equivalent to the one-at-a-time plan. Therefore the factorial plan would have the same precision or power for detecting factor effects as the one-at-a-time plan, but is more efficient since it requires only 2 × 16 = 32 total runs as opposed to the 56 required by the one-at-a-time plan. The number of replicates of each factor level in the factorial design is equal to the number of replicates per cell times the product of the levels of all other factors in the design. This multiplication is referred to as hidden replication. In the case shown in Figure 3.1, there are only two factors each at four levels; therefore, the number of replicates of each factor level is 2 × 4 = 8. In the factorial plan, the 32 treatment combinations would be randomized to experimental units, thus preventing biases from unknown sources. In more complicated research problems many treatment factors may be under study. The efficiency of factorial designs can be demonstrated even in the simplest case where each factor has only two levels. For example, consider a design with 4 factors. A factorial design would require all combinations of four factors at two levels, or 2^4 = 16 cells. If two replicates were run for each cell, there would be a total of 2 x 16 = 32 experiments or runs. To examine the effect of any one of the four factors, half the runs (or 2 x 2^3 = 16 due to the hidden replication) would be at one level of the factor and half at the other level. Thus the treatment effect would consist of a difference of two averages of 16. Results from the same 32 experiments can be used to calculate the treatment effect for each of the four factors. To have equal precision for comparing treatment effects using a one-at-a-time plan, 32 runs would be required for comparing the levels of each factor while holding the others constant. This would result in 4 x 32 = 128 experiments, or four times the number required for a factorial design!

## 3.3 Interpreting Interactions

If there is an interaction or joint effect between two factors, the effect of one factor upon the response will differ depending on the level of the other factor. This can be illustrated graphically in Figure 3.2. On the left side of the figure is a contour plot representing the results of a series of experiments with paper helicopters. This plot can be interpreted like a topographical map with the lines representing contours of equal flight time. You can simulate what would happen in a series of experiments where wing length was held constant and body width varied by drawing a straight line parallel to the body width axis across the contour plot. The flight time for various runs can be read off as the label for the contour lines the straight line intersects. For example, if wing length were held constant a value below its mid-point on the left of the contour plot, the flight times resulting from five runs with varying body width are represented as the black line traced on the graph at the right line in Figure 3.2. If the wing length were held constant at a higher value, the grey line indicates what the result of a series of experiments with body width might look like. The fact that two lines or curves on the right side of the figure are not parallel indicates there is an interaction between wing length and body width. They show that the effect of body width depends upon the wing length.

Figure 3.2 Contour Plot of Flight Time for Helicopter Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_69_0.png)

Interactions are common in the real world, but using the classical one-at-a-time strategy of experimentation tacitly assumes that interactions do not exist. To see the fallacy that results from this assumption, examine Figure 3.3, which represents what would happen if one were to search for the optimum combination of wing length and body width.

Figure 3.3 One-at-a-Time Optimization with Paper Helicopters

![](img/878b651cdbe9da3d6d22e64d64b8a54f_70_0.png)

The vertical set of circles are drawn at the wing length, body width combinations for a series of experiments that vary wing length while holding body width constant. The numbers within the circles represent the resulting flight times. After examining the result of this series of experiments, the optimal wing length would be chosen and another series of experiments would be conducted by holding wing length constant at its optimal value and varying body width. The results of these experiments can be visualized as the horizontal series of circles. The maximum result, 2.8, is not the overall optimum, because the optimal wing length depends on the body width and vice versa.

Table 3.1 Mooney Viscosity of Silica B at 100° C

| Naphthene Oil (phr) | 0 | 12 | 24 | 36 | 48 | 60 |
|---|---|---|---|---|---|---|
| 0 | 25 | 30 | 35 | 40 | 50 | 60 |
| 10 | 18 | 21 | 24 | 28 | 33 | 41 |
| 20 | 13 | 15 | 17 | 20 | 24 | 29 |
| 30 | 11 | 14 | 15 | 17 | 18 | 25 |

When the effect of the factors is close to linear, the interaction is easier to explain in words. Table 3.1 shows the results of a factorial experiment conducted by Derringer (1974) to determine the effect of elastomer compounds on the viscosity of silica at 100°C. The elastomer compounds were Naphthene Oil, studied at 4 levels, and Filler content, studied at 6 levels.

Figure 3.4 shows a graphical representation of the data in the table. This figure is called an interaction plot. As Filler is increased from 0 to 60, the viscosity increases along a fairly linear trend. However, the slope of the trend line depends upon the level of Naphthene Oil. When there is no Naphthene Oil added, increasing Filler from 0 to 60 causes viscosity to increase rapidly from 25 to 60; but when there is 30 phr of Naphthene Oil, increasing Filler from 0 to 60 causes a more gradual increase in viscosity from 11 to 25.

Figure 3.4 Interaction Plot of Filler and Naphthene Oil

![](img/878b651cdbe9da3d6d22e64d64b8a54f_71_0.png)

Since interactions are common in factorial experiments, it is important to learn how to explain or interpret an interaction in order to clearly present the results of research studies. This is best done by describing the effect of one factor upon the response, and then contrasting or comparing how that effect changes depending on the level of the other factor. An interaction plot, like Figure 3.4, can guide the description or interpretation. Many more examples of interpreting interactions will be given throughout this chapter and the remainder of the book.

## 3.4 Creating a Two-Factor Factorial Plan in SAS

A factorial design can be easily created using nested do loops in the SAS data step. For example, to create a factorial design to study paper helicopters with three levels of body width (3.25", 3.75" and 4.25") and three levels of wing length (4.0", 5.0" and 6.0") the following SAS data step creates all possible combinations.

```
data copter;
do BW = 3.25 to 4.25 by .5;
do WL = 4 to 6 by 1;
output;
end;
end;
run;
```

To add two replicates of each cell and a random number for later use in randomizing the list, add an additional nested do loop as shown below.

```
data copter;
do BW = 3.25 to 4.25 by .5;
do WL = 4 to 6 by 1;
do rep = 1 to 2;
u=ranuni(0);
output;
end;
end;
end;
run;
```

To randomize the order of the factorial design or CRFD, add the following data step.

```
proc sort data=copter; by u;
data list; set copter;
experiment=_n_;
title Paper Helicopter Experiments;
proc print;
var BW WL;
id experiment;
run;
```
