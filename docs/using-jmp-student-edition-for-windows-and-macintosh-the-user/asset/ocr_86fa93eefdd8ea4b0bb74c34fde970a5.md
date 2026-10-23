# Counts per Unit

The Counts per Unit selection calculates sample size for the Poisson-distributed counts typical when you can measure more than one defect per unit. A unit can be an area and the counts can be fractions or large numbers.

Although the number of defects observed in an area of a given size is often assumed to have a Poisson distribution, the area and count are assumed to be large enough to support a normal approximation.

Questions of interest are:

+   - Is the defect density within prescribed limits?
+   - Is the defect density greater than or less than a prescribed limit?

Enter alpha and the baseline count per unit. Then enter two of the remaining fields to see the calculation of the third. The test is for one-sided (one-tailed) change. Enter the Difference to Detect in terms of the baseline count per unit (defects per unit). The computed sample size is expressed in those units.

As an example, consider a wafer manufacturing process with a target of 4 defects per wafer and you want to verify that a new process meets that target.

+   1. Select **DOE > Sample Size and Power**.
+   2. Click the **Counts per Unit** button.
+   3. Enter an alpha of 0.1 to be the chance of failing the test if the new process is as good as the target.
+   4. Enter a power of 0.9, which is the chance of detecting a change larger than 2 (6 defects per wafer). In this kind of situation, alpha is sometimes called the *producer’s risk* and beta is called the *consumer’s risk*.
+   5. Click **Continue** to see the computed sample size of 8.128 (Figure 14.12).

The process meets the target if there are less than 48 defects (6 defects per wafer in a sample of 8 wafers).

![](bbox=[0.373, 0.619, 0.702, 0.852])