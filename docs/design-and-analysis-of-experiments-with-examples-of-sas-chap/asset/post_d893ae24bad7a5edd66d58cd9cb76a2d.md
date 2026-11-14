
should be used. This design is then called a completely randomized fractional factorial design of CRFF. The design resulting from the code above is shown below in standard order (not randomized).

| Obs | A | B | C | D | E |
|---|---|---|---|---|---|
| 1 | -1 | -1 | -1 | -1 | 1 |
| 2 | 1 | -1 | -1 | -1 | -1 |
| 3 | -1 | 1 | -1 | -1 | -1 |
| 4 | 1 | 1 | -1 | -1 | 1 |
| 5 | -1 | -1 | 1 | -1 | 1 |
| 6 | 1 | -1 | 1 | -1 | -1 |
| 7 | -1 | 1 | 1 | -1 | 1 |
| 8 | 1 | 1 | 1 | -1 | -1 |
| 9 | -1 | -1 | -1 | 1 | -1 |
| 10 | 1 | -1 | -1 | 1 | 1 |
| 11 | -1 | 1 | -1 | 1 | -1 |
| 12 | 1 | 1 | -1 | 1 | 1 |
| 13 | -1 | -1 | 1 | 1 | 1 |
| 14 | 1 | -1 | 1 | 1 | -1 |
| 15 | -1 | 1 | 1 | 1 | -1 |
| 16 | 1 | 1 | 1 | 1 | 1 |

To illustrate the analysis of a 2k-1 design, consider a continuation of the dry soup mix example presented in Section 5.4.3. In that example, the majority of variability in the soup “intermix” was found to be within a batch rather than between batches. The researchers responsible for the project made a list of factors that they thought might influence the variability within a batch (see Hare, 1988). These were options that could be changed on the mixer where a batch was mixed and the intermix was added through ports. The list consisted of: (1) the number of ports where intermix was added, (2) the temperature of the mixer (that could be controlled by adding cooling water to the jacket surrounding it), (3) the mixing time, (4) weight of the batch, and (5) the delay time between mixing and packaging. The response or variability in fill weights of the intermix was obtained by taking five consecutive samples of the soup mix every 15 minutes as the batch was being packaged. The factor labels and levels are shown in Table 6.3.

## Table 6.3 Factors and Levels for Soup Mix 2^(5-1) Experiment

| Factor Label | Name | Low Level | High Level |
|---|---|---|---|
| A | Number of Ports | 1 | 3 |
| B | Temperature | Cooling Water | Ambient |
| C | Mixing Time | 60 sec. | 80 sec. |
| D | Batch Weight | 1500 lbs | 2000 lbs |
| E | Delay Days | 7 | 1 |

The normal batch size was 2000 lbs and the normal mixing time was 60 seconds. Since this experiment was to be run in a production facility, the research and production staff both had to agree to the plan. The factor levels could not be changed between batches with relatively little effort and they were not a problem. The requested reduction in batch weight and the increase in mixing time for some batches in the planned list of experiments would not seriously interfere with the production schedule if the list was short, but it would slow production if a 32-run design were used. For this reason a 16-run fractional factorial plan was agreed upon. The alias structure for the 2^(5-1) plan shown above is:

- A + BCDE
- B + ACDE
- C + ABDE
- D + ABCE
- E + ABCD
- AB + CDE
- AC + BDE
- AD + BCE
- AE + BCD
- BC + ADE
- BD + ACE
- BE + ACD
- CD + ABE
- CE + ABD
- DE + ABC

Therefore, if three-factor and four-factor interactions could be assumed negligible, estimates of all main effects and two-factor interactions could be made. The experimental unit for this experiment was the batch of dried soup mix put in the mixer, and Table 6.4 shows a randomized list of the 2^(5-1) experiments in actual factor levels. The response y_r was an estimate of the standard deviation of fill weight within a batch, computed from the sampling study made during packaging of each batch.

The SAS commands, to read in the data (in standard order) and to merge it with the design in coded factor levels created earlier, are shown on the next page.

```
data Process;
input 5 68;
datalines;
1.13 1.25 .97 1.70 1.47 1.28 1.18 .98
.78 1.36 1.85 .62 1.09 1.10 .76 2.1
data soup; merge design process;
```

## Table 6.4 2^(5-1) Experiment To Determine Which Factors Are Associated with Fill Variation in Random Order

| Batch | (A) Number of Ports | (B) Temperature | (C) Mixing Time (sec) | (D) Batch Weight (lbs) | (E) Delay (days) | Response $\sigma_p$ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | Cooling Water | 60 | 2000 | 7 | 0.78 |
| 2 | 3 | Cooling Water | 80 | 2000 | 7 | 1.10 |
| 3 | 3 | Ambient | 60 | 1500 | 1 | 1.70 |
| 4 | 3 | Cooling Water | 80 | 1500 | 1 | 1.28 |
| 5 | 1 | Ambient | 60 | 1500 | 7 | 0.97 |
| 6 | 1 | Cooling Water | 80 | 1500 | 7 | 1.47 |
| 7 | 1 | Ambient | 60 | 2000 | 1 | 1.85 |
| 8 | 3 | Ambient | 80 | 2000 | 1 | 2.10 |
| 9 | 1 | Ambient | 80 | 2000 | 7 | 0.76 |
| 10 | 3 | Ambient | 60 | 2000 | 7 | 0.62 |
| 11 | 1 | Cooling Water | 80 | 2000 | 1 | 1.09 |
| 12 | 1 | Cooling Water | 60 | 1500 | 1 | 1.13 |
| 13 | 3 | Cooling Water | 60 | 1500 | 7 | 1.25 |
| 14 | 3 | Ambient | 80 | 1500 | 7 | 0.98 |
| 15 | 3 | Cooling Water | 60 | 2000 | 1 | 1.36 |
| 16 | 1 | Ambient | 80 | 1500 | 1 | 1.18 |

The SAS commands to fit the model in the main effects and two-factor interactions and to make a normal probability plot of the regression coefficients, are shown on the next page. This is the same thing that was done in Section 3.7.5, except only 15 terms are included in the model rather than the full model which would contain main effects and interactions up to order 5. Each effect in this model is confounded with one other interaction as shown in the alias pattern on the previous page. Therefore only 15 effects can be estimated.

As can be seen in the normal plot of effects, the main effect E (Delay Time between mixing and packaging), BE (the interaction between Temperature and Delay Time), and DE (the interaction between Batch Weight and Delay Time) appear to be significant. If the hierarchical effect ordering can be assumed, this is the correct interpretation, and the three-factor and four-factor interactions can be assumed negligible.

```
proc glm data=soup;
model =A B C D E A*B A*C A*D A*E B*C B*D B*E C*D
C*E D*E/solution;
output out=ParameterEstimates=sol;
run;
data nplot; set sol;
estimate=estimate;
if '_n_=1' drop StdErr tValue Probt;
*proc rank calculates normal scores for parameter estimates;
proc rank data=work.nplot out=nplots normal=blon; var estimate;
ranks zscore;
proc nplots; set nplots;
if abs(zscore)<=.9 then parameter=' ';
run;
run;
ods graphics on;
proc sgplot data=nplots;
scatter x=zscore y=estimate/datalabel=parameter;
yaxis label='Normal Scores';
xaxis label='Regression Coefficient';
run;
ods graphics off;
```

## Figure 6.1 Normal Plot of Effects from Full Variability Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_221_0.png)

E=Delay Time has a positive effect (as seen on the normal plot); this would normally mean that increasing the Delay Time between mixing and packaging would increase the response (or within batch variation). However, due to the unconventional assignment of 7 to the low (coded) level of factor E and 1 to the high (coded) level in Table 6.3, it actually tells us that on the average increasing the delay time between mixing and packaging decreases the within batch variability. Since the interactions BE and DE also appear to be significant, the average main effect of factor E does not tell the whole story. Figure 6.2 shows the interaction plot for Temperature and Delay Time. Here it can be seen that Delay Time has little effect on the within batch variability if the mixer is cooled with cooling water during mixing. However, the within batch variability is decreased substantially by increasing delay time between mixing and packaging if the mixing was done at ambient temperature.

## Figure 6.2 Interaction Plot for Mixing Temperature by Delay Time

![](img/878b651cdbe9da3d6d22e64d64b8a54f_222_0.png)

Figure 6.3 shows the interaction plot for Batch Weight and Delay Time. Here it can be seen that increasing the delay time between mixing and packaging has little effect on the variability within a batch for small (1500 lbs.) batches, while increasing the delay time between mixing and packaging decreases within batch variability for large (2000 lbs.) batches.

Based on the results of this study, the minimum variation of intermix within a batch could be obtained by using the larger batch size (2000 lbs.), the ambient temperature at mixing, and a 7-day delay between mixing and packaging. It did not answer a new question prompted by the results: does it take a full 7-day delay between mixing and packaging or could a 3-day or 4-day delay reduce variability just as much? However, the production and research staff agreed that the current results made sense, since the uniformity of intermix related to the hardness of the vegetable oil which is affected by temperature and
