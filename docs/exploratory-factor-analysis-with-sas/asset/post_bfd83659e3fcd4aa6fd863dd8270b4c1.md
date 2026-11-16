
| Example | Sample | Items/Scales | Example Items |
| :--- | :--- | :--- | :--- |
| 2. Marsh Self-Description Questionnaire (SDQ) | 15,661 10th graders from the National Education Longitudinal Study of 1988. | 13 items and 3 scales: parents (5 items), English (4 items), mathematics (4 items) | My parents treat me fairly.<br>I get good marks in English.<br>I do badly in tests of mathematics. |
| 3. Geriatric Depression Scale | 479 older adults from the Long Beach Longitudinal Survey. | 30 items in a scale without a clear factor structure | Do you often get bored?<br>Are you hopeful about the future? |

It is common wisdom that extraction techniques tend to yield similar results. Let us examine this assertion to see whether it holds across our samples.

## Example Syntax and Output

To get started, let's review the syntax and output to produce a factor analysis of the engineering data (example data set 1 in Table 2.1 on page 15). We will use iterated PAF extraction and ask SAS to extract two factors since the items in the data generally represent two scales (please note, in Chapter 3 we will discuss the criteria to determine the number of factors to extract. The syntax to do this is presented below.

```
proc factor data = engdata nfactors = 2 method = PRINIT priors = SMC;
   var EngProbSolv1 EngProbSolv2 EngProbSolv3 EngProbSolv4
   EngProbSolv5 EngProbSolv6 EngProbSolv7 EngProbSolv8
   INTERESTeng1 INTERESTeng2 INTERESTeng3 INTERESTeng4
   INTERESTeng5 INTERESTeng6;
run;
```

Since we are at heart lazy programmers who enjoy shortcuts (where appropriate), we are going to take a minute to explain two handy shortcuts for referring to a set of variables that contain the same prefixes: ranges and lists. Variable ranges require the same prefix and a numeric suffix (e.g., var1 var2 var3). You can then refer to a set of variables by the first variable and last variable in the range separated by a dash (e.g., var1-var3). Variable lists require only an identical prefix. The suffix can be numeric or character (e.g., var011 varXYZ varABC). You can then refer to the set by the common prefix followed by a colon (e.g., var:). There is another type of range that uses a double dash (e.g., --) that refers to variables based on position in the data set, but we do not recommend using that because variable order can change and you can get yourself in trouble. If we used a range or a list with the above syntax, this would change your VAR statement to the following:

```
var EngProbSolv1-EngProbSolv8 INTERESTeng1-INTERESTeng6;
```

```
*OR;
var EngProbSolv: INTERESTeng:;
```

We will use the list notation to refer to variables throughout the remainder of this book to reduce and simplify syntax that we present.

The syntax produces a series of results. Of particular interest to us right now are the communalities and the eigenvalues. We present these results, along with some of the related tables, below. Figure 2.1 on page 17 and Figure 2.2 on page 18 present the initial communalities and eigenvalues extracted. Figure 2.3 on page 18 shows us the iterative estimates of communalities that are produced as SAS attempts to identify stable estimates of the communalities. The final eigenvalues and communalities are presented in Figure 2.4 on page 19, Figure 2.5 on page 19, and Figure 2.6 on page 19. Notice that two different tables are produced to show the final eigenvalues extracted. The first shows the value of all the eigenvalues, and the second shows only the eigenvalues that were extracted.

## Figure 2.1 Initial communality estimates

```
The SAS System
The FACTOR Procedure
Initial Factor Method: Iterated Principal Factor Analysis

Prior Communality Estimates: SMC
```

| EngProbSolv1 | EngProbSolv2 | EngProbSolv3 | EngProbSolv4 | EngProbSolv5 | EngProbSolv6 | EngProbSolv7 |
|---|---|---|---|---|---|---|
| 0.74225891 | 0.69492663 | 0.75168425 | 0.79173824 | 0.79014397 | 0.76641517 | 0.78640575 |

| EngProbSolv8 | INTERESTeng1 | INTERESTeng2 | INTERESTeng3 | INTERESTeng4 | INTERESTeng5 | INTERESTeng6 |
|---|---|---|---|---|---|---|
| 0.66617372 | 0.67364170 | 0.80199479 | 0.81578725 | 0.80569754 | 0.78059756 | 0.73930386 |

## Figure 2.2 Initial eigenvalues extracted

| | Eigenvalue | Difference | Proportion | Cumulative |
|---|---|---|---|---|
| 1 | 7.41147001 | 4.14045379 | 0.56987 | 0.56987 |
| 2 | 3.27101622 | 3.07385573 | 0.3084 | 1.0071 |
| 3 | 0.19716049 | 0.12724260 | 0.0186 | 1.0257 |
| 4 | 0.06991789 | 0.02097769 | 0.0066 | 1.0323 |
| 5 | 0.04894020 | 0.00959991 | 0.0046 | 1.0369 |
| 6 | 0.03934028 | 0.01737713 | 0.0037 | 1.0406 |
| 7 | 0.02196316 | 0.03590061 | 0.0021 | 1.0427 |
| 8 | -.01393745 | 0.01888235 | -0.0013 | 1.0414 |
| 9 | -.03281980 | 0.01385724 | -0.0031 | 1.0383 |
| 10 | -.04667704 | 0.02487962 | -0.0044 | 1.0339 |
| 11 | -.07155666 | 0.01105570 | -0.0067 | 1.0272 |
| 12 | -.08261235 | 0.01464078 | -0.0078 | 1.0194 |
| 13 | -.09725314 | 0.01092932 | -0.0092 | 1.0102 |
| 14 | -.10818246 | | -0.0102 | 1.0000 |

## Figure 2.3 Iterative estimates of communalities

| Iteration | Change | Communalities |
|---|---|---|
| 1 | 0.0230 | 0.7143 0.67528 0.76418 0.80488 0.79669 0.76782 0.77790 0.66895 0.67210 0.82503 0.83455 0.81580 0.79624 0.75064 |
| 2 | 0.0056 | 0.72861 0.67045 0.76741 0.80863 0.79843 0.76826 0.77575 0.67075 0.66984 0.83083 0.83888 0.81707 0.79920 0.75210 |
| 3 | 0.0016 | 0.72787 0.66926 0.76824 0.80954 0.79898 0.76822 0.77520 0.67091 0.66898 0.83246 0.83999 0.81712 0.79976 0.75217 |
| 4 | 0.0005 | 0.72766 0.66897 0.76845 0.80981 0.79901 0.76831 0.77506 0.67094 0.66887 0.83296 0.84031 0.81706 0.79986 0.75211 |

## Figure 2.4 Final eigenvalue estimates

| | Eigenvalue | Difference | Proportion | Cumulative |
|---|---|---|---|---|
| 1 | 7.41735945 | 4.13561079 | 0.6933 | 0.6933 |
| 2 | 3.28174866 | 3.09229491 | 0.3067 | 1.0000 |
| 3 | 0.18945375 | 0.10923108 | 0.0177 | 1.0178 |
| 4 | 0.08022267 | 0.02194042 | 0.0075 | 1.0253 |
| 5 | 0.05828225 | 0.01517213 | 0.0054 | 1.0307 |
| 6 | 0.04311012 | 0.01355272 | 0.0040 | 1.0347 |
| 7 | 0.02955740 | 0.03421141 | 0.0028 | 1.0375 |
| 8 | -0.0465401 | 0.01603057 | -0.0004 | 1.0371 |
| 9 | -0.02068458 | 0.00937260 | -0.0019 | 1.0351 |
| 10 | -0.03005719 | 0.02685945 | -0.0028 | 1.0323 |
| 11 | -0.05691664 | 0.02614394 | -0.0053 | 1.0270 |
| 12 | -0.0306647 | 0.00278501 | -0.0078 | 1.0192 |
| 13 | -0.0885149 | 0.03405705 | -0.0080 | 1.0112 |
| 14 | -1.1990854 | | -0.0112 | 1.0000 |

## Figure 2.5 Final eigenvalues extracted

| Factor1 | Factor2 |
|---|---|
| 7.4173594 | 3.2817487 |

## Figure 2.6 Final communalities extracted

| EngProbSolv1 | EngProbSolv2 | EngProbSolv3 | EngProbSolv4 | EngProbSolv5 | EngProbSolv6 | EngProbSolv7 |
|---|---|---|---|---|---|---|
| 0.72767880 | 0.66896630 | 0.76844749 | 0.80981353 | 0.79900569 | 0.76831462 | 0.77506294 |
| EngProbSolv8 | INTERESTeng1 | INTERESTeng2 | INTERESTeng3 | INTERESTeng4 | INTERESTeng5 | INTERESTeng6 |
| 0.67094317 | 0.66857315 | 0.83296139 | 0.84031090 | 0.81705556 | 0.79986155 | 0.75211302 |

## Does Extraction Method Matter?

So, now that we have gone through the effort of learning about the different extraction methods and figuring how to run them in SAS, what difference do they really make? Let’s see by comparing the results of five different extraction methods using the data sets summarized in Table 2.1 on page 15. We ran these models using the same syntax presented in the section above, just changing the METHOD option and eliminating the PRIORS option for all except the PAF and iterated PAF methods. We then organized the results into some nice summary tables to permit easy comparison.

### Engineering data.

As we mentioned above, this data usually gives a clear two-factor solution. Table 2.2 on page 20 presents the communality estimates for the initial extraction, and each of the subsequent extraction methods. As you can see, the communalities for the various items are relatively stable despite the relatively small sample size, rarely varying by more than 0.10 across all extraction methods for a particular item. Table 2.3 on page 21 presents the eigenvalues extracted by the various methods. We also see very similar eigenvalues produced across the various methods. This suggests that when basic assumptions are met and factor structure is clear, the extraction method might not matter much.

Table 2.2 Communality estimates for the engineering data across different extraction techniques

| Variable: | Initial | ML | PAF | Iterated PAF | ULS | ALPHA |
|---|---|---|---|---|---|---|
| EngProbSolv1 | .742 | .712 | .731 | .728 | .728 | .733 |
| EngProbSolv2 | .695 | .663 | .675 | .669 | .669 | .669 |
| EngProbSolv3 | .752 | .766 | .764 | .768 | .768 | .769 |
| EngProbSolv4 | .792 | .810 | .805 | .810 | .810 | .810 |
| EngProbSolv5 | .790 | .807 | .797 | .799 | .799 | .796 |
| EngProbSolv6 | .766 | .774 | .768 | .768 | .768 | .767 |
| EngProbSolv7 | .786 | .778 | .778 | .775 | .775 | .774 |
| EngProbSolv8 | .666 | .674 | .670 | .671 | .671 | .669 |
| INTERESTeng1 | .674 | .666 | .672 | .669 | .668 | .668 |
