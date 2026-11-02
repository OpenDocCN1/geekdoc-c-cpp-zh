![](bbox=[0.245, 0.108, 0.801, 0.425])

Fig. 2. Confirmed zoomed region after checking the concavity condition

| 3-arm type | Micro GA | MGA+DFP | MGA+LGA |
|---|---|---|---|
| Convergence Generation | 9000 | 4000+α | 4100 |
| Objection Function | 0.690497E+10 | 0.690488E+10 | 0.690488E+10 |

Table 2. Comparison of results: MGA, MGA+DFP, MGA+LGA

# ### 3. Example of the SZGA

The value of the zooming factor α, an optimal parameter was obtained in reference [8], and was found to show good match with the empirical one. Using this zooming factor in SZGA, the displacement of a truss structure was derived by minimizing the total potential energy of the system. The capacity of the servomotor, which operates the wicket gate mounted in a Kaplan type turbine of the electric power generator, was optimized using SZGA with the value of zooming factor α.

This is just one parameter among the full optimal parameters discussed in sec.2.1⁹. Therefore, the analysis done with this factor⁸ is a simplified analysis. As commented in section 2.1, the values of the parameters of a well-behaved test model suggested in the Table 1 can be used for an optimization, or the values of the parameters obtained in another way as discussed in the next section can be used.

Several additional examples of SZGA optimization are presented in the following sections to provide more insight on SZGA and to find another way of choosing the values of the SZGA parameters. The first example finds the Moony-Rivlin coefficients of a rubber material to compare with those from the least square method. The second example is a damage detection problem in which the difference between the measured natural frequencies and those of the assumed damage in the structure is minimized. The third example finds the