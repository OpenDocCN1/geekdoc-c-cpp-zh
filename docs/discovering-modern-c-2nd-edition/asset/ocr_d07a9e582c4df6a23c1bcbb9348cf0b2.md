+   1. Create a temporary variable `sum` for the addition of `x` and `y` (line 5).
+   2. Perform a loop reading `x` and `y`, adding it element-wise, and writing the result to `sum` (lines 6+7).
+   3. Copy `sum` to a temporary variable, say, `t_xy`, in the return statement (line 8).
+   4. Delete `sum` with the destructor when it goes out of scope (line 9).
+   5. Create a temporary variable `sum` for the addition of `t_xy` and `z` (line 5).
+   6. Perform a loop reading `t_xy` and `z`, adding it element-wise, and writing the result to `sum` (lines 6+7).
+   7. Copy `sum` to a temporary variable, say, `t_xyz`, in the return statement (line 8).
+   8. Delete `sum` (line 9).
+   9. Delete `t_xy` (after second addition).
+   10. Perform a loop reading `t_xyz` and writing to `w` (in assignment).
+   11. Delete `t_xyz` (after assignment).

This is admittedly the worst-case scenario; however, it only happened with very old compilers. Modern compilers perform more optimizations by static code analysis and optimize return values (§2.3.5.3), thus avoiding the copies into temporaries `t_xy` and `t_xyz`. The optimized version still performs:

+   1. Create a temporary variable `sum` for the addition of `x` and `y` (for distinction we call it `sum_xy`) (line 5).
+   2. Perform a loop reading `x` and `y`, adding it element-wise, and writing the result to `sum` (lines 6+7).
+   3. Create a temporary variable `sum` (for distinction, `sum_xyz`) for the addition of `sum_xy` and `z` (line 5).
+   4. Perform a loop reading `sum_xy` and `z`, adding it, and writing the result to `sum_xyz` (lines 6+7).
+   5. Delete `sum_xy` (after second addition).