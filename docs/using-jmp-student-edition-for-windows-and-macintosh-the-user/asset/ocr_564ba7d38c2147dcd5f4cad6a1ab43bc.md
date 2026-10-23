σ = √[ Σ (from i=1 to n) (x_i - x̄)² / (n - 1) ]

+   - **Specified Sigma** allows the user to enter a specific, known sigma used for computing capability analyses. Sigma is, obviously, user-specified and is therefore not computed. This is the option used for control chart-generated capability analyses, where the sigma used in the chart is entered (in the dialog) as the specified sigma.

+   - **Short Term, Grouped by fixed subgroup size** computes σ using the following formula. In this case, if r is the number of subgroups and each i-th subgroup is defined by the order of the data, sigma is computed as
+   
+   σ = √[ Σ (i=1 to n) (x_ij - x̄_i.)² / (n - r - 1) ]

+   - **Short Term, Grouped by Column** brings up a column list dialog from which you choose the grouping column. In this case, with r equal to the number of subgroups, sigma is computed as
+   
+   σ = √[ Σ (i=1 to n) (x_ij - x̄_i.)² / (n - r - 1) ]

(Note that this is the same formula for Short Term, Grouped by fixed subgroup size and is commonly referred to as the Root Mean Square Error or RMSE.)

**Note:** There is a preference for Distribution called **Ppk Capability Labeling** that will label the long-term capability output with Ppk labels. This option is found using **File > Preferences**.

When you click **OK**, the platform appends a Capability Analysis table, like the one in Figure 2.22, at the bottom of the text reports. You can remove and redo a Capability Analysis as many times as you want.

The specification limits can be stored and automatically retrieved as a column property. To do this, choose **Spec Limits** from the **Save** command menu. When you save the specification limits, they appear on the histogram when opened at a later time.