# 36.1　Introduction

In this chapter you will learn nothing new about flowcharts. Earlier, you learned that an array is actually just a special type of variable, in that an array can hold multiple values at the same time. In flowcharts, you can use arrays in the same way that you use variables.

# 36.2　Converting PHP Scripts to Flowcharts

Since there is nothing new to discuss, let’s directly proceed to solve some exercises!

# Exercise 36.2-1　 *Designing the Flowchart*

*Design the flowchart that corresponds to the following PHP script.*

```
```php
<?php
define("ELEMENTS", 100);

$values = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $values[$i] = trim(fgets(STDIN));
}

for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    if ($values[$i] < 0) {
        echo $values[$i];
    }
}
?>
```
```

# *Solution*

In this PHP script, there are two counted loop structures, the second of which nests a single-alternative decision structure. The corresponding flowchart is presented next.

![](bbox=[0.194, 0.724, 0.414, 0.939])