# GOING DEEPER: TWO-FACTOR ANOVA USING PROC MIXED 339

| TABLE 14.7 PROC MEANS Output |
| Analysis Variable : HEIGHT |
| FAMILY GENDER N Obs Mean |
| 1 F | 3 | 65.67 |
| M | 2 | 71.50 |
| 2 F | 3 | 64.33 |
| M | 3 | 69.00 |
| 3 F | 1 | 63.00 |
| M | 1 | 64.00 |
| 4 F | 2 | 66.50 |
| M | 3 | 67.67 |

2. Examine how the following PROC MIXED statement is constructed:

```
CLASS FAMILY GENDER;
MODEL HEIGHT = GENDER;
RANDOM FAMILY FAMILY*GENDER;
```

+   * FAMILY and GENDER appear in the CLASS statement because they are grouping-factors.
* The MODEL statement includes only the fixed factor GENDER.
* The RANDOM statement includes the random factors FAMILY and FAMILY*GENDER.

Observe the output table titled “Type 3 Text of Fixed Effects” shown in Table 14.8. This shows the results of a hypothesis test that there is no difference in means by GENDER, which is marginally nonsignificant (p=0.07). SAS reports no testing FAMILY.

| TABLE 14.8 PROC MIXED Output Testing the Fixed Factor |
| Type 3 Tests of Fixed Effects |
| Effect Num DF Den F F Value Pr > F |
| GENDER | 1 | 3 | 7.95 | 0.0667 |

3. To illustrate why it is important to properly classify a random factor as random, change the MODEL to where there are only fixed effects:

```
MODEL HEIGHT = FAMILY GENDER*FAMILY;
```

Run the changed program and observe the (abbreviated) output given in Table 14.9. Note that in this case test for a GENDER effect is significant (p=0.0018). How- (continued)