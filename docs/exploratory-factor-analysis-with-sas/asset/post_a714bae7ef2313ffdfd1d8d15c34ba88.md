
## Types of Rotation

As with extraction, there are many choices of rotation method. In PROC FACTOR, 24 methods are available. Each method uses a slightly different algorithm to achieve the same broad goal — simplification of the factor structure. In general, the rotation methods fall into two broad categories: orthogonal and oblique (referring to the angle maintained between the X- and Y-axes).

Orthogonal rotations produce factors that are uncorrelated (i.e., maintain a 90° angle between axes), and oblique methods allow the factors to correlate (i.e., allow the X- and Y-axes to assume a different angle than 90°). Traditionally, researchers have been guided to orthogonal rotation because (the argument went) uncorrelated factors are more easily interpretable. In addition, the mathematics is simpler, a fact that made a significant difference during much of the 20th century when EFA was performed by hand calculations or on early computers. Orthogonal rotations (which include quartimax, equamax, and varimax) are generally the default setting in other statistical software. However, in PROC FACTOR, there is no default method of rotation—the researcher must specify the method in order for it to occur.

Let us review some of the more common methods of rotation. The first three methods are orthogonal methods (i.e., produce uncorrelated factors) and the latter two are oblique methods (i.e., produce correlated factors).

**Varimax** rotation seeks to maximize the variance within a factor (within a column of factor loadings) such that larger loadings are increased and smaller are minimized. In this way, this method simplifies the factors by identifying a set of variables that have high loadings on one and another set that have high loadings on another. However, some variables might not load strongly on any of the factors.

**Quartimax** tends to focus on rows, maximizing the differences between loadings across factors for a particular variable—increasing high loadings and minimizing small loadings. This method seeks to simplify interpretation at the variable level—it wants each variable to load on one factor, and only one.

**Equamax** is considered a compromise between varimax and quartimax, in that it seeks to clarify loadings in both directions. It attempts to find a solution where factor loadings clearly distinguish the factors, and the variables load on one primary factor.

**Promax** is recommended by Thompson (2004) as the more desirable oblique rotation choice.2 This method starts by actually conducting an orthogonal rotation to clarify the pattern of loadings. It then slowly starts to allow the factors to become correlated through a procrustean rotation (which is less common and not discussed here). The initial method of rotation can be specified through the PREROTATE option. If no option is specified, PROC FACTOR will default to using a varimax rotation.

## Direct oblimin rotation is another oblique rotation that can sometimes be problematic but often gives very similar results to promax

The two oblique methods, promax and oblimin, have parameters that allow the researcher to limit how correlated factors can be. The POWER option raises the factor loadings to a specified power, effectively increasing the correlation of the factors as the power becomes larger. The default power for these methods is 3, but users can adjust the value to any value greater than or equal to 1. A low correlation can be specified as POWER=1, but a high can be specified as POWER=5. Even though researchers can adjust the possible correlation between factors, they cannot force the factors to be correlated if they are not—in other words, you can limit how strongly correlated the factors are, but not the minimum correlation.

Each of the techniques described above is specified on the ROTATE option in the FACTOR procedure. The different rotation methods summarized above can be requested using the following keywords.

```
rotate =
VARIMAX /*Varimax rotation*/
QUARTIMAX /*Quartimax rotation*/
EQUAMAX /*Equamax rotation*/
PROMAX /*Promax rotation*/
COBLIMIN /*Direct Oblimin rotation*/
```

Please note that the mathematical algorithms for each rotation discussed above are different, and beyond the scope of this brief introduction. However, the overall goal of each method is the same: simplicity and clarity of factor loadings. For details about how they achieve these goals, see SAS (2015). For a good overview of the technical details of different versions of varimax rotation, see Forina, Armanino, Lanteri, and Leardi (1989).

## Orthogonal vs Oblique Rotation

Conventional wisdom in the literature and many texts advise researchers to use orthogonal rotation because it produces more easily interpretable results, but this might be a flawed argument. In the social sciences (and many other sciences), we generally expect some correlation among factors, particularly scales that reside within the same instrument or questionnaire (i.e., shared method variance will generally produce nonzero correlations). In practice, even when we create features using an orthogonal method, the factor scores (scores derived from the factor structure; see Chapter 9) are often correlated despite the orthogonal nature of the factors. Therefore, using orthogonal rotation results in a loss of valuable information if the factors are really correlated, and oblique rotation should theoretically render a more accurate, and perhaps more reproducible, solution.¹ Further, in the unlikely event that researchers manage to produce truly uncorrelated factors, orthogonal and oblique rotation produce nearly identical results, leaving oblique rotation a very low-risk, potentially high-benefit choice.

The two sets of methods—orthogonal and oblique—do, however, differ in ease of interpretation. When using orthogonal rotation, researchers have only one matrix to interpret. When using oblique rotations, there are two matrices to review (described in the next section). In our experience—and in many of our examples—the two methods tend to parallel each other in interpretation. So again, in our mind this does not create an insurmountable barrier.

## Interpretation of Factor Matrices

All extracted factors are initially orthogonal (Thompson, 2004), but remain so only as long as the rotation is orthogonal (we discussed this briefly in the section above). In practice, this results in interpretation of one matrix (a pattern matrix) when conducting an orthogonal rotation, and two matrices (a pattern and structure matrix) when conducting an oblique rotation. To further complicate interpretation, an unrotated factor matrix is always output, and a reference structure matrix is output when an oblique rotation is done—neither of which is traditionally interpreted. The presence of multiple matrices, whether they are to be interpreted or not, is a source of much confusion in practice.² Let’s start with a few gentle conceptual definitions of each:

**Unrotated factor matrix coefficients** are generally reported by most statistical software regardless of rotation. They represent the unrotated factor loadings, and are generally not of interest.³ In PROC FACTOR, they appear toward the top of the output in a table entitled “Factor Pattern.” Despite the title, this should not be confused with the pattern matrix that is described below.

**Pattern matrix coefficients** are essentially a series of standardized regression coefficients (betas or βs in the regression world) expressing the variable as a function of factor loadings. These are also output for all rotation models. You can think of these as the list of ingredients in the recipe (e.g., to make Item 13, add 0.70 of factor 1, 0.13 of factor 2, 0.02 of factor 3, etc. Mix well... deliciously). Like regression coefficients, they hold all other variables (factors) in the equation constant when estimating the pattern matrix coefficients. So, if factors are uncorrelated, pattern and structure coefficients are identical. As factors become more strongly correlated, the two types of coefficients will become less alike. Thus, think of pattern matrix coefficients as “row” statistics, describing the individual item’s unique

- 1. However, some authors have argued that oblique rotations produce less replicable results as they might overfit the data to a greater extent. We do not think there is empirical evidence to support this argument, but overfitting the data is a concern to all EFA analyses, as we will discuss later in the book.
- 2. In this section we draw heavily on Thompson (2004), which is always a good reference.
- 3. Except for nerds like us trying to understand all this stuff.
