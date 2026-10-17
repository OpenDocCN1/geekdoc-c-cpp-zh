
```php
$x = $x - $y;
 echo "Hello Olympians!";
 if ($x + $y == 24) {
   echo "The sum of x + y equals to 24";
 }
 else {
   echo "Nothing of the above";
 }
 }
 ?>
```

### Solution

This is the case in which you can’t proceed with the conversion because there are some statements (in bold) existing between the else and if keywords.

## 21.10 Converting a Case Decision Structure to Nested Decision Control Structures, and Vice Versa

Converting a case decision structure to nested decision control structures is quite easy. All you need to do is get the variable or the expression that the switch statement evaluates and use it in all nested decision control structures.

### Case Decision Structure

```
switch (var_expr) {
  case value-1:
    block of statements 1
    break;
  case value-2:
    block of statements 2
    break;
  case value-3:
    block of statements 3
    break;
  .
  .
  .
  case value-N:
    block of statements N
    break;
  default:
    block of statements N+1
}
```

### Nested Decision Control Structures

```
if (var_expr == value-1) {
  block of statements 1
}
else {
  if (var_expr == value-2) {
    block of statements 2
  }
  else {
    if (var_expr == value-3) {
      block of statements 3
    }
    .
    .
    .
    else {
      if (var_expr == value-N) {
        block of statements N
      }
      else {
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_276_0.png)

### Exercise 21.10-1 *Converting the PHP Script*

> **Notice:** The opposite conversion (from nested decision control structures to a case decision structure) is possible as long as the `else` keyword and the succeeding `if` statement (in the nested decision control structures) are side by side without any statements existing between them, and as long as the same variable or expression is evaluated for all paths. Moreover, this variable or expression should be tested in each path to determine if it is equal to constant values `value-1`, `value-2`, and `value-N` respectively.

Rewrite the PHP script using nested decision control structures.

```php
<?php
echo "What is your name? ";
$name = trim(fgets(STDIN));
if ($name == "John") {
    echo "You are my cousin!";
}
else {
    if ($name == "Aphrodite") {
        echo "You are my sister!";
    }
    else {
        if ($name == "Loukia") {
            echo "You are my mom!";
        }
        else {
            echo "Sorry, I don't know you.";
        }
    }
}
?>
```

### Solution

All nested decision control structures should evaluate the same variable `$name`.

### Exercise 21.10-2 *Converting the PHP Script*

Rewrite the PHP Script using the case decision structure.

```php
<?php
echo "Enter a number: ";
$x = trim(fgets(STDIN));
echo "Enter a second number: ";
$y = trim(fgets(STDIN));

if ($x == 1) {
    echo "Hello Zeus!";
}
else {
    $x = $x + $y;
    echo "Hello Olympians!";
    if ($x == 2) {
        echo "Hello to everyone!";
    }
    else {
        $x = $x - $y;
        echo "Hello again!";
        if ($x == 3) {
            echo "Hello and goodbye!";
        }
        else {
            echo "Gooooooood morning NY!";
        }
    }
}
?>
```

### Solution

Once again, this is a case in which you can't proceed with the conversion because there are some statements (in bold) existing between else and if keywords.

## 21.11 What is Code Indentation and Why is it so Important?

As you've been reading through this book, you may wonder why space characters appear in front of the PHP statements and why these statements are not written at the leftmost edge of the paragraph, as in the following example.

```php
<?php
echo "Enter a number: ";
$x = trim(fgets(STDIN));
echo "Enter a second number: ";
$y = trim(fgets(STDIN));
if ($x > 5) {
echo "Variable x is greater than 5";
}
else {
$x = $x + $y;
echo "Hello Zeus!";
if ($x == 3) {
echo "Variable x equals to 3";
}
else {
$x = $x - $y;
echo "Hello Olympians!";
if ($x + $y == 24) {
echo "The sum of x + y equals to 24";
}
else {
echo "Nothing of the above";
}
}
}
?>
```

The answer is obvious! A code without indentation is difficult to read and understand. Anyone who reads a code written this way gets confused about the if-else pairing (that is, to which if an else belongs). Moreover, if a long PHP script is written this way, it is almost impossible to find, for example, the location of a forgotten closing brace }.

Code indentation can be defined as a way to organize your source code. Indentation formats the code using spaces or tabs in order to improve readability. Well indented code is very helpful, even if it takes some extra effort, because in the long run it saves you a lot of time when you revisit your code. Unfortunately, it is sometimes overlooked and the trouble occurs at a later time. Following a particular programming style helps you to avoid syntax and logic errors. It also helps programmers to more easily study and understand code written by others.

> **Notice:** Code indentation is similar to the way authors visually arrange the text of a book. Instead of writing long series of sentences, they break the text into chapters and paragraphs. This action doesn’t change the meaning of the text but it makes it easier to read.

All statements that appear inside a set of braces { } must always be indented. For example, by indenting the statements inside a dual-alternative decision structure, you visually set them apart. As a result, anyone can tell at a glance which statements are executed when the Boolean expression evaluates to true, and which are executed when the Boolean expression evaluates to false.

> **Notice:** Only humans have difficulty reading and understanding a script without indentation. A computer can execute any code, written with or without indentation, as long as it contains no syntax errors.

## 21.12 Using the “From Inner to Outer” Method in Decision Control Structures

“From inner to outer” is a method proposed by this book to help you learn “Algorithmic Thinking” from the inside out. This method first manipulates and designs the inner (nested) control structures. Then, as the algorithm is developed, more and more control structures are added, nesting the previous ones.

Let’s try the following example.

*Design a flowchart that lets the user enter a number and, if its last digit is equal to 5, a message “Last digit equal to 5” is displayed; otherwise, a message “Nothing special” is displayed. Moreover, if the user enters a non-numeric character, an error message should be displayed.*

First, you can design the inner decision structure that displays the messages “Last digit equal to 5” or “Nothing special” (depending on the last digit). The flowchart fragment is shown here.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_281_0.png)

> **Remember!** You can isolate the last digit of any number using the modulus 10 operation. It is not necessary to know the exact number of digits.

Now let’s deal with the data validation problem. In this exercise, you need to test whether or not the user has entered a valid numeric value. If not, an error message should be displayed; otherwise, you can proceed to check the last digit. The outer decision structure is shown in the flowchart that follows.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_281_1.png)

Now, you can combine both flowchart fragments, nesting the first into the second one and the final flowchart becomes

![](img/4d9a992abc5da7946ac44f9e6bf1d032_282_0.png)

Now you may wonder why we go to all this trouble. It was too easy and it could have been designed as usual without the use of the “from inner to outer” method. Yes, you are probably right. But imagine this method used in very large and complicated control structures. It can help you design error-free flowcharts or even PHP scripts and save you a lot of effort! This book uses this method wherever and whenever it seems necessary.

## 21.13 Review Questions: True/False

Choose **true** or **false** for each of the following statements.

- 1. Smaller algorithms are always the best solution to a given problem.
- 2. You can move a statement outside, and right before, a dual-alternative decision structure as long as it exists at the beginning of both paths of the decision structure.
- 3. You can always use a logical operator instead of nested decision control structures to increase readability.
- 4. Two single-alternative decision structures can be merged into one single-alternative decision only when they are in a row and when they evaluate the same Boolean expression.
- 5. Conversion from a dual-alternative decision structure to two single-alternative decision structures is always possible.
- 6. Two single-alternative decision structures can be “merged” into (actually, replaced by) one dual-alternative decision only when they are in a row and only when they evaluate the same Boolean expression.
- 7. Conversion from a case decision structure to a multiple-alternative decision structure is always possible.
- 8. Conversion from a multiple-alternative decision structure to a case decision structure is always possible.
- 9. Conversion from a multiple-alternative decision structure to nested decision control structures is always possible.
