# 10.1　What is the Sequence Control Structure?

“Sequence control structure” refers to the line-by-line execution by which statements are executed sequentially, in the same order in which they appear in the script. They might, for example, carry out a series of read or write operations, arithmetic operations, or assignments to variables.

The sequence control structure is the simplest of the three fundamental control structures that you learned about in Chapter 4. The following script shows an example of PHP statements that are executed sequentially.

```
```php
<?php
	echo "Enter a number: ";
	$a = trim(fgets(STDIN));

	$b = $a * $a;

	echo "The square of ", $a, " is ", $b;
?>
```
```

# Exercise 10.1-1　*Calculating the Area of a Parallelogram*

*Write a PHP script that calculates and displays the area of a parallelogram.*

# Solution

The area of a parallelogram can be calculated using the following formula:

*Area = Base × Height*

In this exercise, the user enters values for *Base* and *Height* and the script calculates and displays the area of the parallelogram. The solution to this problem is shown here.

```
```php
<?php
	echo "Enter the length of Base: ";
	$base = trim(fgets(STDIN));
	echo "Enter the length of Height: ";
	$height = trim(fgets(STDIN));

	$area = $base * $height;

	echo "The area of the parallelogram is ", $area;
?>
```
```