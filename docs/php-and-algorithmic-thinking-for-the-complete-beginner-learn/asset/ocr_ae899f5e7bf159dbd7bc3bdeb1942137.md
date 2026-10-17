# Second Approach – Using nested loop control structures and a decision control structure

The main idea is to use three counted loop structures, nested one within the other. In this case, there are three counter variables and each one of them corresponds to one digit of the three-digit integer. The PHP script is as follows.

```
```php
<?php
echo "Enter a digit 0 - 9: ";
$x = trim(fgets(STDIN));

for ($digit3 = 1; $digit3 <= 9; $digit3++) {
    for ($digit2 = 0; $digit2 <= 9; $digit2++) {
        for ($digit1 = 0; $digit1 <= 9; $digit1++) {
            if ($digit3 == $x || $digit2 == $x || $digit1 == $x) {
                echo $digit3 * 100 + $digit2 * 10 + $digit1, "\n";
            }
        }
    }
}
?>
```
```

If you follow the flow of execution, the value 100 is the first “integer” evaluated ($digit1 = 1, $digit2 = 0, $digit3 = 0). Then, the most-nested loop control structure increments variable $digit1 by one and the next value evaluated is “integer” 101. This continues until $digit1 reaches the value 9; that is, until the “integer” reaches the value 109. The flow of execution then exits the most-nested loop control structure, variable $digit2 increments by one, and the most-nested loop control structure starts over again, thus the values evaluated are the “integers” 110, 111, 112, ... 119. The process goes on until all integers up to the value 999 are evaluated.

> **Notice:** Please note that variable $digit3 starts from 1, whereas variables $digit2 and $digit1 start from 0. This is necessary since the scale for three-digit numbers begins from 100 and not from 000.

> **Notice:** Please note how the echo statement composes the three-digit integer.