
each individual on the construct being examined.¹ Thus, the computation of weighted factor scores makes sense and was a natural progression over a period of many decades of research. However, it is important to recognize the intricate nature of the factor score computation. There are many methods of computing factor scores and no single universal technique. In addition, factor scores can be sensitive to the extraction and rotation methods used (DiStefano, Zhu, & Mîndrilă, 2009).

The practice of factor score estimation introduced a new assumption into our analyses: that the factor loadings (correlations between an item and the factor) are stable and reasonable estimates of the dynamics within a population. A corollary, of course, is that the factor loadings are valid (invariant) for all subgroups being examined. A similar set of assumptions and corresponding issues is present in linear modeling /regression analyses, particularly when researchers are using multiple regression to predict outcomes for individuals. (For papers on prediction in regression, see Osborne, 2000, 2008.) Specifically, the issue is that these procedures can overfit the data. Most samples contain idiosyncratic aspects that most quantitative analyses will take advantage of in order to fit the model, despite those sample characteristics being nonreproducible (Thompson, 2004, p. 70). Because of this issue, we recommended in earlier chapters that we focus on replication and evaluate the anticipated precision or variability across samples to evaluate the goodness of EFA results. However, factor score estimation can be considered a relatively common practice and thus a book about EFA might not be complete without mentioning this practice. Therefore, here are our goals for this chapter:

- 1 Review some basic aspects of computing factor scores.
- 2 Review how the solutions that result from EFA can be unstable across samples, which can contribute to instability of factor scores.

## Example Syntax and Output

Two basic procedures exist for producing factor scores in SAS: 1) a predefined SAS option and 2) a program-it-yourself option. As you might imagine, the predefined SAS option is by far the easier. When you include the OUT=output-data-set-name option on the FACTOR statement (SAS, 2015), SAS will automatically output a data set that contains all of your original data along with an estimate of weighted factor scores (e.g., Factor1, Factor2, etc.). SAS computes the factor scores as a linear combination of a standardized version of our variables (i.e., with a mean of 0 and a standard deviation of 1) and something called the standardized scoring coefficients.² The scoring coefficients are essentially the regression coefficients used in the computation of the factor scores. Note that these are different from the pattern matrix loadings, which are viewed as the regression coefficients for computing the communalities. It is important that you specify the desired number of factors to extract and the extraction and rotation methods when using this method; if you do not, SAS will use the default options of extracting the minimum number of factors recommended by the proportion of variance and the minimum eigenvalue criteria (see Chapter 3, “Factor Extraction Criteria,” on page 33) and performing principal components analysis with no rotation. An example of the syntax to estimate factor scores, using this method for the engineering data, is presented below.

```
proc factor data = engdata nfactors = 2 method = prin priors = SMC rotate = OBLIMIN out=factor_scores1;
var EngProb: INTERESTeng: ;
run;
```

An example of the data set output by the above syntax is presented in Figure 9.1 on page 161. Note the factor scores are always appended to the end of the data set.

### Figure 9.1 Factor scores output by the OUT statement

| INTERESTeng4 | INTERESTeng5 | INTERESTeng6 | Factor1 | Factor2 |
| :--- | :--- | :--- | :--- | :--- |
| 6 | 7 | 7 | 0.7962651676 | 0.6604940082 |
| 7 | 7 | 7 | 1.6222928986 | 1.0862679178 |
| 6 | 6 | 5 | -0.021803084 | -0.348717039 |
| 6 | 5 | 5 | -0.035478843 | -0.539327043 |
| 7 | 6 | 7 | 1.308684714 | 0.3708796572 |
| 6 | 6 | 6 | -1.202473823 | -0.021525577 |
| 3 | 5 | 5 | 0.754992655 | -2.188145724 |
| 7 | 7 | 7 | 1.6222928986 | 1.0862679178 |
| 6 | 6 | 6 | 0.4076043415 | -0.214541205 |
| 6 | 6 | 6 | 0.4540395521 | 0.0073631982 |
| 6 | 6 | 6 | -3.271861285 | 0.1722012358 |
| 7 | 7 | 7 | 0.3870097678 | 1.0664138721 |
| 6 | 6 | 6 | -1.468030696 | -0.10499217 |
| 6 | 6 | 6 | 0.3175199537 | 0.3094655347 |
| 4 | 4 | 5 | -0.71565535 | -1.87973315 |
| 7 | 6 | 6 | 0.2754235235 | 0.5105299818 |
| 7 | 7 | 7 | -0.759471801 | 1.03740319 |
| 7 | 7 | 7 | 0.60300251 | 1.1084506835 |
| 6 | 6 | 6 | 1.6093502558 | -0.105548033 |
| 4 | 4 | 4 | -0.861718881 | -2.081203918 |
| 6 | 6 | 6 | -0.832571262 | -0.006356835 |

1 Keep in mind that others might use the pattern matrix loadings instead of the standardized scoring coefficients when estimating factor scores. See DiStefano et al. (2009) or (Grice, 2001) for more information about these methods.

The other way of estimating factor scores—the program-it-yourself way—is often more complex. You will need to write your own code, which might contain a number of procedures or DATA steps. Some options that might be useful for this are the SCORE and OUTSTAT=output-data-set-name options. Both options are added to the FACTOR step. The SCORE option will print the standardized scoring coefficients, and the OUTSTAT option will output a data set that contains the various results (e.g., pattern loadings, communalities, etc.) from the analysis. The standardized scoring coefficients are also included in this data set when the SCORE option is used in conjunction with the OUTSTAT option. This information can be useful in the various calculations of factor scores. A simple example of the syntax to estimate equally weighted improper factor scores (discussed in the next section) is presented below.

```
data factor_scores2;
set engdata;
Factor1=mean(of EngProbSolv:); *compute mean of all items in the
engineering problem solving scale;
Factor2=mean(of INTERESTeng:); *compute mean of items in the
interest in engineering scale;
run;
```

## Application: Factor Score Estimation

Now, let's walk through an example to demonstrate some of the challenges and issues associated with the estimation of factor scores. We use the following syntax to run our factor analysis for the engineering data, to output a data set called factor_scores1 containing the predefined SAS factor scores (based on the standardized scoring coefficients) for each individual, to output a data set called Results that contains the pattern loading and standardized scoring coefficients along with other summary results, and to output a table containing the standardized scoring coefficients. The two output data sets and the summary table were requested by adding the OUT=, OUTSTAT=, and SCORE options to the FACTOR step, as described above.

```
proc factor data = engdata nfactors = 2 method = prin priors = SMC
rotate = oblimin out=factor_scores1 outstat=results score;
var EngProb: INTERESTeng: ;
run;
```

The pattern loading matrix and the standardized scoring coefficients output by SAS are presented in Table 9.1 on page 163. These two sets of coefficients represent different potential weights that could be used to estimate factor scores and that we will use for the current example. We include the pattern matrix because you are likely to be more familiar with it, and we present the standardized scoring coefficients as a representation of the built-in SAS weights for computing factor scores.

### Table 9.1 Pattern coefficients and standardized score coefficients from engineering data

| Var: | Rotated pattern coefficients 1 | Rotated pattern coefficients 2 | Standardized scoring coefficients 1 | Standardized scoring coefficients 2 |
|---|---|---|---|---|
| EngProbSolv1 | .859 | -.016 | .142 | -.013 |
| EngProbSolv2 | .841 | -.071 | .091 | -.010 |
| EngProbSolv3 | .879 | -.008 | .147 | .010 |
| EngProbSolv4 | .909 | -.025 | .187 | -.006 |
| EngProbSolv5 | .886 | .021 | .158 | .006 |
| EngProbSolv6 | .869 | .020 | .140 | .008 |
| EngProbSolv7 | .868 | .033 | .151 | .021 |
| EngProbSolv8 | .790 | .072 | .084 | .009 |
| INTERESTeng1 | .042 | .801 | .003 | .086 |
| INTERESTeng2 | -.023 | .921 | .001 | .225 |
| INTERESTeng3 | -.014 | .922 | -.004 | .233 |
| INTERESTeng4 | -.001 | .904 | .012 | .178 |
| INTERESTeng5 | -.007 | .897 | .001 | .209 |
| INTERESTeng6 | .009 | .864 | .002 | .131 |

The syntax provided above will output a data set containing factor scores for each individual in the data set based on the predefined SAS method of computing scores, which in turn is based on the standardized scoring coefficients. However, we must do some additional work to compute factor scores based on the pattern matrix. This syntax, along with explanatory notes, is provided below.

```
* Grab and restructure pattern loadings;
data coeff_online (keep=F1_: F2_: merge);
set results end=last;
*Array of new variables to contain all loadings in one line;
array newVar{2,14} F1_EngProbSolv1-F1_EngProbSolv8 F1_INTERESTeng1-
F1_INTERESTeng6 F2_EngProbSolv1-F2_EngProbSolv8 F2_INTERESTeng1-
F2_INTERESTeng6;
```
