
## Figure 12.3 Illustration of Control Factors for Connector Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_521_0.png)

Therefore, this was not a split-plot experiment like the file example. The pointrep option of proc factex can be used to create a cartesian product design similar to the way it was shown in Section 8.2.1.

```
*Create noise factor design with factex;
proc factex;
factors F G;
output out=G1 nvals=(24 120) F nvals=(72 150) G nvals
=(25 75);
*Add the control factor design;
factors A B C D/nlevel=3;
model estimate=(A B C D);
output design=pointrep=s1 A cvals=('Low' 'Medium' 'High')
B cvals=('Thin' 'Medium' 'Thick')
C cvals=('Shallow' 'Medium' 'Deep')
D cvals=('Low' 'Medium' 'High');
proc print; run;
```

One of the comments that has been made about product array parameter design experiments popularized by Taguchi is that they require more experiments than are necessary. One of the main purposes of parameter design experiments is to detect interactions between control factors and noise factors. By understanding the interactions it may be possible to select levels of the control factors that will minimize the effect of the noise factors. By utilizing a cartesian product array design, all interactions between the factors in the control array and the factors in the noise array will be estimable. However, it may be possible to do this with fewer runs by utilizing resolution IV or resolution V fractional factorial designs where all interactions between control and noise factors are clear. Examples of this will be shown in Section 12.5.

## Figure 12.4 Complete Layout of Control Factor Array and Noise Factor Array

| 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | No. |
|---|---|---|---|---|---|---|---|---|
| 2 | 2 | 2 | 2 | 1 | 1 | 1 | 1 | E |
| 2 | 2 | 1 | 2 | 2 | 2 | 1 | 1 | F |
| 2 | 1 | 2 | 1 | 2 | 2 | 1 | 1 | ExF |
| 1 | 1 | 2 | 2 | 2 | 1 | 2 | 1 | G |
| 1 | 2 | 1 | 2 | 2 | 1 | 2 | 1 | ExG |
| 1 | 2 | 2 | 1 | 1 | 2 | 2 | 1 | FxG |
| 2 | 1 | 1 | 2 | 1 | 2 | 2 | 1 | E |
| 120h | 120h | 120h | 120h | 24h | 24h | 24h | 24h | Conditioning time (E) |
| 150F | 150F | 72F | 72F | 150F | 150F | 72F | 72F | Conditioning temperature (F) |

| No. | A | B | C | D | Interference factor (A) | Wall thickness (B) | Insertion depth (C) | Percentage adhesive (D) |
|---|---|---|---|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 | Low | Thin | Shallow | Low |
| 2 | 1 | 2 | 2 | 2 | Low | Medium | Medium | Medium |
| 3 | 1 | 3 | 3 | 3 | Low | Thick | Deep | High |
| 4 | 2 | 1 | 2 | 3 | Medium | Thin | Medium | High |
| 5 | 2 | 2 | 3 | 1 | Medium | Medium | Deep | Low |
| 6 | 2 | 3 | 1 | 2 | Medium | Thick | Shallow | Medium |
| 7 | 3 | 1 | 3 | 2 | High | Thin | Deep | Medium |
| 8 | 3 | 2 | 1 | 3 | High | Medium | Shallow | High |
| 9 | 3 | 3 | 2 | 1 | High | Thick | Medium | Low |

| 75% | 25% | 75% | 25% | 75% | 75% | 75% | 25% | Conditioning RH (G) |
|---|---|---|---|---|---|---|---|---|
| 19.1 | 20.0 | 19.6 | 19.6 | 19.9 | 16.9 | 9.5 | 15.6 | ... |
| 21.9 | 24.3 | 19.8 | 19.7 | 19.6 | 19.4 | 16.2 | 15.0 | ... |
| 24.4 | 24.2 | 18.8 | 22.0 | 18.4 | 18.9 | 17.5 | 14.5 | ... |
| 24.7 | 23.2 | 18.9 | 21.0 | 18.6 | 18.9 | 17.4 | 18.3 | ... |
| 25.3 | 27.5 | 21.4 | 25.6 | 25.1 | 19.4 | 18.6 | 19.7 | ... |
| 24.7 | 22.5 | 19.6 | 14.7 | 19.8 | 20.0 | 16.3 | 16.2 | ... |
| 21.6 | 24.3 | 18.6 | 16.8 | 23.6 | 18.4 | 19.1 | 16.4 | ... |
| 24.4 | 23.2 | 19.6 | 17.8 | 16.8 | 15.1 | 15.6 | 14.2 | ... |
| 28.6 | 22.6 | 22.7 | 23.1 | 17.3 | 19.3 | 19.9 | 16.1 | ... |

One situation where product arrays are actually more efficient is when the experiment is a split-plot. For example, in the lava tile experiment, the noise factor array consisted of simply measuring the response (number of defective tiles in a sample of 100) once for tiles produced in the inner kiln position and again for tiles produced in the outer kiln position. Therefore no additional experimental effort was required. Only eight batches of clay were mixed and molded, but more information was produced by measuring multiple responses for each run of the control factor array. Split-plot designs are sometimes described as super efficient since the sub-plot factors and interactions between sub-plot and whole-plot factors can be tested with the (usually) smaller sub-plot error term.

A third example of a product array parameter design experiment involves the design of a product. The product is the simple circuit for a temperature controller that uses resistance thermometer \( R_T \). The circuit diagram that is shown in Figure 12.5 was described by Taguchi and Phadke (1985). The

## Figure 12.5 Temperature Controller Circuit

![](img/878b651cdbe9da3d6d22e64d64b8a54f_523_0.png)

response, or measure of product performance, is the resistance value of \( R_T \) at which the relay turns on. Through circuit relations, the response is given by the rational function

\( R_T = \frac{R_3 R_2 (E_2 R_4 + E_0 R_1)}{R_1 (E_2 R_2 + E_2 R_1 - E_0 R_2)} \). (12.2)

The adjustment factor is \( R_3 \), which is known by the circuit relations. The control factors that a designer can specify are the nominal ratings of the resistors and diodes \( A = R_1, B = R_2 / R_1, C = R_4 / R_1, D = E_0 \) and \( F = E_2 \). The noise factors are deviations from the nominal values of the control factors that would be expected due to manufacturing imperfections and deterioration while the product is in use. The objective was to find the nominal settings of the control factors that minimize the variation in \( R_T \) since the desired value of \( R_T \) can always be obtained by adjusting \( R_3 \). This is an example of the

type of problems encountered in the electronics industry in Japan which were successfully solved using parameter design experiments. In problems similar to this where there is no clear functional relation like Equation (12.2), Taguchi recommends the values of the response be determined experimentally.

Since the response is a known function of the factors or independent variables, statisticians evaluating the methods used by Taguchi have shown that this particular kind of problem can be solved more efficiently using computer optimization as described by Box and Fung (1986) and illustrated by Lawson and Madrigal (1994). However, computer optimization was not possible in the early 1960s and the solution to this problem will be illustrated using a product array parameter design experiment to give a historical perspective.

The control factors and levels used in the control factor array are shown in Table 12.4.

## Table 12.4 Factors and Levels for Circuit Parameter Design

| Control Factors | -1 | 0 | 1 |
|---|---|---|---|
| A : R1 | 2.67 | 4.0 | 6.0 |
| B : R2/R1 | 1.33 | 2.0 | 3.0 |
| C : R4/R1 | 5.33 | 8.0 | 16.0 |
| D : E0 | 8.00 | 10.0 | 12.0 |
| F : E2 | 4.80 | 6.0 | 7.2 |
| Noise Factors | 97.96% of Nominal | Nominal | 102.04% of Nominal |

The experimental design for the control factors is the 18-run orthogonal array shown in Table 12.5. The coded factor levels on the left side of the table were created for this example using the %mktex macro that was described in Section 6.7 as shown in the commands below

```
%mktex(2 3*4, n=18, levels=1)
proc print data=design; run;
```

The %mktex macro creates the design in a non-randomized order in the SAS file named design and a randomized list in the SAS file named randomized. For this experiment there is no experimental error since the response consists of evaluating a function, so there is no need for a randomized list. The default levels for the factors produced by %mktex are 1, 2, ..., k where k is the number of levels of the factor. The levels=1 option creates centered integers levels (i.e., -1 and 1 for two-level factors, -1, 1 and 0 for the three-level factors, etc.) The design that is created by %mktex is the OA(18) design that was popularized by Taguchi for use in parameter design experiments. Wang and Wu (1995) found this design to have properties similar to the Plackett-Burman Designs, in that main effects plus linear×linear two-factor interactions can be
