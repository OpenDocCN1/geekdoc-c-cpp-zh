type of problems encountered in the electronics industry in Japan which were successfully solved using parameter design experiments. In problems similar to this where there is no clear functional relation like Equation (12.2), Taguchi recommends the values of the response be determined experimentally.

Since the response is a known function of the factors or independent variables, statisticians evaluating the methods used by Taguchi have shown that this particular kind of problem can be solved more efficiently using computer optimization as described by Box and Fung (1986) and illustrated by Lawson and Madrigal (1994). However, computer optimization was not possible in the early 1960s and the solution to this problem will be illustrated using a product array parameter design experiment to give a historical perspective.

The control factors and levels used in the control factor array are shown in Table 12.4.

Table 12.4 Factors and Levels for Circuit Parameter Design

| Control Factors | -1 | 0 | 1 |
|---|---|---|---|
| A : R1 | 2.67 | 4.0 | 6.0 |
| B : R2/R1 | 1.33 | 2.0 | 3.0 |
| C : R1/R1 | 5.33 | 8.0 | 16.0 |
| D : Eo | 8.00 | 10.0 | 12.0 |
| F : E2 | 4.80 | 6.0 | 7.2 |
| Noise Factors | 97.96% of Nominal | Nominal | 102.04% of Nominal |

The experimental design for the control factors is the 18-run orthogonal array shown in Table 12.5. The coded factor levels on the left side of the table were created for this example using the %mktex macro that was described in Section 6.7 as shown in the commands below

```
%mktex(2 3*4, n=18, levels=1)
proc print data=design; run;
```

The %mktex macro creates the design in a non-randomized order in the SAS file named design and a randomized list in the SAS file named randomized. For this experiment there is no experimental error since the response consists of evaluating a function, so there is no need for a randomized list. The default levels for the factors produced by %mktex are 1, 2, ..., k where k is the number of levels of the factor. The levels=1 option creates centered integers levels (i.e., -1 and 1 for two-level factors, -1, 1 and 0 for the three-level factors, etc.) The design that is created by %mktex is the OA(18) design that was popularized by Taguchi for use in parameter design experiments. Wang and Wu (1995) found this design to have properties similar to the Plackett-Burman Designs, in that main effects plus linear×linear two-factor interactions can be