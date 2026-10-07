# 13.1.1 Using the MEANS or LSMEANS Statement

When you perform a one-way ANOVA, there is a two-step procedure: (1) test $H_0 = \mu_1 = \mu_2 = ... = \mu_h$ to determine whether any significant differences exist, and (2) if $H_0$ is rejected, then run subsequent comparison tests to determine which differences are significantly different. Pairwise comparison of means can be performed using one of several multiple comparison tests specified using the MEANS statement, has the following format (where indentvar a CLASS variable):

```
MEANS in dependentvar / typecomposition <meansoptions>
```

For PROC GLM, use the LSMEANS statement:

```
LSMEANS in dependentvar / typecomposition <meansoptions>
```

Table 13.2 lists comparison options for both ANOVA and GLM. For example, you are comparing the time to relief of three headache medicines – brands 1, 2, and 3. The time-to-relief data are reported in minutes. For your experiment, 15 subjects were randomly placed on one of the three medications. Which (if any) is the most effective? The data for this example are as follows:

| Brand 1 | Brand 2 | Brand 3 |
| 24.5 | 28.4 | 26.1 |
| 23.5 | 34.2 | 28.3 |
| 26.4 | 29.5 | 24.3 |
| 27.1 | 32.2 | 26.2 |
| 29.9 | 30.1 | 27.8 |

# TABLE 13.2 Common type comparison Options for the PROC ANOVA or GLM MEANS Statement (Options Following the Slash /)

| Option | Explanation |
| BON | Bonferroni t-tests of difference |
| DUNCAN | Duncan's multiple range test |
| SCHEFFE | Scheffe multiple comparison procedure |
| SNK | Student Newman–Keuls multiple range test |
| LSD | Fisher's significant difference test |
| TUKEY | Tukey's Standardized range test |
| DUNETT ('x') | Dunnett's test – compares to a single control, where 'x' is the category value of the group MEANS |
| ALPHA=pValue | Specifies the significance level for comparisons (default: 0.05) |
| CLDIFF | Requests that confidence limits are included in the output |

Common typecomparison options for the PROC GLM LSMEANS Statement (options following the slash /)

+   ADJUST=option Specifies type of multiple comparison. Examples are BON, DUNCAN, SCHEEFE, SNK, LSD, and DUNNETT= Calculates p-values base (default is T). You can also specify TUKEY or DUNNETT options