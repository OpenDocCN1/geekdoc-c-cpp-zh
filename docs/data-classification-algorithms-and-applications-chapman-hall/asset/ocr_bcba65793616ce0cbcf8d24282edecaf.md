# TABLE 5.3: Example of Gene Expression Data and Rule Groups

| Rows/conditions | Discretized gene expression data | Class label |
| r1 | a, b, c, d, e | C |
| r2 | a, b, c, o, p | C |
| r3 | c, d, e, f, g | C |
| r4 | c, d, e, f, g | ¬C |
| r5 | e, f, g, h, o | ¬C |

To address the above challenging problems, RCBT discovers the most significant TopkRGS for each row of a gene expression dataset. Note that TopkRGS can provide a more complete description for each row, which is different from existing interestingness measures that may fail to discover any interesting rules to cover some of the rows if given a higher support threshold. As such, the information in those rows that are not covered will not be captured in the set of rules. Given that gene expression datasets have a small number of rows, RCBT will not lose important knowledge.

Particularly, the rule group conceptually clusters rules from the same set of rows. We use the example in Table 5.3 to illustrate the concept of a rule group [50]. Note the gene expression data in Table 5.3 have been discretized. They consist of 5 rows, namely, r1, r2, ..., r5 where the first three rows have class label C while the last two have label ¬C. Given an item set I, its Item Support Set, denoted R(I), is defined as the largest set of rows that contain I. For example, given item set I = {a,b}, its Item Support Set, R(I) = {r1,r2}. In fact, we observe that R(a) = R(b) = R(ab) = R(ac) = R(bc) = R(abc) = {r1,r2}. As such, they make up a rule group {a → C, b → C, ..., abc → C} of consequent C, with the upper bound abc → C and the lower bounds a → C, and b → C.

Obviously all rules in the same rule group have the exactly same support and confidence since they are essentially derived from the same subset of rows [50], i.e. {r1,r2} in the above example. We can easily identify the remaining rule members based on the upper bound and all the lower bounds of a rule group. In addition, the significance of different rule groups can be evaluated based on both their confidence and support scores.

In addition, RCBT has designed a row enumeration technique as well as several pruning strategies that make the rule mining process very efficient. A classifier has been constructed from the top-k covering rule groups. Given a test instance, RCBT also aims to reduce the chance of classifying it based on the default class by building additional stand-by classifiers. Specifically, given k sets of rule groups RG1,...,RGk, k classifiers CL1,...,CLk are built where CL1 is the main classifier and CL2,...,CLk are stand-by classifiers. It makes a final classification decision by aggregating voting scores from all the classifiers.

A number of experiments have been carried out on real bioinformatics datasets, showing that the RCBT algorithm is orders of magnitude faster than previous association rule mining algorithms.

# 5.5 Discussion and Conclusion

In this chapter, we discussed two types of popular rule-based classification approaches, i.e., rule induction and classification based on association rules. Rule induction algorithms generate a small set of rules directly from the data. Well-known systems include AQ by Michalski et al. [36], CN2 by Clark and Niblett [9], FOIL by Quinlan [10], FOCL by Pazzani et al. [37], I-REP by Furnkranz and Widmer [11], and RIPPER by Cohen [13]. Using association rules to build classifiers was proposed by Liu et al. in [30], which also reported the CBA system. CBA selects a small subset