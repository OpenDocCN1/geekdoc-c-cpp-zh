
# Entering Responses and Factors

The steps for entering factors in a response surface design are unique to this design. To add factors, follow the step in Figure 13.6.

Figure 13.6 Entering Factors into a Response Surface Design

![](img/a858f3b35ed4923af65c22e8829ee5a8_219_0.png)

Click Continue to proceed to the next step.

# Choosing a Design

Highlight the type of response surface design you would like to use and click Continue.

Figure 13.7 Choose a Design Type

![](img/a858f3b35ed4923af65c22e8829ee5a8_219_1.png)

The Response Surface designer provides the following types of designs:

# Box-Behnken Designs

The Box-Behnken design has only three levels per factor and has no points at the vertices of the cube defined by the ranges of the factors. This is sometimes useful when it is desirable to avoid extreme points due to engineering considerations. The price of this characteristic is the higher uncertainty of prediction near the vertices compared to the central composite design.

# Central Composite Designs

The response surface design list contains two types of central composite designs: *uniform precision* and *orthogonal*. These properties of central composite designs relate to the number of center points in the design and to the axial values:

- Uniform precision means that the number of center points is chosen so that the prediction variance at the center is approximately the same as at the design vertices.
- For orthogonal designs, the number of center points is chosen so that the second order parameter estimates are minimally correlated with the other parameter estimates.

# Specifying Axial Value (Central Composite Designs Only)

When you select a central composite (CCD-Uniform Precision) design and then click **Continue**, you see the panel in Figure 13.8. It supplies default axial scaling information. Entering 1.0 in the text box instructs JMP to place the axial value on the face of the cube defined by the factors, which controls how far out the axial points are. You have the flexibility to enter the values you want to use.

![](img/a858f3b35ed4923af65c22e8829ee5a8_220_0.png)

**Figure 13.8** Display and Modify the Central Composite Design

- **Rotatable** makes the variance of prediction depend only on the scaled distance from the center of the design. This causes the axial points to be more extreme than the range of the factor. If this factor range cannot be practically achieved, it is recommended that you choose On Face or specify your own value.
- **Orthogonal** makes the effects orthogonal in the analysis. This causes the axial points to be more extreme than the −1 or 1 representing the range of the factor. If this factor range cannot be practically achieved, it is recommended that you choose On Face or specify your own value.
- **On Face** leaves the axial points at the end of the −1 and 1 ranges.
- **User Specified** uses the value entered by the user, which can be any value greater than zero. Enter that value into the Axial Value text box.

If you would like to inscribe the design, click the box beside **Inscribe**. When checked, JMP re-scales the whole design so that the axial points are at the low and high ends of the range (the axials are −1 and 1 and the factorials are shrunken based on that scaling).

# Specifying Output Options

Use the Output Options panel to specify how you want the output data table to appear. When the options are correctly set up, click Make Table.

Figure 13.9 Select the Output Options

![](img/a858f3b35ed4923af65c22e8829ee5a8_221_0.png)

- Run Order—Lets you designate the order you want the runs to appear in the data table when it is created. Choices are:
  - Keep the Same—the rows (runs) in the output table will appear as they do in the Design panel.
  - Sort Left to Right—the rows (runs) in the output table will appear sorted from left to right.
  - Randomize—the rows (runs) in the output table will appear in a random order.
  - Sort Right to Left—the rows (runs) in the output table will appear sorted from right to left.
  - Randomize within Blocks—the rows (runs) in the output table will appear in random order within the blocks you set up.
- Number of Center Points—Specifies additional runs placed at the center points.
- Number of Replicates—Specify the number of times to replicate the entire design, including centerpoints. Type the number of times you want to replicate the design in the associated text box. One replicate doubles the number of runs.

# Viewing the Design Table

Now you have a data table that outlines your experiment, as described in Figure 13.10.

# Figure 13.10  The Design Data Table

![](img/a858f3b35ed4923af65c22e8829ee5a8_222_0.png)

The name of the table is the design type that generated it.

This script allows you to easily fit a model using the values in the design table.

There are two center points per replicate.

The column called Pattern identifies the coding of the factors. It shows all the codings with “+” for high, “−” for low factor, “a” and “A” for low and high axial values, and “0” for midrange. Pattern is suitable to use as a label variable in plots because when you hover over a point in a plot of the factors, the pattern value shows the factor coding of the point.

Runs are in a random order.

The Y column is for recording experimental results.

# Continuing the Analysis, If Needed

After creating and viewing the design table, running the experiment, and recording your results in the design table’s Y column, run a fit model analysis on the data. The data table contains a script labeled **Model**. Right-click it and select **Run Script** (Figure 13.11) to fit the model.

# Figure 13.11  Running the Script

![](img/a858f3b35ed4923af65c22e8829ee5a8_222_1.png)

After clicking **Run Model** in the dialog, (Figure 13.12), review the analysis.

# Figure 13.12 Fitting the Model

![](img/a858f3b35ed4923af65c22e8829ee5a8_223_0.png)

- **Error Standard Deviation** Error Standard Deviation is the unexplained random variation around the means.
- **Sample Size** Sample size is how many experimental units (runs, or samples) are involved in the experiment.
- **Power** Power is the probability of declaring a significant result.
- **Effect Size** Effect size is how different the means are from each other or from the hypothesized value.

The Sample Size and Power command in JMP helps estimate in advance either the sample size needed, power expected, or the effect size expected in the experimental situation where there is a single mean comparison, a two sample comparison, or when comparing k sample means.

When you select DOE > Sample Size and Power, the panel shown in Figure 14.1 appears with button selections for experimental situations. The following sections describe each of these selections and explains how to enter estimated parameter values and the desired computation.

# Figure 14.1 Sample Size and Power Choices

![](img/a858f3b35ed4923af65c22e8829ee5a8_226_0.png)

# One-Sample and Two-Sample Means

After you click either One Sample Mean, or Two Sample Means in the initial Sample Size selection list (Figure 14.1), the Power and Sample Size dialog in Figure 14.2 appears and asks for the anticipated experimental values. The values you enter depend on your initial choice. As an example, consider the two-sample situation.

# Figure 14.2 Initial Power and Sample Size Dialogs for Single Mean (left) and Two Means (right)

![](img/a858f3b35ed4923af65c22e8829ee5a8_227_0.png)

The Two Sample Means choice in the initial Power and Sample Size dialog always requires values for Alpha and the error standard deviation (Error Std Dev), as shown here, and one or two of the other three values: Difference to detect, Sample Size, and Power. The power and sample size platform then calculates the missing item. If there are two unspecified fields, the power and sample size platform constructs a plot that shows the relationship between those two values:

- power as a function of sample size, given specific effect size
- power as a function of effect size, given a sample size
- effect size as a function of sample size, for a given power.

The Power and Sample Size dialog asks for the values depending the first choice of design:

- Alpha Alpha is the significance level, usually 0.05. This implies willingness to accept (if the true difference between groups is zero) that 5% (alpha) of the time a significant difference will be incorrectly declared.
- Error Std Deviation Error Std (Standard) Deviation is the true residual error. Even though the true error is not known, the power calculations are an exercise in probability that calculates what might happen if the true values were as specified.
- Extra Params Extra Params (Parameters) is only for multi-factor designs. Leave this field zero in simple cases. In a multi-factor balanced design, in addition to fitting the means described in the situation, there are other factors with the extra parameters that can be specified here. For example, in a three-factor two-level design with all three two-factor interactions, the number of extra parameters is five—two parameters for the extra main effects, and three parameters for the interactions. In practice, it isn’t very important what values you enter here unless the experiment is in a range where there is very few degrees of freedom for error.
- Difference to Detect Difference to detect is the smallest detectable difference (how small a difference you want to be able to declare statistically significant). For single sample problems this is the difference between the hypothesized value and the true value.
- Sample Size Sample size is the total number of observations (runs, experimental units, or samples). Sample size is not the number per group, but the total over all groups. Computed sample size numbers can have fractional values, which you need to adjust to real units. This is usually done by
