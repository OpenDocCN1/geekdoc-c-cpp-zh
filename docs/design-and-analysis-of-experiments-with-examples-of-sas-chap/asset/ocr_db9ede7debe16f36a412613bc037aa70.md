(a) Create the design below in SAS ADX and enter data for the six responses that are shown in Table 11.12.

Table 11.12 Data from Plasma Etch Experiment

| x1 | x2 | x3 | y1 | y2 | y3 | y4 | y5 | y6 |
|---|---|---|---|---|---|---|---|---|
| 0.153846154 | 0.153846154 | 0.692307692 | 0.26 | 0.90 | 0.24 | 0.93 | 0.91 | 0.94 |
| 0.153846154 | 0.153846154 | 0.692307692 | 0.30 | 0.94 | 0.22 | 0.98 | 0.88 | 1.00 |
| 0.246153846 | 0.246153846 | 0.507692308 | 0.33 | 1.82 | 0.14 | 1.49 | 0.99 | 1.04 |
| 0.246153846 | 0.246153846 | 0.507692308 | 0.36 | 1.84 | 0.14 | 1.64 | 1.02 | 1.04 |
| 0.246153846 | 0.153846154 | 0.600000000 | 0.62 | 7.14 | 0.22 | 7.35 | 0.84 | 0.84 |
| 0.246153846 | 0.153846154 | 0.600000000 | 0.68 | 7.10 | 0.17 | 7.27 | 0.87 | 0.87 |
| 0.153846154 | 0.246153846 | 0.600000000 | 0.23 | 2.62 | 0.25 | 2.16 | 0.77 | 0.92 |
| 0.153846154 | 0.246153846 | 0.600000000 | 0.23 | 2.73 | 0.31 | 1.88 | 0.76 | 0.88 |
| 0.153846154 | 0.200000000 | 0.646153846 | 0.27 | 3.01 | 0.15 | 2.70 | 0.91 | 0.98 |
| 0.200000000 | 0.153846154 | 0.646153846 | 0.39 | 4.50 | 0.17 | 4.25 | 0.87 | 0.92 |
| 0.246153846 | 0.200000000 | 0.553846154 | 0.30 | 4.79 | 0.20 | 4.50 | 0.99 | 0.96 |
| 0.200000000 | 0.246153846 | 0.553846154 | 0.31 | 2.88 | 0.19 | 2.36 | 0.91 | 1.01 |
| 0.200000000 | 0.200000000 | 0.600000000 | 0.34 | 1.22 | 0.13 | 1.54 | 0.92 | 0.99 |

(b) Fit the Scheffé special cubic model for each response, check the adequacy of the fits, and reduce the model to the quadratic for responses where the ternary mixture coefficient is not significant.

(c) Make contour plots of the fitted surface for each response.

(d) By examining your contour plots, or using the contour optimizer in ADX, find a region in the constrained space where the fitted models predict that all response specifications can be met.

8. If all three components in a mixture design have the same lower and upper constraints (L=0.20, U=0.80), use Table 11.6 to create an orthogonally blocked mixture design, for fitting the Scheffé quadratic model, with two blocks of four mixtures in each block.