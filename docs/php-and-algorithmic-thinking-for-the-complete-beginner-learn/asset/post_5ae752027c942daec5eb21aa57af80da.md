

To optimize the code, you need to decrease the total number of multiplication, addition, and subtraction operations that the previous script had. For example, the statement

```
$t = 500 * 0.10 + ($kwh - 500) * 0.25;
```

can also be written as

```
$t = 50 + ($kwh - 500) * 0.25;
```

or even better as

```
$t = 0.25 * $kwh - 75;
```

Similarly, the statement

```
$t = 500 * 0.10 + 1500 * 0.25 + ($kwh - 2000) * 0.40;
```

can also be written as

```
$t = 50 + 375 + ($kwh - 2000) * 0.40;
```

or even better as

```
$t = 425 + ($kwh - 2000) * 0.40;
```

and finally as

```
$t = 0.4 * $kwh - 375;
```

Now that everything about the inner code fragment has been clarified, data validation can be achieved by following the “from inner to outer” method. The outer PHP script given in general form that validates data input is

```
<?php
    echo "Enter number of Kilowatt-hours consumed: ";
    $kwh = trim(fgets(STDIN));

    if (is_numeric($kwh) != true) {
        echo "Entered value contains non-numeric characters";
    }
    elseif ($kwh < 0) {
        echo "Entered value is negative";
    }
    else {
        //Here goes the code that calculates
        //and displays the total amount to pay
    }
?>
```

Combining this script with the last script from the previous exercise and applying code optimization, the PHP script becomes

```
file_23_4-6.php

<?php
echo "Enter number of Kilowatt-hours consumed: ";
$kwh = trim(fgets(STDIN));

if (is_numeric($kwh) != true) {
    echo "Entered value contains non-numeric characters";
}
elseif ($kwh < 0) {
    echo "Entered value is negative";
}
else {
    if ($kwh <= 500) {
        $t = $kwh * 0.10;
    }
    elseif ($kwh <= 2000) {
        $t = 0.25 * $kwh - 75;
    }
    elseif ($kwh <= 4000) {
        $t = 0.4 * $kwh - 375;
    }
    else {
        $t = 0.6 * $kwh - 1175;
    }

    $t = 1.10 * $t;
    //This is equivalent to
    //$t = $t + $t * 10 / 100
    //but more efficient
    echo "Total amount to pay (taxes included): ", $t;
}
?>
```

> **Notice:** It becomes clear now that, even though this script is more efficient than the one of the previous exercise, it is very difficult to read. No one who reads this script can understand that `$t = 0.6 * $kWh - 1175` is actually `$t = 500 * 0.10 + 1500 * 0.25 + 2000 * 0.4 + ($kWh - 4000) * 0.60`. Many times, when efficiency is not important, programmers do sacrifice efficiency for readability. This script is shown to demonstrate how a script can be made more efficient. But you don’t have to follow this kind of writing, at least not for now anyway. After all, today’s computers are so fast that you don’t have to worry about efficiency. Until the time at which you become the next Mark Zuckerberg of Facebook or the next Bill Gates of Microsoft, please write readable scripts! This book as well, since it addresses novice programmers, mostly prefers readability to efficiency.

# Exercise 23.4-7 *Progressive Rates and Text Messaging Services*

The LAV Cell Phone Company charges customers a basic rate of $8 per month to send text messages. Additional rates are charged based on the total number of text messages sent, as shown in the following table.

| Number of Text Messages Sent | Additional Rates (in USD per text message) |
|---|---|
| Up to 50 | Free of charge |
| 51 – 150 | $0.05 |
| 151 and above | $0.10 |

Federal, state, and local taxes add a total of 10% to each bill.
Write a PHP script that prompts the user to enter the number of text messages sent and then calculates and displays the total amount to pay.
Please note that the rates are progressive.

# Solution

The PHP script is presented here.

```
<?php

echo "Enter number of text messages sent: ";
$count = trim(fgets(STDIN));

if ($count <= 50) {
    $extra = 0;
}
elseif ($count <= 150) {
    $extra = ($count - 50) * 0.05;
}
else {
    $extra = 100 * 0.05 + ($count - 150) * 0.10;
}

$total_without_tax = 8 + $extra;
$tax = $total_without_tax * 10 / 100;
$total = $total_without_tax + $tax;
echo "Total amount to pay: ", $total;
?>
```

# 23.5 Exercises of a General Nature with Decision Control Structures

# Exercise 23.5-1 *Finding a Leap Year*

Write a PHP script that prompts the user to enter a year and then displays a message indicating whether or not it is a leap year. Moreover, if the user enters non-numeric characters, an error message should be displayed.

(Note that this involves data validation!)

# Solution

A year is a leap year when at least one of the following conditions is met:

+   1. **1st Condition:** The year is exactly divisible by 4, and not by 100.
+   2. **2nd Condition:** The year is exactly divisible by 400.

In the following table, some years are not leap years because none of the conditions evaluates to true.

| Year | Conditions | Leap Year |
|---|---|---|
| **1600** | 1st Condition: False, because it is exactly divisible by 4, and also by 100<br>2nd Condition: **True**, because it is exactly divisible by 400 | Yes |
| **1900** | 1st Condition: False, because it is exactly divisible by 4, and also by 100<br>2nd Condition: False, because it is not exactly divisible by 400 | No |
| **1918** | 1st Condition: False, because it is not exactly divisible by 4<br>2nd Condition: False, because it is not exactly divisible by 400 | No |
| **2000** | 1st Condition: False, because it is exactly divisible by 4, and also by 100<br>2nd Condition: **True**, because it is exactly divisible by 400 | Yes |
| **2002** | 1st Condition: False, because it is not exactly divisible by 4<br>2nd Condition: False, because it is not exactly divisible by 400 | No |
| **2004** | 1st Condition: **True**, because it is exactly divisible by 4, and not by 100<br>2nd Condition: False, because it is not exactly divisible by 400 | Yes |
| **2016** | 1st Condition: **True**, because it is exactly divisible by 4, and not by 100<br>2nd Condition: False, because it is not exactly divisible by 400 | Yes |

The PHP script is shown here.

```
<?php
	echo "Enter a year: ";
	$y = trim(fgets(STDIN));

	if (is_numeric($y) == true) {
		if ($y % 4 == 0 && $y % 100 != 0 || $y % 400 == 0) {
			echo "Leap year!";
		}
		else {
			echo "Not a leap year";
		}
	}
	else {
		echo "Invalid Number";
	}
?>
```

> **Remember!** The AND (`&&`) operator has a higher precedence than the OR (`||`) operator.

# Exercise 23.5-2 **Displaying the Days of the Month**

Write a PHP script that prompts the user to enter a month and a year and then displays how many days are in that month. The script needs to take into consideration the leap years. In case of a leap year, February has 29 instead of 28 days.

# Solution

The PHP script is shown here.

```
<?php
	echo "Enter month 1 - 12: ";
	$m = trim(fgets(STDIN));
	echo "Enter year: ";
	$y = trim(fgets(STDIN));

	if ($m == 2) {
		if ($y % 4 == 0 && $y % 100 != 0 || $y % 400 == 0) {
			echo "This month has 29 days";
		}
```

# Exercise 23.5-3 **Is the Number a Palindrome?**

> **Notice:** Please note the way cases 4, 6, and 9 are written. Since there isn’t any break statement in any of those cases, they all reach case 11.

A palindrome is a number that remains the same after reversing its digits. For example, the number 13631 is a palindrome. Write a PHP script that lets the user enter a five-digit integer and tests whether or not this number is a palindrome. Moreover, individual error messages should be displayed when the user enters any non-numeric characters or any integer with either less than or more than five digits.

(Note that this involves data validation.)

# Solution

To test if the user enters a palindrome number, you need to split its digits into five different variables as you learned in Chapter 13. Then, you can check whether the 1st digit is equal to the 5th digit and the 2nd digit is equal to the 4th digit. If this evaluates to true, the number is a palindrome.

To validate data input, you need to check whether the user has entered a five-digit number. Keep in mind that all five-digit numbers are in the range of 10000 to 99999. Therefore, you can just restrict the data input to within this range.

In order to display many different error messages, the best practice is to use a multiple-alternative decision structure which first checks data input validity for all cases, and then tries to solve the required problem. For example, if you need to check for various errors, you can do something like the following.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_355_0.png)

