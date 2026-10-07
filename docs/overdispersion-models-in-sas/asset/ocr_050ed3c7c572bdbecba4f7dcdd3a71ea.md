of the early work is Johnson, Kotz, and Balakrishnan (1997), who also provide results on other forms of mixtures of multinomials. Algorithms for data generation under either the Dirichlet-multinomial or Random-clumped Multinomial models are provided in Appendix 7.1.

# 7.9 A Study on Housing Satisfaction

Two independent random samples of neighborhoods were taken from the rural and urban areas in Montevideo, Minnesota. Five households were selected from each sampled neighborhood. The families in each household provided information on their satisfaction with their homes. They were classified as “Unsatisfied,” “Satisfied,” and “Very Satisfied.” Brier (1980), Koehler and Wilson (1986), Wilson (1989), and Morel and Nagar (1993) have analyzed data from this study. We used the data report by Wilson (1989) which consists of 18 rural and 17 urban neighborhoods. The responses of the families within a neighborhood are correlated. We will illustrate the fitting of the Dirichlet-multinomial (7.30) and Random-clumped Multinomial (7.33) distributions to the rural data only. Since residents within the neighborhoods generally talk to each other to convince one, and share and even common opinions, it is reasonable to model these “clumped” data by equation (7.32). The rural data can be found in

Table 7.3: Housing Satisfaction Rural Data

| Unsatisfied | Satisfied | Very Satisfied |
|---|---|--|
| 3 | 2 | 0 |
| 3 | 2 | 0 |
| 0 | 5 | 0 |
| 3 | 2 | 0 |
| 0 | 5 | 0 |
| 4 | 1 | 0 |
| 3 | 2 | 0 |
| 2 | 3 | 0 |
| 4 | 0 | 1 |
| 0 | 4 | 1 |
| 2 | 3 | 0 |
| 4 | 1 | 0 |
| 4 | 1 | 0 |
| 1 | 2 | 2 |
| 4 | 1 | 0 |
| 1 | 3 | 1 |
| 4 | 1 | 0 |
| 5 | 0 | 0 |

The computation of $\pi$ and $ho$ are illustrated in Program 7.3. In order to get the MLE, the module `DirMult_RCMult` is invoked. This module has been kindly provided by Dr. Justin