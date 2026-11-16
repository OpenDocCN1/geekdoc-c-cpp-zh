
Heywood, H. B. (1931). On finite sequences of real numbers. *Proceedings of the Royal Society, Series A*, 134(824), 486-501.

Ichikawa, M., & Konishi, S. (1995). Application of the bootstrap methods in factor analysis. *Psychometrika*, 60(1), 77-93. doi: 10.1007/bf02294430

Hunter, J. E. (1997). Needed: A Ban on the Significance Test. *Psychological Science*, 8(1), 3-7. doi: 10.1111/1467-9280.00197.b00534.x

Killeen, P. R. (2008). Replication Statistics. In J. W. Osborne (Ed.), *Best Practices in Quantitative Methods* (pp. 103-124). Thousand Oaks CA: Sage Publications.

Osborne, J. W. (2015). *Best Practices in Logistic Regression*. Thousand Oaks, CA: SAGE Publications.

Pennell, R. (1972). Routinely computable confidence intervals for factor loadings using the 'jack-knife'. *British Journal of Mathematical and Statistical Psychology*, 25(1), 107-114. doi: 10.1111/j.2044-8317.1972.tb00481.x

Schmidt, F. L. (1996). Statistical significance testing and cumulative knowledge in psychology: Implications for training of researchers. *Psychological Methods*, 1(2), 115-129.

Thompson, B. (2002). What future quantitative social science research could look like: Confidence intervals for effect sizes. *Educational Researcher*, 31(3), 25-32.

Thompson, B. (2004). *Exploratory and confirmatory factor analysis: Understanding concepts and applications*: Washington, DC. American Psychological Association.

Wilkinson, L. (1999). Task Force on Statistical Inference, APA Board of Scientific Affairs (1999). Statistical methods in psychology journals: guidelines and explanations. *American Psychologist*, 54(8), 594-604.

Yu, C. H. (2003). Resampling methods: concepts, applications, and justification. *Practical Assessment, Research & Evaluation*, 8(19), 1-23.

Zhang, G., Preacher, K. J., & Luo, S. (2010). Bootstrap confidence intervals for ordinary least squares factor loadings and correlations in exploratory factor analysis. *Multivariate Behavioral Research*, 45(1), 104-134. 10.1080/00273170903504836

Zientek, L. R., & Thompson, B. (2007). Applying the bootstrap to the multivariate case: Bootstrap component/factor analysis. *Behavior Research Methods*, 39(2), 318-325. doi: 10.3758/bf03193163

## Data Cleaning

- The Importance of Data Cleaning ........................ 141
- Outliers ................................................ 142
- Two Types of Outliers in EFA ............................ 142
- Response Sets and Unexpected Patterns in the Data ....... 143
- How Common Is Random Responding? ........................ 145
- Detection of Random Responding .......................... 145
- Application: Random vs Constant Responding .............. 147
- Missing Data ............................................ 149
- What Is Missing or Incomplete Data? ..................... 149
- Dealing with Missing Data ............................... 151
- Application: Nonrandom Missingness and Imputation ....... 152
- Summary ................................................. 155
- Exercises ............................................... 155
- References .............................................. 156

## The Importance of Data Cleaning

If this is not the first book or article by the first author that you have come across, you might know that he has been a constant (perhaps tiresome) advocate of the argument that data is not ready to analyze until it is clean and missing data has been dealt with. In fact, he wrote an entire book about all the different—legitimate—things a researcher can do to improve the quality of their data and the results that come from analysis of those data.

Exploratory factor analysis is no exception, but there are different issues, and different priorities when dealing with EFA. Residuals, a common tool used to identify outliers in inferential statistics, contradict the exploratory nature of EFA¹ and thus they cannot be used for EFA. Instead, a number of other tools and techniques are used to identify overly influential cases. Missing data is also increasingly problematic to EFA. The factor analysis model cannot handle missing data and decreases such cases by default. This process can introduce systematic error and bias into the results. Therefore, missing data should be reviewed and potentially dealt with, via various methods, prior to EFA.

In this chapter we aim to provide a brief look at the issue of data cleaning for EFA. Specifically, we seek to discuss two particular threats to EFA—outliers and missing data—and the methods for dealing with them. A thorough review of this topic and the associated SAS procedures is beyond the scope of this book. Interested readers are encouraged to seek out additional information on their own.

## Outliers

## Two Types of Outliers in EFA

There are two different types of outliers in factor analysis.² The first type of outlier is a case (or value) that does not belong. There are many reasons why cases might not belong: the case could be from a different population, could be the result of data recording or entry error, could have resulted from motivated misreporting, or could represent a small subgroup with a different factor structure that has not been recognized. Whatever the reason, having these "illegitimate" cases in the data does not serve any useful purpose. When you identify such a case, you should check the original data, if it is available, to identify whether the case suffers from a data entry or key error. It might be possible to fix the data manually. Alternatively, you could remove it and then use missing-data techniques (described below) to replace it with a reasonable estimate of what it might have been.

The second type of outlier in EFA is a variable that does not belong. In this context, a variable can be considered an outlier when it loads on its own factor as a single-item factor. If an item does not load on any other factor, and no other items load on that factor, it is considered an outlier, and should be removed from the analysis (or the scale should be reworked to more fully represent that dimension of the latent construct if it is a legitimate facet of the construct).

Many outliers can be identified through careful review of data and analyses. The out-of-bounds value (a subtype of the first outlier) can usually be identified through frequency distributions of the variables to be analyzed. Anything off the scale or out of plausible range should be reviewed. PROC FREQ can be used to produce such tables. This type of examination should always be the first step for researchers. The second type of outlier, the variable that does not belong, is even easier to identify. This is the variable in your analysis that does not play well with others and instead takes a factor for itself. This variable should be removed, and the analysis should be rerun.

1 Estimation of residuals assumes an accurate model, and we cannot make that assumption in EFA.

2 In this context, we will use the term 'outlier' to loosely describe a thing that does not belong. There are more technical definitions for different contexts, but you will have to indulge us here. There are also some in the scholarly community who insist that removing outliers (and indeed, data cleaning in general) is detrimental to the scientific process. The first author has published many articles, given numerous talks and, ultimately, wrote an entire book to empirically demonstrate why this position is wrong-headed.

The individual case that is an outlier (the other subtype of the first outlier) is trickier to identify in EFA. Visual examination of the data can help one identify odd patterns for review and potential elimination (like the participant who answers “3” to every item). Other patterns, like random responding or motivated misresponding, are more difficult to identify. These patterns can be classified into response sets that individuals use to mask or filter their true belief or response. Each is associated with a different motive and outcome, and only some might be detected. We discuss these response sets and the challenges associated with them in the following section.

## Response Sets and Unexpected Patterns in the Data

Response sets¹ (such as random responding) are strategies that individuals use (consciously or otherwise) when responding to educational or psychological tests or scales. These response sets range on a continuum from unbiased retrieval (where individuals use direct, unbiased recall of factual information in memory to answer questions) to generative strategies (where individuals create responses not based on factual recall because of inability or unwillingness to produce relevant information from memory; see Meiser, 1994, p. 43). Response sets have been discussed in the measurement and research methodology literature for over seventy years now (Cronbach, 1942; Goodfellow, 1940; Lorge, 1937), and some (e.g., Cronbach, 1950) argue that response sets are ubiquitous, found in almost every population on almost every type of test or assessment. In fact, early researchers identified response sets on assessments as diverse as the Strong Interest Inventory (Strong, 1927); tests of clerical aptitude, word meanings, temperation, and spelling; and judgments of proportion in color mixtures, seashore pitch, and pleasantness of stimuli. (See summary in Cronbach, 1950, Table 1.)

Response sets can be damaging to factor analysis and to the quality of measurement in research. Much of the research we as scientists perform relies upon the goodwill of research participants (students, teachers, participants in organizational interventions, minimally compensated volunteers, etc.) with little incentive to expend effort in providing data to researchers. If we are not careful, participants with lower motivation to perform at their maximum level might increase the error variance in our data, masking real effects of our research. In the context of this book, random and motivated misresponding can have deleterious effects such as masking a clear factor structure or attenuating factor loadings and communalities.

Here are some examples of response sets that are commonly discussed in the literature:
