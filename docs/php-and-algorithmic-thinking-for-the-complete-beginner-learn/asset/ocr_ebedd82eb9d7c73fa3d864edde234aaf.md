# Chapter 21
Tips and Tricks with Decision Control Structures

+   c. do not produce the same results.
+   d. none of the above

# 3. The following two scripts

```
<?php
    $a = trim(fgets(STDIN));
    $b = trim(fgets(STDIN));

    $y = 5;

    if ($a > 15 || $b < 25)
        $y--;
    else
        $y++;

    echo $y;
?>
```

```
<?php
    $a = trim(fgets(STDIN));
    $b = trim(fgets(STDIN));

    $y = 5;

    if ($a > 15)
        $y--;
    elseif ($b < 25)
        $y--;
    else
        $y++;
    echo $y;
?>
```

+   a. produce the same result.
+   b. do not produce the same result.
+   c. neither of the above

# 4. The following two scripts

```
<?php
    $a = trim(fgets(STDIN));
    if ($a > 40) {
        echo $a * 2;
    }
    else {
        echo $a * 3;
    }
?>
```

```
<?php
    $a = trim(fgets(STDIN));
    if ($a > 40) {
        echo $a * 2;
    }
    if ($a <= 40) {
        echo $a * 3;
    }
?>
```

+   a. produce the same result(s), but the left script is faster.
+   b. produce the same result(s), but the right script is faster.
+   c. do not produce the same result(s).
+   d. none of the above

# 5. The following code fragment

```
if ($a == 5)
    echo "Hello Zeus!";
elseif ($b == 6)
```