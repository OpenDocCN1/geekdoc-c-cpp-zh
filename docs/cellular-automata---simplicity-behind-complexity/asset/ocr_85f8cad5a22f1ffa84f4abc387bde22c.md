the number of land-use classes was reduced to five (water, forest, agriculture, built-up, and Tsuu T'ina nation) and only four transitions were considered, namely forest to agriculture, forest to built-up, agriculture to forest, and agriculture to built-up. The model was calibrated over the period 1985-2001 and the simulation was run from 1985 to 2006 using three external driving factors (distance to Calgary city center, distance to a main road, distance to the main river). Higher values were obtained for the three Kappa simulation statistics calculated (Table 14), confirming that the simulation results could be improved by either reducing the number of land-use transitions in the model or improving the rules for some of the land-use transitions considered.

| | 1992 | 1996 | 2001 | 2006 |
|---|---|---|---|---|
| Kappa | 0.947 | 0.941 | 0.929 | 0.917 |
| KLocation | 0.951 | 0.947 | 0.938 | 0.939 |
| KFisto | 0.996 | 0.994 | 0.991 | 0.976 |
| Kappa Simulation | 0.304 | 0.262 | 0.251 | 0.227 |
| KTransLoc | 0.429 | 0.377 | 0.336 | 0.341 |
| KTransition | 0.709 | 0.695 | 0.747 | 0.665 |

Table 14. Overall Kappa coefficients of agreement obtained when running simulation with a reduced number of land-use transitions.

# ## 4. Conclusion

While the potential of CA models is increasingly acknowledged for land-use change studies, their calibration and the evaluation of their performance remains a challenge. In this research, we developed a calibration method that allows the modeler to interactively obtain information about historical land-use changes and the factors associated to these changes in order to automatically derive conditional and mathematical transition rules. When testing the applicability of this model in a study area in southern Alberta, sensitivity analyses were conducted to evaluate the influence of various conditions involved in the calibration of the model, including the cell size, the neighborhood configuration, the selection of the parameter values, and the number of driving factors. These analyses indicate that the simulation outcomes are affected by the selection of these conditions and that there exist no method to *a priori* identify the most adequate combination.

Sensitivity of raster-based CA models to cell size and neighborhood configuration has been recognized by several authors over the last years. One approach to overcome this sensitivity to scale is the implementation of object-based CA models with the inclusion of a dynamic neighborhood as proposed by Moreno et al. (2009, 2010) and others (Hamman et al., 2007). While such models are computationally intensive and the handling of the topology cumbersome, they appear as a promising approach to better capture the meaningful entities composing a landscape along with their evolution.

The calibration technique described in this paper provides useful insights regarding the number and choice of external driving factors that should be considered in the calibration. When taking into account external factors in addition to the influence of the cells within extended neighborhoods, the number of possible combinations of factors becomes too high to be thoroughly evaluated by a simple sensitivity analysis. Other approaches based on data