# Solution

In this exercise the counted loop structure should increase the value of variable `counter`, starting from 0, until it reaches the given value. The PHP script is as follows.

```
```php
<?php
	echo "Enter an integer: ";
	$num = trim(fgets(STDIN));

	for ($i = 0; $i <= $num; $i++) {
		echo sqrt($i), "\n";
	}
?>
```
```

# 27.2  Rules that Apply to Counted Loop Structures

There are certain rules you should always follow when writing scripts with counted loop structures, since they can save you from undesirable side effects.

+   ➢ **Rule 1:** The *counter* variable can appear in a statement inside the loop but its value should never be altered. The same applies to *initial_value*, *final_value*, and *offset* in case they are variables and not constant values.
+   
+   ➢ **Rule 2:** The *offset* should never be zero. If it is set to zero, the loop performs an infinite number of iterations!
+   
+   ➢ **Rule 3:** If *initial_value* is smaller than *final_value* and the *offset* is negative, the loop performs zero iterations. Breaking this rule on purpose, however, can be useful in certain situations.
+   
+   ➢ **Rule 4:** If *initial_value* is greater than *final_value* and the *offset* is positive, the loop performs zero iterations. Breaking this rule on purpose, however, can be useful in certain situations.

# Exercise 27.2-1  *Counting the Total Number of Iterations*

How many iterations does the following code fragment perform?

```
```php
for ($i = 5; $i <= 10; $i++) {
    echo $i;

    $i--;
}
```
```

# Solution

This script breaks the first rule of counted loop structures, which states, *The counter variable can appear in a statement inside the loop but its value should never be altered.* The corresponding flowchart fragment that follows can help you better understand what really goes on.