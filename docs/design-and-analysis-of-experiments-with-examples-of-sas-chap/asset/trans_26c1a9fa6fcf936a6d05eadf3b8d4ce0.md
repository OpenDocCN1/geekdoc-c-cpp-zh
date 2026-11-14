

Effects estimated by regression. The principles of effect sparsity and hierarchical ordering help in interpreting the results.

The subset of runs for one-quarter and higher fractions of $2^k$ factorials can also be carefully selected by choosing generators that confound p added factors to interactions among the k-p factors in the base design. From the generators the defining relation and alias structure for the design can be determined. SAS ADX system automatically generates designs that have the highest resolution and minimum aberration among all $2^{k-p}$ designs with the same number of runs. Designs of resolution R confound main effects with R - 1 and higher order interactions. These designs also have a projective property. When only R - 1 factors or less appear significant after running a resolution R design, the insignificant factors can be ignored and a full factorial in R - 1 factors will remain. The $2^{k-p}$ fractional factorial projects to a $2^{R-1}$ full factorial in R - 1 factors.

After analysis of data from a resolution III fractional factorial, the interpretation may be straightforward if only one factor appears to have a significant effect. When more than one factor appears to have a significant effect, the interpretation may be more difficult due to aliasing of interactions with main effects. Augmenting a resolution III fractional factorial with a foldover or mirror fraction can often eliminate the confounding between apparently important main effects and interactions, and can allow for a simple interpretation of the effects after only a fraction of the runs needed for a full factorial.

When confounded strings of two-factor interactions appear significant when analyzing data from a resolution IV design, augmenting the design with certain foldover fractions or D-Optimal subsets of runs can provide the data to determine which interactions are significant.

Plackett-Burman designs preserve many of the benefits of factorial and fractional factorial designs such as orthogonality among main effects and the projective property. In addition, these designs are available in run sizes that are multiples of 4 rather than powers of 2 as they are for fractional factorial designs. If more than one factor is significant after the analysis of a Plackett-Burman design, significant interactions can sometimes be detected using regression subset selection techniques without requiring additional experiments such as a foldover or D-Optimal fraction.

Finally, when more than two levels are required for some factors, mixed level fractional factorials can be created using orthogonal array and orthogonal main effect plans that are generated with the SAS Mkt macros. These designs are similar to Plackett-Burman designs in that they are orthogonal in the main effects and have no defining relation. Many of these designs also have a projective property, and interactions can be detected without additional experiments using methods of analysis similar to those used for Plackett-Burman designs.

## 6.9 练习

- 1. Consider a $2^{3-1}$ fractional factorial design,
  - (a) Modify the SAS code in Section 6.2 to create a list of the runs in the design.
  - (b) Determine the defining relation.
  - (c) Determine the complete alias pattern.
  - (d) Use SAS ADX to create this design.
  - (e) Examine the Alias Structure in SAS ADX.

- 2. Melo et al. (2007) used a $2^{4-1}$ fractional factorial design with generator D = ABC to study the factors that influence the production of levan by aerobic fermentation using the yeast Zymomonas mobilis. Levan is a sugar polymer of the fructan group which has been shown to have anti-tumor activity against sarcoma and Ehrlich carcinoma in Swiss albino mice. The factors varied in the fermentation medium and their levels are shown in the table below.

| Label | Factor | Levels - | Levels + |
|---|---|---|---|
| A | Sucrose initial concentration(g·L⁻¹) | 150 | 250 |
| B | Temperature(°C) | 20 | 30 |
| C | Yeast extract initial concentration(g·L⁻¹) | 2.0 | 5.0 |
| D | Agitation(rpm) | 50 | 100 |

  - (a) What is the defining relation and complete alias structure for this design?
  - (b) What is the resolution of this design?
  - (c) The fermentations were carried out batchwise in Pyrex flasks. After 72 hours of fermentation, the levan produced was extracted from the fermented medium and its dry weight was determined. The results (in g·L⁻¹) for the 8 experiments (in standard order) were: 4.70, 14.67, 1.71, 3.73, 9.47, 7.61, 0.15, 4.78. From this data, calculate the 7 effects and make a normal probability plot to determine what is significant.
  - (d) Delete the smallest three effects and fit the model again. Are the four effects left in the model significant?
  - (e) Based on the effect heredity principle, what do you think the significant string of aliased two-factor interactions could represent?
  - (f) Can the design be collapsed to a full factorial by ignoring insignificant factors?
  - (g) Based on what you said in (e) write an interpretation of the significant effects and interaction. Based on your model determine the factor levels that will produce the maximum dry weight of levan.

- 3. Use SAS ADX to create a quarter fraction $2^{5-2}$ design.
  - (a) Examine the Confounding rules used by SAS ADX to create the design.
  - (b) Modify the SAS code for exercise 1 to create the same design.
  - (c) Determine the defining relation.
  - (d) Verify that the alias structure in SAS ADX (for this design) can be obtained from the defining relation you found in (c).
  - (e) Suppose that after analysis of data from this experiment that two main effects A and D appear to be significant. Because of the confounding between main effects and two-factor interactions, interpreting the results to mean that these two main effects are the only significant effects could be misleading. Using the effect heredity principle, suggest two alternate plausible models that could explain the data.
  - (f) List the experiments in a foldover fraction that you could use to augment the original eight experiments in order to remove the aliasing between main effects and two-factor interactions.

- 4. Erhart (2007) ran a $2^{8-4}$ fractional factorial experiment to determine the factors that affect flight time of paper helicopters. The standard design is shown in the figure below with all dimensions in centimeters. The factors

![](img/878b651cdbe9da3d6d22e64d64b8a54f_263_0.png)

and levels (in centimeters) he studied are shown in the table below. The low level on paper weight was phone book white pages paper, and the high level was standard copy paper. The fold direction was against (opposite to) or with the direction of rotation.

| Label | Factor | - | + |
|---|---|---|---|
| A | Rotor length | 5.5 | 11.5 |
| B | Rotor width | 3.0 | 5.0 |
| C | Body length | 1.5 | 5.5 |
| D | Foot length | 0.0 | 2.5 |
| E | Fold Length | 5.0 | 11.0 |
| F | Fold width | 1.5 | 2.5 |
| G | Paper weight | telephone book page | copy paper |
| H | Fold direction | against | with |

  - (a) What would you recommend for the generators of a $2^{8-4}$ design? Create the design you recommend in (a) and randomize the order of the runs. What is the experimental unit?
  - (b) List the aliases (up to three-factor interactions) for the 15 effects that can be estimated.
  - (c) Actually run the experiments by making the helicopters and timing them with a stopwatch.
  - (d) Calculate the effects (or regression coefficients) and make a half-normal plot of the effects.
  - (e) Using the principle of effect heredity, try to determine what any strings of aliased two-factor interactions, that appear significant on your plot, represent.
  - (f) Which factors would you include in a follow-up design to determine the combination of factor levels that produces the optimum flight time.

- 5. Create a $2^{7-3}$ design in the SAS data step with generators $E = ABC, F = ABD, G = ACD$.
  - (a) Determine the defining relation for this design.
  - (b) Determine the confounded strings of two-factor interactions that can be estimated from this design.
  - (c) Suppose that after the analysis of data from this experiment, the significant effects appear to be B, BC + AE + FG and BE + AC + DG. What foldover fraction would you recommend in order to determine which specific interactions are causing the two strings of confounded interactions to appear significant.
  - (d) List the experiments in the foldover fraction you recommend in part (c).

- 6. Consider the experiment to study factors that affect the percent removal of arsenic from drinking water using an iron coated sand filter.

