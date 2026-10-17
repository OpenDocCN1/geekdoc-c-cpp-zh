2. Create a trace table to determine the values of the variables in each step of the PHP script for two different executions.

The input values for the two executions are: (i) 3, 4; and (ii) 4, 4

```
<?php
    $a = trim(fgets(STDIN));
    $b = trim(fgets(STDIN));

    $c = $a + $b;
    $d = 1 + $a / $b * $c + 2;
    $e = $c + $d;
    $c += $d + $e;
    $e--;
    $d -= $c + $d % $c;
    echo $c, " ", $d, " ", $e;
?>
```