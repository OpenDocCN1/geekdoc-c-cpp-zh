
## CREATING ONE-WAY FREQUENCY TABLES FROM SUMMARIZED DATA

3. To tell SAS to reorder this table in the order in which you specified the categories in the data set (which makes more sense in this example), use the ORDER=DATA option in the statement:

```sas
PROC FREQ ORDER=DATA;
```

Rerun the analysis and observe the new table.

## 10.3.1 Testing Goodness of Fit in a One-Way Table

A good-of-fit test of a single population is a test to determine if the distribution of observed frequencies in the sample data closely matches the expected number of occurrences under a hypothetical distribution for the population. The observations are assumed to be independent, and each data value can be counted in one and only one category. It is also assumed that the number of observations is fixed. The hypotheses being tested follows:

- $H_0$: The population follows the hypothesized distribution.
- $H_a$: The population does not follow the hypothesized distribution.

A chi-square statistic is calculated, and a decision can be made on the $p$-value associated with that statistic. A low $p$-value indicates that the data do not follow the hypothesized, or theoretical, distribution. If the $p$-value is sufficiently low (usually <0.05), you will reject the null hypothesis. The syntax to perform a goodness-of-fit test is as follows:

```sas
PROC FREQ; TABLES variable / CHISQ=(list of ratios);
```

As an example, we will use data from an experiment conducted by the nineteenth-century monk Gregor Mendel. According to a genetic theory, crossbred pea plants show a 9:3:3:1 ratio of yellow peas, green peas, and yellow wrinkled offspring. Of the 556 plants, under the theoretical ratio (distribution) of 9:3:3:1, you would expect about

- $(9/16) \times 556 = 312.75$ yellow peas (56.25%)
- $(3/16) \times 556 = 104.25$ yellow wrinkled peas (18.75%)
- $(3/16) \times 556 = 104.25$ green peas (18.75%)
- $(1/16) \times 556 = 34.75$ green wrinkled peas (6.25%)

After growing 556 of these pea plants, Mendel observed the following:

- 315 have yellow peas
- 108 have yellow wrinkled peas
- 101 have green peas
- 32 have green wrinkled peas

## CHAPTER 10: ANALYZING COUNTS AND TABLES

Do these offspring support the hypothesized ratios? The following Hands-on-Example illustrates the use of SAS PROC FREQ to run a goodness-of-fit test to assess whether the observed frequencies seem to support the theory.

## HANDS-ON EXAMPLE

This example illustrates how to perform a goodness-of-fit-test.

- 1. Open the program file AFREQ4.SAS.

```sas
DATA GENE;
  INPUT @1 COLORTYPE $13. @15 NUMBER 3;
DATALINES
YELLOWSMOOTH 315
YELLOWWRINKLE 108
GREENSMOOTH 101
GREENWRINKLE 32

* HYPOTHIZING A 9:3:3:1 RATIO;
PROC FREQ ORDER=DATA; WEIGHT NUMBER;
TITLE 'GOODNESS OF FIT ANALYSIS'
TABLE COLORTYPE / NOCUM CHISQ
TESTP= (0.5625 0.1875 0.1875 0.0625);
```

Note the following components of this SAS program:

- The data are summarized as indicated by the WEIGHT NUMBER statement in PROC FREQ.
- The ORDER=DATA option causes the output frequencies to be ordered as they were input into the data set.
- Frequencies are based on the variable COLORTYPE.
- The /NOCUM CHISQ and TESTP= statements request the goodness-of-fit test. The test ratios are based on the percent progeny expected from each of the four categories. The NOCUM option requests a table without the cumulative column.
- The NOCUM option instructs SAS not to include the “Cumulative Frequency” column in the table.

Note that you must use the ORDER=DATA option to ensure that the hypothesized ratios listed in the TESTP= match up correctly with the categories in the table.

- 2. Run the program and observe the output, as given in Table 10.9. A graph deviations is also included in the output (in the latest versions of SAS), but not shown here.

It is a good idea to make sure the “Test Percent” column matches the hypothesized percentages for the categories of the tested variable.

Note that in this case, the p-value for the chi-square test is >0.05 (p=0.9254), which leads us to reject the null hypothesis and conclude that the evidence indicates support for the theory that the population exhibits the 9:3:3:1 phenotypic ratios.

## ANALYZING TWO-WAY TABLES

| TABLE 10.9 Goodness-of-Fit Test Using PROC FREQ | |
| COLORTYPE | Frequency | Percent | Test Percent |
| :--- | :--- | :--- | :--- |
| YELLOWSMOOTH | 315 | 56.65 | 56.25 |
| YELLOWWRINKLE | 108 | 19.42 | 18.75 |
| GREENSMOOTH | 101 | 18.17 | 18.75 |
| GREENWRINKLE | 32 | 5.76 | 6.25 |

| Chi-Square for Specified Proportions | |
| :--- | :--- |
| Chi-Square | 0.470 |
| DF | 3 |
| Pr > ChiSq | 0.9254 |

## 10.4 ANALYZING TWO-WAY TABLES

To create a cross-tabulation table using PROC FREQ for relating variables, use the statement with both variables separated by an asterisk (e.g., A*B). A cross-tabulation table is formed by counting the occurrences in cells. The number of columns in a table is denoted by $c$, and the number of rows by $r$. Thus, a table is $r \times c$.

- $H_0$: The variables are independent.
- $H_a$: The variables are not.

Note that the likelihood ratio statistic given in Table 10.9 is an alternative to the chi-square. While the results are usually similar, many practitioners prefer to report the chi-square statistic. The other statistics reported in this table are for special settings and are not discussed here.

| TABLE 10.10 Cross-Tabulation from FREQ | | |
| Frequency | Row Pct | Col Pct | Total |
| :--- | :--- | :--- | :--- |
| Arson | 43 | 46.24 | 50.23 |
| Coining | 14 | 10.87 | 52.75 |
| Fraud | 144 | 69.57 | 30.43 |
| Rape | 62 | 41.33 | 58.67 |
| Stealing | 300 | 44.18 | 55.82 |
| Violence | 110 | 41.51 | 58.49 |
| Total | 673 | 753 | 1426 |
| | 47.19 | 52.81 | 100.00 |

3. Observe the statistics given in Table 10.11. The chi-square value is 49.7 and $p < 0.0001$. Thus, you reject the null hypothesis of no association (independence) and conclude that there is evidence of a relationship between drinking status and type of crime.

```sas
PROC FREQ; TABLES GENDER*DRINK/CHISQ;
```
