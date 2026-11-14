CD, RS, QS, PS, AS, BS, CS, DP, DQ, DR, and DS can be estimated clear of main effects or two-factor interactions. This is what is referred to by the number of clear terms in Figure 8.11.

The third design shown in Figure 8.8 is also resolution IV, but by utilizing a one-half fraction of the combinations of whole-plot treatment levels and then splitting each whole-plot into four sub-plots, only eight whole plots are required. The generators for this design are ABCD, ABPR, and BCPQS. In this design seven effects, namely main effects A, B, C, and D and confounded strings of interactions AB + CD + PR, AC + BD, and AD + BC, are estimated less precisely and should be compared to whole-plot variability for testing significance. This design also allows estimation of 13 of the 28 two-factor interactions clear of main effects and other two-factor interactions, so it appears to be similar to the second design listed in Figure 8.8. However, because of the reduced number of whole plots and the increased number of sub-plots all 13 of the clear two-factor interactions can be tested with the more precise sub-plot error term, whereas in the second design six of the clear two-factor interactions (namely AD, BD, CD, RS, QS, and PS) must be tested with the less precise whole-plot error term.

The fourth and last design shown in Figure 8.8 consists of a full factorial in the four whole-plot factors A, B, C and D in 16 whole plots each divided into 4 sub-plots. The defining relation for this design is I = ABCPR = ADPQS = BCDRQS. This design is resolution V, and all main effects and two-factor interactions can be estimated clear of other main effects and two-factor interactions.

The choice between these four alternative designs would depend upon the relative cost of whole plot and sub-plot experimental units and the precision desired for the various estimable two-factor interactions. For more discussion on this topic, see Kulachi et al. (2006), Bisgaard (2000) and Bingham and Sitter (2001).

When using proc factex, the user does not have a choice about the degree of fractionation in the whole-plot and sub-plot design. proc factex only allows choice of the overall degree of fractionation. For example, the code below creates a 2^{8-3} fractional factorial with four whole-plot factors and four sub-plot factors. The search algorithm in proc factex only finds a 2^{-1} \times 2^{-2}

```
proc factex;
   factors A B C D P Q R S;
   size design=32;
   blocks units=(Block=16);
   model resolution=4/minabs;
   uniteffect Block / whole=(A B C D)
              sub=(P Q R S);
   examine aliasing=sub(2) confounding;
   output out=sa;
proc print; run;
```