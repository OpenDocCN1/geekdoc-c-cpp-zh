
## Figure 2.20 The Script Menu

![](img/a858f3b35ed4923af65c22e8829ee5a8_39_0.png)

- Data Table Window gives a view of the underlying data table, which is especially useful when there are By-Groups.

## Capability Analysis

The Capability Analysis option gives a capability analysis for quality control applications. The capability study measures the conformance of a process to given specification limits. A dialog prompts you for Lower Spec Limit, Upper Spec Limit, and Target. You only have to enter one of the three values. Only those fields you enter are part of the resulting Capability Analysis table. Optionally, you can enter a known value for sigma, the process standard deviation.

Capability Analyses can calculate capability indices using several different short-term estimates for σ. After requesting a Distribution, select Capability Analysis from the popup menu on the outline bar for the variable of interest. The Dialog box shown in Figure 2.21 appears, allowing specification of long-term or one or more short-term sigmas, grouped by a column or a fixed sample size.

## Figure 2.21 Capability Analysis Dialog Box

![](img/a858f3b35ed4923af65c22e8829ee5a8_39_1.png)

All capability analyses use the same formulas. The difference between the options lies in how sigma is computed. These options for sigma can be explained as:

- Long-term uses the overall sigma. This is the option used for Ppk statistics, and has sigma computed as

σ = √[ Σ (from i=1 to n) (x_i - x̄)² / (n - 1) ]

- **Specified Sigma** allows the user to enter a specific, known sigma used for computing capability analyses. Sigma is, obviously, user-specified and is therefore not computed. This is the option used for control chart-generated capability analyses, where the sigma used in the chart is entered (in the dialog) as the specified sigma.

- **Short Term, Grouped by fixed subgroup size** computes σ using the following formula. In this case, if r is the number of subgroups and each i-th subgroup is defined by the order of the data, sigma is computed as

σ = √[ Σ (i=1 to n) (x_ij - x̄_i.)² / (n - r - 1) ]

- **Short Term, Grouped by Column** brings up a column list dialog from which you choose the grouping column. In this case, with r equal to the number of subgroups, sigma is computed as

σ = √[ Σ (i=1 to n) (x_ij - x̄_i.)² / (n - r - 1) ]

(Note that this is the same formula for Short Term, Grouped by fixed subgroup size and is commonly referred to as the Root Mean Square Error or RMSE.)

**Note:** There is a preference for Distribution called **Ppk Capability Labeling** that will label the long-term capability output with Ppk labels. This option is found using **File > Preferences**.

When you click **OK**, the platform appends a Capability Analysis table, like the one in Figure 2.22, at the bottom of the text reports. You can remove and redo a Capability Analysis as many times as you want.

The specification limits can be stored and automatically retrieved as a column property. To do this, choose **Spec Limits** from the **Save** command menu. When you save the specification limits, they appear on the histogram when opened at a later time.

## Figure 2.22 The Capability Analysis Table

![](img/a858f3b35ed4923af65c22e8829ee5a8_41_0.png)

The Capability Analysis table is organized into two parts. The upper part of the table shows these quantities:

- The Specification column lists the names of items for which values are shown. They are Lower Spec Limit, Upper Spec Limit, and Spec Target.
- The Value column lists the values you specified for each limit and the target
- %Actual is the observed percent of data falling outside the specification limits.

The lower portion of the Capability Analysis table lists five basic process capability indexes, their values, and their upper and lower Confidence Intervals. It also lists the percent and PPM for areas outside the spec limits. The PPM column (parts per million) is the Percent column multiplied by 10,000.

This Sigma Quality measurement is frequently used in Six Sigma methods, and is also referred to as the process sigma.

Sigma Quality = Normal Quantile( 1 − Expected (# defects) / n ) + 1.5

For example, if there are 3 defects in n=1,000,000 observations, the formula yields 6.03, or a 6.03 Sigma process. The above and below columns do not sum to the total column because Sigma Quality uses values from the Normal distribution, and is therefore not additive.

Table 2.1 “Capability Index Names and Computations,” p. 41, describes these indices and gives computational formulas.

## Table 2.1 Capability Index Names and Computations

| Index | Index Name | Computation |
|---|---|---|
| CP | process capability ratio, Cₚ | (USL − LSL)/6σ where USL is the upper spec limit LSL is the lower spec limit |

## Table 2.1 Capability Index Names and Computations (continued)

| CIs for CP | Lower CI on CP | CP√[ χ²_{1-α/w, n-1} / (n-1) ] |
| CIs for CP | Upper CI on CP | √[ χ²_{1-(1-α)/w, n-1} / (n-1) ] |
| CPK (PPK for AIAG) | process capability index, Cₚₖ | min(CPL, CPU) |
| CIs for CPK | Expected Value E(Ĉₚₖ) | Let c = √n (μ - (USL + LSL)/2) / σ denote the noncentrality parameter and d = (USL - LSL)/σ represent the specification limit in σ units. Then the expected value is (1/6)√[(n-1)/(2n)] [Γ((n-2)/2)/Γ((n-1)/2)] (d√n - 2√[2/π] exp((-c²/2) - 2c(1 - 2Φ(-c)))) |
|  | Variance Var(Ĉₚₖ) | Using c and d from above, the variance is [d²/(36) (n-1)/(n-3)] - [d/(9√n) (n-1)/(n-3)] [√[2/π] exp((-c²/2)) + c(1 - 2Φ(-c))] + (1/9)[(n-1)/(n(n-3))](1 + c²) - ((n-1)/(72n))[Γ((n-2)/2)/Γ((n-1)/2)]² (d√n - 2√[2/π] exp((-c²/2) - 2c(1 - 2Φ(-c))))² |
|  | Lower CI | E(Ĉₚₖ) - k√Var(Ĉₚₖ) |
|  | Upper CI | E(Ĉₚₖ) + k√Var(Ĉₚₖ) |

interest such as an engineering specification. When used in capability assessment, Z USL is the distance to the upper specification limit and Z LSL is the distance to the lower specification limit.

Z USL = (USL-Xbar)/sigma = 3 * CPU

Z LSL = (Xbar-LSL)/sigma = 3 * CPL

Z Bench = Inverse Cumulative Prob(1 - P(LSL) - P(USL))

where

P(LSL) = Prob(X < LSL) = 1 - Cum Prob(Z LSL)

P(USL) = Prob(X > USL) = 1 - Cum Prob(Z USL)

**Note:** You can also do a non-normal capability analysis through **Fit Distribution** options, described in the next section. After you fit a distribution, you have the option to generate quantiles and a target value for the fitted distribution. If you give a target value, a capability analysis is automatically generated by using the quantile values and target you specified.

## The Fit Y by X Platform

Any time two variables need to be compared, the Fit Y by X platform is the choice to make. This single platform produces one way ANOVA, scatterplots, and contingency table analysis—most of the two-variable analyses seen in an introductory statistics course.

## Introduction

After starting JMP Student Edition,

- Open the data file Denim.jmp.

Details about this data are found in Chapter 2, “The Distribution Platform” in the section “About the Data,” p. 21.

## Launching the Platform

In this introduction section, the variables are examined in pairs.

- Select Analyze > Fit Y By X from the menu bar.

This brings up the Fit Y By X platform launch dialog as seen in Figure 3.1

Figure 3.1 Fit Y By X Launch Dialog

![](img/a858f3b35ed4923af65c22e8829ee5a8_45_0.png)

Notice the word “Contextual” in the title bar. It is there because this dialog launches other platforms depending on the modeling types (continuous or categorical) of the variables in the analysis. More

information on modeling types is found in “The Modeling Type of Variables,” p. 29. Initially, this example consists of three analyses, with Starch Content (%) as the Y variable in all of them. Method, Size of Load (lbs), and Sand Blasted? are the X variables. All three analyses are requested at the same time to illustrate some of JMP Student Edition’s interactive capabilities. These analyses would be equally valid if performed separately.

- Select Starch Content (%) from the list of columns and click the Y, Response button.
- To select all three X variables, click on Method, hold down the Shift key, then click Sand Blasted?.
- Note that these dialog boxes respond to dragging as well as button clicks, as in the next step.
- Drag these highlighted variables to the box to the right of the X, Factor button.
- Click OK.

Three plots appear as in Figure 3.2.

## Figure 3.2 Fit Y by X Results

![](img/a858f3b35ed4923af65c22e8829ee5a8_46_0.png)

On the far left and far right, dot plots of each level of a nominal variable are plotted side by side, a situation leading to one-way ANOVAs. In the middle plot, JMP Student Edition produces a scatterplot of two continuous variables, a situation leading to fitting lines and curves.

## Computing a t-test

As a simple example, examine the plot on the far right, relating starch content to whether the fabric was sand blasted or not. Is the starch content different for the two levels of Sand Blasted? This is a typical situation examined with a two-sample t-test. To conduct the t-test,

- Select t test from the drop-down menu in the plot’s title bar.

The t-test report appears in the outline beneath the plot labeled t test.

## Figure 3.3 t-test Results

![](img/a858f3b35ed4923af65c22e8829ee5a8_46_1.png)

Some things should be noticed about this report.
