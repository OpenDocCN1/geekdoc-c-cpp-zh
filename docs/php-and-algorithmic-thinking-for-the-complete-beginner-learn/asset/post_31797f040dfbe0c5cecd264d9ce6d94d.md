

## 41.6 The Scope of a Variable

As already mentioned, there is a one-to-one match between the formal and the actual arguments. So what actually happens here is that the value “Vassilis Bouras” is passed to the argument `$title` leaving argument `$name` with no value. Obviously, PHP will complain about it by saying that an argument is missing for the function `prepend_title()`.

> **Notice:** The default value must be a constant value, not a variable.

The scope of a variable refers to the range of effect of that variable.

In PHP, a variable can have a local or global scope. A variable declared within a subprogram has a local scope and can be accessed only from within that subprogram. On the other hand, a variable declared outside of a subprogram has a global scope and can be accessed from within any subprogram, as well as from the main code. To access a global variable from within a subprogram, though, you must use the PHP keyword `global`.

Let’s see some examples. The next PHP script declares a global variable `$a` as well as a local variable `$b` within the procedure. The value of the global variable `$a`, though, is accessed and displayed within the procedure.

```php
<?php

function display_values() {
    global $a;
    $b = 3;             //Local scope
    echo $a, $b;        //This displays 10 3
}

$a = 10;                //Global scope
display_values();

?>
```

If you wish to access more than one global variable from within a subprogram, you can write the keyword `global` and, next to it, all the variables separated with commas, as shown here.

```php
global $a, $b, $c;
```

Be careful though! If the value of a global variable is altered within a subprogram, this change is also reflected outside of the subprogram. In the next example, the procedure `display_values()` increases the value of variable `$a` to 11, and when the flow of execution returns to the main code, variable `$a` still contains the value 11.

```php
<?php

function display_values() {
    global $a, $b;       //Permit access to global variables $a and $b
```

## Chapter 41
Tips and Tricks with Subprograms

a procedure doesn’t. Of course, if you pass your arguments by reference, then both of them can return many results—indirectly, of course.

- determine which variables participate in each part of the script and their roles in that part. The flowchart that follows can help you decide what to do with each variable, whether it should be passed to the subprogram and/or returned from the subprogram, or if it should just be a local variable within the subprogram.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_818_0.png)

So, with the help of this flowchart, let’s discuss each part of the script independently! The parts that are not marked with a dashed rectangle will comprise the main code.

### First part

In the first part of the script, there are three variables: $i, $temp1, and $sex. However, not all of them must be included in the formal argument list. Let’s find out why!

### Variable $answer

- is not initialized/updated outside of the subprogram; thus, it should not be passed to the subprogram
- is initialized within the subprogram and its value is used outside of it; thus, it must be returned to the caller

Therefore, since only one value must be returned to the main code, a function can be used, as shown here.

```php
function part2() {
do {
echo "Do you go jogging in the afternoon? ";
$temp2 = trim(fgets(STDIN));
$Answer = strtolower($temp2);
} while ($Answer != "yes" && $Answer != "no" && $Answer != "sometimes");
return $Answer;
}
```

### Third part

In the third part of the example, there are four variables: $answer, $total_yes, $sex and $female_no and all of them must be included in the formal argument list. Let’s find out why!

- Both variables $answer and $sex
  - are initialized/updated outside of the subprogram; thus, they must be passed to the subprogram
  - are not updated within the subprogram; thus, they should not be returned to the caller
- Both variables $total_yes and $female_no
  - are initialized outside of the subprogram; thus, they must be passed to the subprogram
  - are updated within the subprogram and their value is used outside of it; thus, they must be returned to the caller

Therefore, since two values must be returned to the main code, a procedure can be used. The variables $total_yes and $female_no must be passed by reference so that their values can be returned to the main code (indirectly), as shown here.

```php
function part3($answer, $sex, &$total_yes, &$female_no) {
if ($answer == "yes") {
$total_yes++;
}

if ($sex == "female" && $answer == "no") {
$female_no++;
}
```

### Fourth part

In the fourth part of the example, there are two variables: `$total_yes` and `$female_no`.
Let’s see what you should do with them.

- Both variables `$total_yes` and `$female_no`
- are updated outside of the subprogram; thus, they must be passed
- to the subprogram
- are not updated within the subprogram; thus, they should not be
- returned to the caller

Therefore, since no value should be returned to the main code, a procedure can be
used, as shown here.

```php
function part4($total_yes, $female_no) {
echo "Total positive answers: ", $total_yes;
echo "Women's negative answers: ", $female_no;
}
```

### The final script

The final script, including the main code and all the subprograms cited above, is
shown here.

```php
file_41.7b.php
<?php
function part1($i) {
do {
echo "Enter Sex for Citizen No ", $i, ": ";
$temp1 = trim(fgets(STDIN));
$sex = strtolower($temp1);
} while ($sex != "male" && $sex != "female");
return $sex;
}
function part2() {
do {
echo "Do you go jogging in the afternoon? ";
$temp2 = trim(fgets(STDIN));
$answer = strtolower($temp2);
} while ($answer != "yes" && $answer != "no" && $answer != "sometimes");

return $answer;
}

function part3($answer, $sex, &$total_yes, &$female_no) {
    if ($answer == "yes") {
        $total_yes++;
    }

    if ($sex == "female" && $answer == "no") {
        $female_no++;
    }
}

function part4($total_yes, $female_no) {
    echo "Total positive answers: ", $total_yes;
    echo "Women's negative answers: ", $female_no;
}

$total_yes = 0;
$female_no = 0;
for ($i = 1; $i <= 100; $i++) {
    $sex = part1($i);
    $answer = part2();

    part3($answer, $sex, $total_yes, $female_no);
}

part4($total_yes, $female_no);
?>
```

## 41.8 Recursion

Recursion is a programming technique in which a subprogram calls itself. This might initially seem like an endless loop, but of course this is not true; a subprogram that uses recursion must be written in a way that obviously satisfies the property of finiteness.

Imagine that the next PHP script helps you find your way home. In this script, recursion occurs because the procedure `find_your_way_home()` calls itself within the procedure.

```php
<?php
function find_your_way_home () {
    if (you_are_already_at_home == true) {
        stop_walking();
    }
    else {
        take_one_step_toward_home();
        find_your_way_home();
    }
}

find_your_way_home();
?>
```

Now, let’s try to analyze recursion through a real example. The next PHP script calculates the factorial of 5 using recursion.

```php
<?php
function factorial($value) {
    if ($value == 1) {
        $return_value = 1;
    }
    else {
        $return_value = $value * factorial($value - 1);
    }

    return $return_value;
}

echo factorial(5);      //This displays 120
?>
```

> **Remember!** In mathematics, the factorial of a non-negative integer N is the product of all positive integers less than or equal to N. It is denoted by N! and the factorial of 0 is, by definition, equal to 1. For example, the factorial of 5 is 1 × 2 × 3 × 4 × 5 = 120.

> **Notice:** Recursion occurs because the function `factorial()` calls itself within the function.

> **Notice:** Please note that there isn’t any loop control structure!

You are probably confused right now. How on Earth was the product 1 × 2 × 3 × 4 × 5 calculated without using a loop control structure? The next diagram may help you understand. It shows the multiplication operations that are performed as function `factorial()` works its way backwards through the series of calls. When the function

