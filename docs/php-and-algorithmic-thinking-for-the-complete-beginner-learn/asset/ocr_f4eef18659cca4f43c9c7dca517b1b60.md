# 3. In the following code fragment,

```
```php
if ($x == 3)
    $x = 5;
    $y++;
```
```

the statement `$y++` is executed

+   a. only when variable `$x` contains a value of 3.  
+   b. only when variable `$x` contains a value of 5.  
+   c. only when variable `$x` contains a value other than 3.  
+   d. either way.

# 4. In the following code fragment,

```
```php
if ($x % 2 == 0) $y++;
```
```

the statement `$y++` is executed when

+   a. variable `$x` is exactly divisible by 2.  
+   b. variable `$x` contains an even number.  
+   c. variable `$x` does not contain an odd number.  
+   d. all of the above  
+   e. none of the above

# 5. In the following code fragment,

```
```php
$x = 3 * $y;
if ($x > $y) $y++;
```
```

the statement `$y++` is

+   a. always executed.  
+   b. never executed.  
+   c. executed either way.  
+   d. executed only when variable `$y` contains positive values.  
+   e. none of the above

# 16.4 Review Exercises

Complete the following exercises.

# 1. Identify the syntax errors in the following PHP script:

```
```php
<?php

$x = trim(fgets(STDIN));

$y <− 5;
if ($x * $y / 2 > 20)
    $y--
    $x == 4 * $x2;
}
```
```