# Chapter 16
The Single-Alternative Decision Structure

+   3. It is a possible that none of the statements enclosed in a single-alternative decision structure will be executed.
+   
+   4. In a flowchart, the Decision symbol represents the beginning and the end of an algorithm.
+   
+   5. The code fragment
+   
+   ```php
+   define("if", 5);
+   $x = if + 5;
+   ```
+   
+   is syntactically correct.
+   
+   6. The single-alternative decision structure uses the reserved keyword `else`.
+   
+   7. The following code fragment satisfies the property of definiteness.
+   
+   ```php
+   if ($b != 3) {
+       $x = $a / ($b - 3);
+   }
+   ```
+   
+   8. The following PHP script satisfies the property of definiteness.
+   
+   ```php
+   <?php
+   $a = trim(fgets(STDIN));
+   $b = trim(fgets(STDIN));
+   
+   if ($b != 3) {
+       $x = $a / ($b - 3);
+   }
+   echo $x;
+   ?>
+   ```

# 16.3  Review Questions: Multiple Choice

Select the correct answer for each of the following statements.

+   1. The single-alternative decision structure is used when
+      a. statements are executed one after another.
+      b. a decision must be made before executing some statements.
+      c. none of the above
+      d. all of the above
+   
+   2. The single-alternative decision structure includes a statement or block of statements on
+      a. the false path only.
+      b. both paths.
+      c. the true path only.