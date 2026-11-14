# Figure 7.3 Half-Normal Plot of Absolute Regression Coefficients from Mouse Growth Experiment

![](bbox=[0.15, 0.12, 0.86, 0.48])

From the half-normal plot it is clear that the only factor having a significant effect on the weaning weight was G - available food. The calculated effect showed that the weaning weight was on the average 4.24g higher for pups of female mice given free access to food compared to pups of mice whose food intake was restricted to 80% of normal. This is the same conclusion that the authors of the article had reached.

# 7.6.3 Criteria for Choosing Block Defining Contrasts

Care must be exercised when choosing the block defining contrasts for 2^k full factorial or 2^{k-p} fractional factorial designs. To illustrate why, consider the following two examples.

Example 1 consists of blocking a 2^5 factorial into 8 blocks of size 2^2 = 4. To do this k - q = 5 - 2 = 3 block defining contrasts must be chosen. Suppose the interactions ABC, CDE and ABCDE are chosen as the block defining contrasts. Their two-factor generalized interactions ABC(CDE) = ABDE, ABC(ABCDE) = DE, CDE(ABCDE) = AB, and their three-factor generalized interaction ABC(CDE)(ABCDE) = ABC(AB) = C are also confounded, accounting for the 7 degrees of freedom for blocks. The block defining contrasts were all three-factor interactions and above, yet one of their generalized interactions is main effect C that we would not want to confound