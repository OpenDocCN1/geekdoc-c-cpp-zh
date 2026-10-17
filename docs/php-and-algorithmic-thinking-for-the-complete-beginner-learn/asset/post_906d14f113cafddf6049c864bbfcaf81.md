
## Third Approach – Using nested loop control structures only

This approach is based on the previous one. The main difference between them is that in this case, variable `$digit1` always begins from a value greater than `$digit2`, and variable `$digit2` always begins from a value greater than `$digit3`. In that way, the first integer that will be displayed is 123.

> **Notice:** There are no integers below the value 123 and above the value 789 that can validate the Boolean expression `$digit3 < $digit2 && $digit2 < $digit1` to true.

The PHP script is as follows.

```php
<?php
    for ($digit3 = 1; $digit3 <= 7; $digit3++) {
        for ($digit2 = $digit3 + 1; $digit2 <= 8; $digit2++) {
            for ($digit1 = $digit2 + 1; $digit1 <= 9; $digit1++) {
                echo $digit3 * 100 + $digit2 * 10 + $digit1, "\n";
            }
        }
    }
?>
```

> **Notice:** This solution is the most efficient since it doesn’t use any decision control structure and, moreover, the number of iterations is kept to a minimum!
> 
> **Remember!** As you can see, one problem can have many solutions. It is up to you to find the optimal one!

## 31.3 Data Validation with Loop Control Structures

Data validation is the process of restricting data input, forcing the user to enter only valid values.

You have already encountered one method of data validation using decision control structures. Let’s recall a previous example.

```php
<?php
echo "Enter a number: ";
$x = trim(fgets(STDIN));

if (is_numeric($x) == true) {
    if ($x > 0) {
        echo $x, " is positive";
    }
}
else {
    echo "Invalid Number";
}
```

## Exercise 31.3-1 Finding the Square Root - Validation Without Error Messages

Write a PHP script that prompts the user to enter a numeric value and then calculates its square root. Moreover, the script should validate data input, allowing the user to enter only *non-negative*¹ numeric values. There is no need to display any error messages.

### Solution

First, let’s write the script without data validation.

```php
<?php
echo "Enter a number: ";
$x = trim(fgets(STDIN));

$y = sqrt($x);
echo $y;
?>
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_531_0.png)

To validate data input without displaying any error messages you can use the first approach. All you need to do is replace the statements marked with a dashed rectangle with the following code fragment.

```php
do {
    echo "Enter a non-negative number: ";
    $x = trim(fgets(STDIN));
} while (is_numeric($x) != true || $x < 0);
```

> ¹ A quantity that is either zero or positive.

## Exercise 31.3-2 Finding the Square Root - Validation with One Error Message

Write a PHP script that prompts the user to enter a numeric value and then calculates its square root. Moreover, the script should validate data input and display an error message when the user enters any non-numeric or negative values.

### Solution

In the previous exercise, the two statements marked with the dashed rectangle were replaced with a code fragment that validated data input without displaying any error message. The same method is followed here, except that the replacing PHP fragment is based on the second approach. The PHP script is as follows.

```php
<?php
echo "Enter a non-negative number: ";
$x = trim(fgets(STDIN));
while (is_numeric($x) != true || $x < 0) {
    echo "Error: Invalid number! \n";
    echo "Enter a non-negative number: ";
    $x = trim(fgets(STDIN));
}
$y = sqrt($x);
echo $y;
?>
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_532_0.png)

![](img/4d9a992abc5da7946ac44f9e6bf1d032_532_1.png)

## Exercise 31.3-3 Finding the Square Root - Validation with Individual Error Messages

Write a PHP script that prompts the user to enter a numeric value and then calculates its square root. Moreover, the script should validate data input and display individual error messages when the user enters any non-numeric or negative values.

### Solution

To validate data input and display individual error messages for each error, you can use the third approach. The PHP script is as follows.

```php
<?php
do {
    echo "Enter a non-negative number: ";
    $x = trim(fgets(STDIN));

    $failure = false;
    if (is_numeric($x) != true) {
        echo "Please enter numeric values! \n";
        $failure = true;
    }
    elseif ($x < 0) {
        echo "Please enter non-negative numbers! \n";
        $failure = true;
    }
} while ($failure == true);

$y = sqrt($x);
echo $y;
?>
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_533_0.png)

## Exercise 31.3-4 Finding the Sum of 10 Numbers

Write a PHP script that prompts the user to enter 10 numbers and then calculates and displays their sum. Moreover, the script should validate data input and display an error message when the user enters any non-numeric or negative values.

### Solution

This exercise was already discussed in Chapter 27. The only difference here is that this script should validate data input and display an error message when the user enters invalid values. For your convenience, the solution proposed in Chapter 27 is reproduced next.

```php
<?php
$sum = 0;
for ($i = 1; $i <= 10; $i++) {
    echo "Enter a number: ";
    $a = trim(fgets(STDIN));
    $sum = $sum + $a;
}
echo $sum;
?>
```

Now, replace the statements marked with a dashed rectangle with the following code fragment

```php
echo "Enter a number: ";
$a = trim(fgets(STDIN));
while (is_numeric($a) != true ) {
    echo "Please enter numeric values! \n";
    echo "Enter a number: ";
    $a = trim(fgets(STDIN));
}
```

and the final PHP script becomes

```php
<?php
$sum = 0;
for ($i = 1; $i <= 10; $i++) {
    echo "Enter a number: ";
    $a = trim(fgets(STDIN));
    while (is_numeric($a) != true ) {
        echo "Please enter numeric values! \n";
        echo "Enter a number: ";
        $a = trim(fgets(STDIN));
    }
    $sum = $sum + $a;
}
echo $sum;
?>
```

**Notice:** The basic purpose of this exercise was to show you how to nest the loop control structure that validates data input into other already existing loop control structures.

## 31.4 Using Loop Control Structures to Solve Mathematical Problems

### Exercise 31.4-1 Calculating the Area of as Many Triangles as the User Wishes

Write a PHP script that prompts the user to enter the lengths of all three sides A, B, and C of a triangle and then calculates and displays its area. You can use Heron’s formula,

$$\text{Area}=\sqrt{S(S-A)(S-B)(S-C)}$$

where S is the semi-perimeter

$$S=\frac{A+B+C}{2}$$

The script should iterate as many times as the user wishes. At the end of each area calculation, the script should ask the user if he or she wishes to calculate the area of another triangle. If the answer is “yes” the script should repeat; it should end otherwise. Make your script accept the answer in all possible forms such as “yes,” “YES,” “Yes,” or even “YeS”.

Moreover, the script should validate data input and display an error message when the user enters any non-positive value.

### Solution

According to the “Ultimate” rule, the post-test loop structure should be as follows, given in general form.

```php
$answer = "yes";   //Redundant initialization of $answer.
do {
    //Here goes the code that prompts the user to enter
    //the lengths of all three sides A, B, C of a triangle and
    //then calculates and displays its area

    echo "Would you like to repeat? ";
    $answer = trim(fgets(STDIN));     //Update/alteration of $answer
} while (strtoupper($answer) === "YES");
```

> **Remember!** The `strtoupper()` function ensures that the scripts operates properly for any given answer “Yes”, “yes”, “YES” or even “YeS” or “yES”!

The solution to this exercise, using a post-test loop structure, is as follows.

```php
file_31_4-1.php
<?php
do {
    echo "Enter side A: ";
    $a = trim(fgets(STDIN));
```
