# Exercise 29.5-1  *Cleaning Out the Loop*

The following code fragment calculates the average value of numbers 1, 2, 3, 4, ... 10000. Try to move as many statements as possible outside the loop to make the script more efficient.

```
```php
$s = 0;
for ($i = 1; $i <= 10000; $i++) {
    $s = $s + $i;
    $average = $s / 10000;
}
echo $average;
```
```

# *Solution*

One very common mistake that novice programmers make when calculating average values is to put the statement that calculates the average inside the loop. Think about it! Imagine that you want to calculate your average grade in school. Your first step would be to calculate the sum of the grades for all of the courses that you’re taking. Then, when all your grades have been summed up, you would divide that sum by the number of courses that you’re taking.

> **Notice:** Calculating an average is a two-step process.

Therefore, it is pointless to calculate the average value inside the loop. You can move this statement outside and right after the loop, and leave the loop just to sum up the numbers as follows.

```
```php
$s = 0;
for ($i = 1; $i <= 10000; $i++) {
    $s = $s + $i;
}
$average = $s / 10000;
echo $average;
```
```