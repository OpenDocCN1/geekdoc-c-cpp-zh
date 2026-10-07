# PERFORMING A TWO-SAMPLE T-TEST

the section on one-sample t-tests (i.e., divide the p-value by 2 if the results are consistent with the alternative hypothesis). Key assumptions underlaying the two-sample t-test are that the random samples are independent and that the populations are normally distributed with equal variances. If the data are non-normal, nonparametric tests such as the Mann–Whitney U are available (see Chapter 15: Nonparametric Statistics).
The following are guidelines regarding normality and equal variance assumptions:

**Normality:** As in the one-sample case, rules of thumb are available to help you determine where to go and trust the results of a two-sample t-test even when the data are non-normal. The sample size guidelines given earlier in this chapter for the one-sample test can be used in the two-sample case by replacing $N$ with $N_1 + N_2$ (see Moore, McCabe, and Craig, 2014).

**Equal variances:** There are two t-tests reported by SAS in this setting: one based on the assumption that the variances of the two groups are equal (and thus using a pooled estimate of the common variance) and one (Satterthwaite) not making such assumption. Both methods make the same assumptions about normality. There is no universal agreement concerning which t-test to use.

A conservative approach suggested by statisticians (see Moore, and Craig, 2014) is to always use the version of the t-test (Satterthwaite) that does not assume equal variances. The classical approach to deciding which version of the t-test to use is formally test the variance assumption using an F-test that SAS gives in the t-test output. The decision criterion using this approach is that if the p-value for the F-test is less than α (say 0.05), you conclude that the variances are unequal and use the Satterthwaite t-test. If the p-value for the F-test is greater than α, you use the t-test on a pooled estimate of the variances. At least one of the reasons for the recommendation to always use the Satterthwaite test is that studies have shown that the F-test for assessing whether the variances are unreliable.

> If your observations are related across “groups” as paired or repeated measurements, the two-sample t-test is an incorrect version of the t-test. For that case, see the section on the paired t-test that follows.

# 11.2.1 Running the Two-Sample t-Test in SAS

Two sample t-tests can be obtained using the PROC TTEST procedure which was previously introduced in the context of a one-sample test. In this section, we'll describe PROC TTEST more completely. The syntax for the TTEST procedure is as follows:

```
PROC TTEST <options>; CLASS variable; <statements>;
```

Table 11.3 lists common options and statements used with PROC TTEST. Other options and statements exist for PROC TTEST concerning analyses not discussed in this text. Consult the SAS documentation for more information.