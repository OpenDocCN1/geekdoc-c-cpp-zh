# Chapter 25
The Pre-Test Loop Structure

```
?>
```

Now let’s rewrite this script using a loop control structure instead. The final script is presented next. If you try to follow the flow of execution, you will find that it operates equivalently to the previous one.

```
<?php

    $sum = 0;

    $a = trim(fgets(STDIN));
    while ($a != -1) {
        $sum = $sum + $a;
        $a = trim(fgets(STDIN));
    }

    echo $sum;
?>
```

Now let’s create a trace table to determine if this script operates properly using 10, 20, 5, and -1 as input values.

| Step | Statement | Notes | $a | $sum |
|---:|---|---|---:|---:|
| 1 | `$sum = 0` |  | ? | 0 |
| 2 | `$a = trim(fgets(STDIN))` |  | 10 | 0 |
| 3 | `while ($a != -1)` | This evaluates to true |  |  |
| 4 | `$sum = $sum + $a` |  | 10 | 10 |
| 5 | `$a = trim(fgets(STDIN))` |  | 20 | 10 |
| 6 | `while ($a != -1)` | This evaluates to true |  |  |
| 7 | `$sum = $sum + $a` |  | 20 | 30 |
| 8 | `$a = trim(fgets(STDIN))` |  | 5 | 30 |
| 9 | `while ($a != -1)` | This evaluates to true |  |  |
| 10 | `$sum = $sum + $a` |  | 5 | 35 |
| 11 | `$a = trim(fgets(STDIN))` |  | -1 | 35 |
| 12 | `while ($a != -1)` | This evaluates to false |  |  |
| 13 | `echo $sum` | The value 35 is displayed |  |  |

As you can see, in the end, variable `$sum` contains the value 35, which is, indeed, the sum of the values 10 + 20 + 5. Moreover, the final given value of -1 does not participate in the final sum.