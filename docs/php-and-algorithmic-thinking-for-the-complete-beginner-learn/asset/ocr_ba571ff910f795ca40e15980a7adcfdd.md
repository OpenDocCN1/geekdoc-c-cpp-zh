c. the true path only.

2. In the following code fragment,

```
if ($x % 2 == 0) {
    $x = 0;
}
else {
    $y++;
}
```

the statement $y++ is executed when

+   a. variable $x is exactly divisible by 2.
+   b. variable $x contains an even number.
+   c. variable $x contains an odd number.
+   d. none of the above

3. In the following code fragment,

```
if ($x == 3)
    $x = 5;
else
    $x = 7;
    $y++;
```

the statement $y++ is executed

+   a. when variable $x contains a value of 3.
+   b. when variable $x contains a value other than 3.
+   c. both of the above

# 17.4 Review Exercises

Complete the following exercises.

+   1. Create a trace table to determine the values of the variables in each step of the next PHP script for two different executions. Then, design the corresponding flowchart.

The input values for the two executions are (i) 3, and (ii) 0.5.

```
<?php
$a = trim(fgets(STDIN));
$z = $a * 3 - 2;
if ($z >= 1) {
    $y = 6 * $a;
}
else {
    $z++;
    $y = 6 * $a + $z;
}
```