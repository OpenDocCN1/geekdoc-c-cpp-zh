```
$y--;
}
}
else {
    $y++;
```

You can even nest case decision structures inside dual-alternative decision structures.

```
<?php
echo "Enter a number: ";
$x = trim(fgets(STDIN));

if ($x < 1 || $x > 3) {
    echo "Invalid Number";
}
else {
    switch ($x) {
        case 1:
            echo "1st choice selected";
            break;
        case 2:
            echo "2nd choice selected";
            break;
        case 3:
            echo "3rd choice selected";
            break;
    }
}
?>
```

This is a nested case decision structure

*Notice:* Please note that keyword default is missing from the switch statement.

In general, you can nest any control structure inside any other control structure as long as you keep them syntactically and logically correct. However, you should always try to keep your script as simple as possible because complex code may lead to invalid results.

# Exercise 20.1-1 Trace Tables and Nested Decision Control Structures

Create a trace table to determine the values of the variables in each step of the next PHP script for three different executions.
The input values for the three executions are (i) 13, (ii) 18, and (iii) 30.