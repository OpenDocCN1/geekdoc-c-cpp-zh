# 7.3 Which of the following are permitted and which are disallowed? Here A and B are the names of two subprograms. They could be either procedures or functions or one of each.

+   - a. A’s body is in SPARK and calls B, which has a SPARK declaration and a SPARK body.
+   - b. A’s body is in SPARK and calls B, which has a SPARK declaration and a non-SPARK body.
+   - c. A’s body is in SPARK and calls B, which has a non-SPARK declaration and a non-SPARK body.
+   - d. A’s body is not in SPARK and calls B, which as a SPARK declaration and a SPARK body.
+   - e. A’s body is not in SPARK and calls B, which has a SPARK declaration and a non-SPARK body.
+   - f. A’s body is not in SPARK and calls B, which has a non-SPARK declaration and a non-SPARK body.

7.4 It is not permitted for a subprogram to have a non-SPARK declaration and a SPARK body. Why would this be disallowed?

7.5 Add a function Check_Overlap to package Interval_Tree described in Section 7.1.1 with the following profile:

```
function Check_Overlap(Item : in Interval ) return Boolean;
```

The function should return True if the given interval overlaps with at least one interval in the tree, otherwise it should return False. Your function should run in O(log n) time and have appropriate SPARK aspects.

7.6 Suppose you write a package with a non-SPARK body and a SPARK specification. Which of the following aspects that may appear on the subprogram declarations in the specification would actually be checked and when would that checking occur?

+   - a. Global
+   - b. Depends
+   - c. Pre
+   - d. Post

7.7 The wrapper package presented on page 266 shows imported declarations in the body of the wrapper package. Is it necessary for those declarations to be in the body or could they continue to be in a package specification of their own? If they could be in their own specification, modify the wrapper package presented to show how it would look. If they must appear in the body, explain why.