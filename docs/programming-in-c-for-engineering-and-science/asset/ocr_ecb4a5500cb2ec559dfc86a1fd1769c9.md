# CHAPTER SUMMARY

# Key Terms

+   - block
+   - break statement
+   - condition
+   - conditional expression
+   - dangling else problem
+   - drop-through behavior

+   - dual-branch if or if-else form
+   - multialternative selection
+   - multibranch if or if-else-if form
+   - single-branch or simple if form
+   - switch statement
+   - ternary operation

# NOTES

+   - The multibranch if is a series of nested if statements written as one.
+   - In a nested if, each else is matched with the nearest preceding unmatched if.
+   - Be sure to use the == operator for equality comparisons, and not = (assignment). Any time an algorithm calls for an equality comparison, the code that implements the algorithm should be carefully checked to ensure that = (assignment) has not been inadvertently used instead of the == (equality operator).
+   - Remember that the type of the expression of a switch statement and the constants in its case lists must be integer-compatible. Note that they may not be real or string expressions.
+   - To prevent drop-through behavior in a switch statement, remember to end the statement list in each case with a break or return statement (except for the final statement list, where it is not needed).
+   - In deciding which statement to use to implement a selection, use a switch if all of the following hold and an if otherwise:
+     1. An equality (==) comparison is being performed.
+     2. The same expression is being compared in each condition.
+     3. The expression being compared is integer-compatible.
+   - Conditional expressions can be used in place of many if-else statements and sometimes provide a simpler alternative.

# Style and Design Tips

In this text, we use the following conventions for formatting the selection statements considered in this chapter.