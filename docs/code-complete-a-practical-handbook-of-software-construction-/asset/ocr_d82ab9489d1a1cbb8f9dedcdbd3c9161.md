+   - If tests are automated, they can be run frequently to see whether any code check-ins have broken the code. Test automation is part of the foundation of test-intensive practices, such as the daily build and smoke test and Extreme Programming.
+   - Automated tests improve your chances of detecting any given problem at the earliest possible moment, which tends to minimize the work needed to diagnose and correct the problem.
+   - Automated tests provide a safety net for large-scale code changes because they increase your chance of quickly detecting defects inserted during the modifications.
+   - Automated tests are especially useful in new, volatile technology environments because they flush out changes in the environments sooner rather than later.

The main tools used to support automated testing provide test scaffolding, generate input, capture output, and compare actual output with expected output. The variety of tools discussed in the preceding section will perform some or all of these functions.

> **Cross-Reference** For more on the relationship between technology maturity and development practices, see Section 4.3, “Your Location on the Technology Wave.”

# 22.7 Keeping Test Records

![](bbox=[0.166, 0.431, 0.243, 0.494])

Aside from making the testing process repeatable, you need to measure the project so that you can tell for sure whether changes improve or degrade it. Here are a few kinds of data you can collect to measure your project:

+   - Administrative description of the defect (the date reported, the person who reported it, a title or description, the build number, the date fixed)
+   - Full description of the problem
+   - Steps to take to repeat the problem
+   - Suggested workaround for the problem
+   - Related defects
+   - Severity of the problem—for example, fatal, bothersome, or cosmetic
+   - Origin of the defect: requirements, design, coding, or testing
+   - Subclassification of a coding defect: off-by-one, bad assignment, bad array index, bad routine call, and so on
+   - Classes and routines changed by the fix
+   - Number of lines of code affected by the defect
+   - Hours to find the defect
+   - Hours to fix the defect

Once you collect the data, you can crunch a few numbers to determine whether your project is getting sicker or healthier: