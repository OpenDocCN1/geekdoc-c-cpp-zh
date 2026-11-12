![](bbox=[0.1, 0.08, 0.9, 0.46])

If CGL does exceed 0.05, then the next decision node (Node 3) is on Marital Status. If married, then the tree branches to Node 7. If some other marital status, the tree branches to Node 4, which then tests CGLs again, this time whether it exceeds 0.289. Counterintuitively, the group with CGL > 0.289 has a lower proportion of high income in its Node 6, than in the lower CGL group in Node 5. Node 7 receives the married individuals with CGL > 0.05. It then splits on whether CGL > 0.202. If not, then the leaf node (Node 8) has almost all high income. If CGL > 0.202, one final split in Node 9 tests whether CGL > 0.423. If so, the 512 records are predominantly high income, otherwise not.

There are some interesting differences between the decision trees built by CART and C5.0. In contrast with the C5.0 tree which shunted over 90% of the records to a single node, the CART tree’s root node split (Figure 6.1) on marital status led to a rather balanced split, probably due to the nature of the Gini Index, which contains the $P_k P_c$ coefficient, favoring balanced branches.

# 6.3.1 How to Build C5.0 Decision Trees Using Python

Python packages do not directly implement C5.0. Instead, we will again use the sklearn package, this time changing the splitting criterion from Gini to entropy.

Before running the code in this section, run the code in the previous Python section, up to but excluding the paragraph that begins “Now we are ready to run the CART algorithm!” The code contained there will set up our variables and variable names in preparation for running this decision tree.