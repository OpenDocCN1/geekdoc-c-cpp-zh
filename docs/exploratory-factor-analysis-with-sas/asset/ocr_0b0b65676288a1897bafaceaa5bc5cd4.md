2 Examine the different factor scores computed above, the distribution of each, and their respective correlations. How do the methods compare?

3 Use the code presented below to split the engineering data into two data sets. Each data set will contain 197 subjects, of which 175 will be in only in that data set, and 22 will be in both data sets. Compute the weighted proper factor score, using the standardized scoring coefficients as weights (the built-in method in SAS). Compare the factor scores for the 22 subjects that are in both groups. How do the results compare?

```
data data1 data2;
   set engdata;
   recordN = _N_;
   if recordN <= 175 then inGrp='Grp 1';
   if 175 < recordN <= 350 then inGrp='Grp 2';
   if recordN > 350 then inGrp='Both';
   if inGrp in ('Grp 1','Both') then output data1;
   if inGrp in ('Grp 2','Both') then output data2;
   run;
```

# References

Baker, F. B. (1985). _The basics of item response theory_ (1st ed. ed.). Portsmouth, NH:Heinemann.

Bond, T. G., & Fox, C. M. (2007). _Applying the Rasch model: Fundamental measurement in the human sciences: (2_<sup>_nd_</sup> _ed.) Mahwah, NJ: Lawrence Erlbaum Associates._

DiStefano, C., Zhu, M., & Mindrila, D. (2009). Understanding and using factor scores: Considerations for the applied researcher. _Practical Assessment, Research & Evaluation, 14_(20), 1-11.

Embretson, S. E., & Reise, S. P. (2000). _Item response theory for psychologists._ Mahwah, New Jersey: Lawrence Erlbaum Associates.

Grice, J. W. (2001). Computing and evaluating factor scores. _Psychological Methods, 6_(4), 430 - 450.

Osborne, J. W. (2000). Prediction in Multiple Regression. Practical Assessment, Research & Evaluation, 7, n2.

Osborne, J. W. (2008). Creating valid prediction equations in multiple regression: Shrinkage, Double Cross-Validation, and Confidence Intervals around prediction. In J. W. Osborne (Ed.), _Best practices in quantitative methods._ (pp. 299-305). Thousand Oaks, CA: Sage Publications.

Thompson, B. (2004). _Exploratory and confirmatory factor analysis: Understanding concepts and applications:_ Washington, DC: American Psychological Association.