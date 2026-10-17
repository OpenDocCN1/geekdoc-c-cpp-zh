# Exercise 21.6-1  “Merging” the Decision Control Structures

In the following PHP script, “merge” as many single-alternative decision structures as possible.

```
```php
<?php

$a = trim(fgets(STDIN));

$y = 0;

if ($a > 0) {
    $y++;
}

$b = trim(fgets(STDIN));       //This statement is not affected by the
                               //previous decision control structure
                               //and does affect the next one.
                               //Thus, it can be moved to the beginning
                               //of the script

if (!($a > 0)) {
    echo "Hello Zeus";
}

if ($y > 0) {                  //Unfortunately this decision control
    echo $y + 5;               //structure can't be merged with
}                              //the next one...

$y++;                          // because of this statement

if ($y <= 0) {
    echo $y + 12;
}
?>
```
```

# Solution

The first decision control structure evaluates variable $a to test if it is greater than zero, and just right after that the second decision control structure evaluates variable