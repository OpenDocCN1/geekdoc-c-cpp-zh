# Sigma Quality Level

Use the Sigma Quality Level feature, accessed by selecting DOE > Sample Size and Power, by entering any two of the following three quantities:

+   - number of defects
+   - number of opportunities
+   - Sigma quality level

When you click Continue, the sigma quality calculator computes the missing quantity using the formula Sigma Quality Level = NormalQuantile(1 - defects/opportunities) + 1.5.

As an example, use the Sample Size and Power feature to compute the Sigma quality level for 50 defects in 1,000,000 opportunities:

+   1. Select DOE > Sample Size and Power.
+   2. Click the Sigma Quality Level button.
+   3. Enter 50 for the number of defects and 1,000,000 as the number of opportunities, as shown in the window to the left in Figure 14.13.
+   4. Click Continue. The results, as shown in the window on the right in Figure 14.13, are a Sigma quality level of 5.3.

Figure 14.13 Sigma Quality Level Example 1

![](bbox=[0.25, 0.47, 0.75, 0.66])

If you want to know how many defects reduce the Sigma Quality Level to “six-sigma” for 1,000,000 opportunities, enter 6 as the Sigma Quality Level and leave the Number of Defects blank (window to the left in Figure 14.14). The computation (window to the right in Figure 14.14) shows that the Number of Defects cannot be more than approximately 3.4.