# Factor Extraction Criteria

+   - How Many Factors? .................................................... 33
+   - Extraction Criteria .................................................... 34
+   - Example Syntax and Output ........................................ 36
+   - How Do the Criteria Compare? ................................... 45
+   - Summary .................................................................... 57
+   - Exercises .................................................................... 58
+   - References ................................................................... 58

# How Many Factors?

Scholars have been arguing about this issue for the better part of a century. There are many who will argue passionately that one method is superior to another, and some methods do seem to be more defensible than others. However, it seems to me that much of the argument comes from a high-stakes mentality where researchers are attempting to confirm one factor structure as superior to another. Let us again repeat our mantra for this book: EFA is exploratory and should be considered a low-stakes process.

There are many guidelines for how to decide the number of factors to extract from an analysis. After all, your statistical software will extract as many factors as there are variables in the analysis, and since our goal is dimension reduction, we then have to decide how many of those extracted factors to retain for further analysis. If the number of factors to retain is not specified in SAS, then PROC FACTOR defaults to using the minimum number of factors that satisfies either the minimum eigenvalue criterion (with the default eigenvalue minimum varying by extraction method, see SAS, 2015) or the proportion of variance criterion (with the default proportion set to 100%). It is important that you do not let the default setting drive your analysis, but instead select and review the method or methods that make sense to you. So what decision rules exist, and which is best?