when the physical requirements of experimentation make it impossible to test all levels of the treatment factor within each block of experimental units. Incomplete block designs are commonly used in agricultural experimentation, animal science, educational testing and food science.

As an example of a situation where an incomplete block design would be useful, consider the following situation. In food science, taste panels are often used to test palatability of new recipes for new food products. In these panels, subjects are asked to taste and rate different recipes. The different recipes represent the levels of the treatment factor. A random sample of subjects (or the experimental units) is included to represent the potential market. Since there is wide variability in taste among subjects it is better to use a blocked design where each subject tastes and rates each recipe. However, if there are many recipes to be tested, subjects will lose their ability to discriminate and it will be difficult to detect any differences. A solution is to have each subject (block) taste only a subset of the recipes.

# 7.2 Balanced Incomplete Block (BIB) Designs

Care must be taken when choosing the subset of treatment combinations tested in each block of an incomplete block design. If one treatment factor level is left out of every block, it cannot be compared to the other treatment levels. If different treatment levels are unequally represented, some comparisons of factor levels will have more precision than others.

The optimal way to create an incomplete block design is to have each treatment level equally replicated and appearing within a block with every other treatment level an equal number of times. This is called a balanced incomplete block design or BIB. By doing this, all pairwise differences of least squares treatment means will have the same standard error, and the power for detecting a difference in any two means will be the same.

The simplest way to construct a BIB for the case where there are $t$ levels of the treatment factor and $k < t$ experimental units per block is to form all possible subsets of $k$ treatment levels chosen from $t$. For example, in the taste panel described above, if there were $t = 6$ recipes to be tested, and it was determined that each subject could taste at most $k = 3$ recipes without losing discriminatory power, $\binom{6}{3} = 20$ subjects would be required. All possible subsets are listed below.

+   (1 2 3), (1 2 4), (1 2 5), (1 2 6), (1 3 4)
+   (1 3 5), (1 3 6), (1 4 5), (1 4 6), (1 5 6)
+   (2 3 4), (2 3 5), (2 3 6), (2 4 5), (2 4 6)
+   (2 5 6), (3 4 5), (3 4 6), (3 5 6), (4 5 6)

Thus, subject one would taste recipes 1, 2 and 3 in a random order; subject 2 would taste recipes 1, 2 and 4, etc. This plan is completely balanced in that each treatment level or recipe is replicated $r = 10$ times (or tested by 10 subjects) and each pair of treatment levels occurs together in the same block $\lambda = 4$ times. For example, treatment levels 1 and 2 occur together only in the