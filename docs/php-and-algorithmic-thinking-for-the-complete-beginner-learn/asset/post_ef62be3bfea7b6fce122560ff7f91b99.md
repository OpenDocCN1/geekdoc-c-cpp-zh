

# 20.3 Review Questions: True/False

Choose **true** or **false** for each of the following statements.

1. Nesting of decision control structures describes a situation in which one or more than one paths of a decision control structure enclose other decision control structures.
2. Nesting level can go as deep as the programmer wishes.
3. When a problem can be solved using either a case decision structure or nested decision control structures, the second option is better because the script becomes more readable.
4. It is possible to nest a multiple-alternative decision structure within a case decision structure, but not the opposite.
5. When designing flowcharts with nested decision control structures, the decision control structure that opens last should be the first one to close.

# 20.4 Review Exercises

Complete the following exercises.

1. Create a trace table to determine the values of the variables in each step of the next PHP script for four different executions. The input values for the four executions are (i) 20, 1; (ii) 20, 3; (iii) 12, 8; and (iv) 50, 0.

```php
<?php
$x = trim(fgets(STDIN));
$y = trim(fgets(STDIN));

if ($x < 30) {
    switch ($y) {
        case 1:
            $x = $x % 3;
            $y = 0;
            break;
        case 2:
            $x = $x * 2;
            $y = 2;
            break;
        case 3:
            $x = $x + 5;
            $y += 3;
            break;
        default:
            $x -= 2;
            $y++;
    }
} else {
    $y++;
}

echo $x, $y;
?>
```

2. Create a trace table to determine the values of the variables in each step of the next PHP script for four different executions.

The input values for the four executions are (i) 60, 25; (ii) 50, 8; (iii) 20, 15; and (iv) 10, 30.

```php
<?php
$x = trim(fgets(STDIN));
$y = trim(fgets(STDIN));

if (($x + $y) / 2 <= 20) {
    if ($y < 10) {
        $x = $x % 3;
        $y += 2;
    }
elseif ($y < 20) {
    $x = $x * 5;
    $y += 2;
}
else {
    $x = $x - 2;
    $y += 3;
}
}
else {
    if ($y < 15) {
        $x = $x % 4;
        $y = 2;
    }
    elseif ($y < 23) {
        $x = $x % 2;
        $y -= 2;
    }
    else {
        $x = 2 * $x + 5;
        $y += 1;
    }
}

echo $x, $y;
?>
```

3. Write a PHP script that prompts the user to enter the lengths of three sides of a triangle, and then determines whether or not the given numbers can be lengths of the three sides of a triangle. If the lengths are not valid, a corresponding message should be displayed; otherwise the script should further determine whether the triangle is

   a. equilateral
      Hint: In an equilateral triangle, all sides are equal.
   b. right (or right-angled)
      Hint: Use the Pythagorean theorem.
   c. not special
      Hint: In any triangle, the length of each side is less than the sum of the lengths of the other two sides.

# Chapter 20

# Nested Decision Control Structures

4. Inside an automated teller machine (ATM) there are notes of $10, $5, and $1. Write a PHP script to emulate the way this ATM works. At the beginning, the machine prompts the user to enter the four-digit PIN and then checks for PIN validity (assume “1234” as the valid PIN). If given PIN is correct, the script should prompt the user to enter the amount of money (an integer value) that he or she wants to withdraw and finally it displays the least number of notes the ATM should dispense. For example, if the user enters an amount of $36, the script should display “3 notes of $10, 1 note of $5, and 1 note of $1”. Moreover, if the user enters a wrong PIN, the machine will allow him or her two retries. If the user enters an incorrect PIN all three times, the message “PIN locked” should be displayed and the script should end.

5. Write a PHP script that prompts the user to enter two values, one for temperature and one for wind speed. If the temperature is above 75 degrees Fahrenheit, the day is considered hot, otherwise it is cold. If the wind speed is above 12 miles per hour, the day is considered windy, otherwise it is not windy. The script should display one single message, depending on values given. For example, if a user enters 60 for temperature and 10 for wind speed, the script should display “The day is cold and not windy”.

# Chapter 21
Tips and Tricks with Decision Control Structures

# ### 21.1 Introduction

This chapter is dedicated to teaching you some useful tips and tricks that can help you write “better” code. You should always keep them in mind when you design your own algorithms, or even your own PHP scripts.

These tips and tricks can help you increase your code’s readability and help make the code shorter or even faster. Of course there is no single perfect methodology because on one occasion the use of a specific tip or trick may help, but on another occasion the same tip or trick may have exactly the opposite result. Most of the time, code optimization is a matter of programming experience.

> > **Remember!** Smaller algorithms are not always the best solution to a given problem. In order to solve a specific problem, you might write a very short algorithm that unfortunately proves to consume a lot of CPU time. On the other hand, you may solve the same problem with another algorithm which, even though it seems longer, calculates the result much faster.

# ### 21.2 Choosing a Decision Control Structure

The following diagram can help you decide which decision control structure is a better choice for a given problem depending on the number of variables checked.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_250_0.png)

# ### 21.3 Streamlining the Decision Control Structure

Look carefully at the following flowchart fragment given in general form.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_251_0.png)

As you can see, two identical statements or blocks of statements exist at the beginning and two other identical statements or blocks of statements exist at the end of both paths of the dual-alternative decision structure. This means that, regardless of the result of the Boolean expression, these statements are executed either way. Thus, you can simply move them outside and (respectively) right before and right after the dual-alternative decision structure, as shown in this equivalent structure.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_251_1.png)

# Exercise 21.3-2 “Shrinking” the PHP Script

Rewrite the following PHP script using fewer statements.

```php
<?php
  $a = trim(fgets(STDIN));

  if ($a > 0) {
    $y = $a * 4;
    echo y;
  }
  else {
    $y = $a * 3;
    echo $y;
  }
?>
```

# Solution

As you can see, the statement `echo $y` exists in both paths of the dual-alternative decision structure. This means that, regardless of the result of the Boolean expression, this statement is executed either way. Therefore, you can simply move the statement outside and right after the dual-alternative decision structure, as shown here.

```php
<?php
$a = trim(fgets(STDIN));

if ($a >= 30) {
    echo "Wrong Number";
}
else {
    if ($a < 10) {
        $y = $a * 2;
    }
    elseif ($a < 20) {
        $y = $a / 2;
    }
    else {
        $y = $a + 2;
    }

    echo $y;
}
?>
```

```php
elseif ($b > 20) {
    $y++;
}
else {
    $y--;
}

echo $y;
?>
```

# Solution

The $y++ statement is executed when **either** variable $a is greater than 10 **or** variable $b is greater than 20. Therefore, you can rewrite the PHP script using an OR (||) logical operator.

```php
<?php
$a = trim(fgets(STDIN));
$b = trim(fgets(STDIN));

$y = 0;

if ($a > 10 || $b > 20) {
    $y++;
}
else {
    $y--;
}

echo $y;
?>
```

# 21.5 Merging Two or More Single-Alternative Decision Structures

Many times, an algorithm contains two or more single-alternative decision structures in a row which actually evaluate the same Boolean expression. An example is shown next.

