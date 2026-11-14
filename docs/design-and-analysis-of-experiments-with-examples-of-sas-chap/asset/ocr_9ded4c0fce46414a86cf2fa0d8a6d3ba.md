set of experiments can be completed and a block variable added to the model to account for any changes in background variables that occurs between the first and second set of experiments.

# 10.3.2 Box-Behnken Design

Whereas the CCD requires five levels ($-\alpha, -1, 0, +1, +\alpha$) for each factor, Box and Behnken (1960) developed some three level designs that will allow estimation of the general quadratic model. These designs consist of $2^k$ factorials in each pair of factors with all other factors held constant at their mid-level plus a few center points. No Box-Behnken design exists for only two factors. An example of a Box-Behnken design in three coded factors is shown in Table 10.2.

Table 10.2 Box-Behnken Design in Three Factors

| run | $x_1$ | $x_2$ | $x_3$ |
|---|---|---|---|
| 1 | -1 | -1 | 0 |
| 2 | 1 | -1 | 0 |
| 3 | -1 | 1 | 0 |
| 4 | 1 | 1 | 0 |
| 5 | -1 | 0 | -1 |
| 6 | 1 | 0 | -1 |
| 7 | -1 | 0 | 1 |
| 8 | 1 | 0 | 1 |
| 9 | 0 | -1 | -1 |
| 10 | 0 | 1 | -1 |
| 11 | 0 | -1 | 1 |
| 12 | 0 | 1 | 1 |
| 13 | 0 | 0 | 0 |
| 14 | 0 | 0 | 0 |
| 15 | 0 | 0 | 0 |

Box-Behnken designs have two advantages over CCDs. The first advantage is that they only require that factors be varied over three levels. This may make experimentation less costly if actual prototypes are being constructed in the experimentation. The second advantage is that they usually (except for the five-factor case) require less total runs than the central composite design. For example, the three-factor CCD required twenty runs whereas the three-factor Box-Behnken design only required 15 runs.

A disadvantage of a Box-Behnken design compared to a central composite design is that it cannot be built up in two steps beginning with a $2^k$ design. This can be visualized in Figure 10.4, which diagrams a three-factor Box-Behnken design. A $2^3$ design consists of runs at all corners of the cube as shown in Section 3.7.1, but as can be seen in Figure 10.4 the Box-Behnken design does not include those points. Therefore a Box-Behnken design should