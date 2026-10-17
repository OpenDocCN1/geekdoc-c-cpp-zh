

- 25. Using the insertion sort algorithm, write the code fragment that sorts array `$a` of N elements in ascending order.
- 26. What is a searching algorithm?
- 27. Name the two most commonly used search algorithms.
- 28. What are the advantages and disadvantages of the linear search algorithm?
- 29. Using the linear search algorithm, write the code fragment that searches array `$a` for value `$needle`.
- 30. What are the advantages and disadvantages of the binary search algorithm?
- 31. Using the binary search algorithm, write the code fragment that searches array `$a` for value `$needle`. Assume array `$a` is sorted in ascending order.

## Section 7

### Subprograms

### 38.1 What is Procedural Programming?

Suppose you were assigned a project to solve the drug abuse problem in your area. One possible approach, which could prove very difficult or even impossible, would be to try to solve this problem by yourself! A better approach would be to subdivide the large problem into smaller subproblems such as prevention, treatment, and rehabilitation. Then, with the help of specialists from a variety of fields, you would build a team to help solve the drug problem. The following diagram shows how each subproblem could be further subdivided into even smaller subproblems.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_770_0.png)

As the supervisor of this project, you could rent a building and establish within it three departments: the prevention department, with all of its subdepartments; the treatment department, with all of its subdepartments; and the rehabilitation department, with all of its subdepartments. Finally, you would hire staff and employ them to do the job for you!

Procedural programming does exactly the same thing. It subdivides an initial problem into smaller subproblems, and each subproblem is further subdivided into smaller subproblems. Finally, for each subproblem a small subprogram would be written, and the main program (as does the supervisor) employs (calls) them to do the job!

Procedural programming has several advantages:

- It enables programmers to reuse the same code whenever it is necessary without having to copy it.
- It is relatively easy to implement.
- It helps programmers follow the flow of execution more easily.

> **Notice:** A very large program can prove very difficult to debug and maintain when it is all in one piece. For this reason, it is often easier to subdivide it into smaller subprograms, each of which performs a clearly defined process.

> **Notice:** Writing large programs without subdividing them into smaller subprograms results in a code referred to as "spaghetti code".

## Chapter 39

### User-Defined Functions

### 39.1 Writing Your Own Functions in PHP

In PHP, and by extension in the majority of computer languages, there are two kinds of functions. There are the built-in functions, such as `trim()`, `strpos()`, `sin()`, and there are the user-defined functions, those that you can actually write and use in your own scripts.

The general form of a PHP function is

```
function name([arg1, arg2, arg3, ...]) {
    A statement or block of statements
    return value;
}
```

where

- `name` is the name of the function. It follows the same rules as those used for variable names.
- `arg1, arg2, arg3, ...` is a list of arguments (variables) used to pass values from the caller to the function. There can be as many arguments as you want.
- `value` is the arithmetic, alphanumeric, or Boolean value that is returned to the caller. It can be a constant value, a variable, an expression or even an array.

> **Notice:** Please note that arguments are optional; that is, a function may contain no arguments.

For example, the next function calculates the sum of two numbers and returns the result.

```php
function get_sum($num1, $num2) {
    $result = $num1 + $num2;
    return $result;
}
```

Of course, this can also be written as

```php
function get_sum($num1, $num2) {
    return $num1 + $num2;
}
```

### 39.2 How Do You Call a Function?

Every call to a user-defined function is made in the same way as calling the built-in functions of PHP. You write the name of the function followed by a list of arguments (if necessary), either within a statement that assigns the function's returned value to a variable or directly within an expression.

Let's see some examples. Suppose there is a function `cube_root()` that accepts an argument (a numeric value) and returns its 3rd root. To calculate the expression, you can either assign the cube root of x to a variable, as shown here

```php
$x = trim(fgets(STDIN));
$cb = cube_root($x);
$y = $cb + 1 / $x;
echo $y;
```

or you can call the function directly in an expression,

```php
$x = trim(fgets(STDIN));
$y = cube_root($x) + 1 / $x;
echo $y;
```

or you can even call the function directly in an echo statement.

```php
$x = trim(fgets(STDIN));
echo cube_root($x) + 1 / $x;
```

Now let's see a more complete example. The next PHP script creates the function `get_message()` and then the main code calls it. The returned value is assigned to variable `$a`.

**file_39.2a.php**

```php
<?php
function get_message() {
    $msg = "Hello Zeus";
    return $msg;
}

echo "Hi there!";
$a = get_message();
echo $a;
?>
```

> **Notice:** Please note that a function does not execute immediately when a script starts running. The first statement that actually executes in this example is the statement `echo "Hi there!"`.

You can also pass (send) values to a function, as long as at least one argument exists within the function's parenthesis. In the next example, the function `display()` is called three times but each time a different value is passed through the argument `$color`.

**file_39.2b.php**

```php
<?php
function display($color) {
    $msg = "There is " . $color . " in the rainbow\n";
    return $msg;
}
echo display("red");
echo display("yellow");
echo display("blue");
?>
```

If you run this script, the following messages are displayed.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_776_0.png)

In the next example, two values must be passed to function `display()`.

```php
<?php
function display($color, $exists) {
    $neg = "";
    if ($exists == false) {
        $neg = "n't any";
    }

    return "There is" . $neg . " " . $color . " in the rainbow\n";
}
echo display("red", true);
echo display("yellow", true);
echo display("black", false);
?>
```

If you run this script, the following messages are displayed.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_777_0.png)

> **Notice:** You can place your functions either above or below your main code. Most programmers, though, prefer to have them all on the top for better observation.

### 39.3 Formal and Actual Function Arguments

Each function contains an argument list called a "formal argument list." As already stated, arguments in this list are optional; the formal argument list may contain no arguments, one argument, or more than one argument.

When the function is called, an argument list is passed to the function. This list is called an "actual argument list."

In the next example, variables `$number1`, `$number2`, `$number3`, and `$number4` constitute the formal argument list whereas variables `$a`, `$b`, `$c`, and `$d` constitute the actual argument list.

```php
<?php
    function add($number1, $number2, $number3, $number4) {

        $result = $number1 + $number2 + $number3 + $number4;
        return $result;
    }

    $a = trim(fgets(STDIN));
    $b = trim(fgets(STDIN));
    $c = trim(fgets(STDIN));
    $d = trim(fgets(STDIN));

    $sum = add($a, $b, $c, $d);
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_777_1.png)

### 39.4 How Does a Function Execute?

When the main code calls a function the following steps are performed:

- The execution of the statements of the main code is interrupted.

- The values of the variables or the result of the expressions that exist in the actual argument list are passed (assigned) to the corresponding arguments (variables) in the formal argument list, and the flow of execution goes to where the function is written.

- The statements of the function are executed.

- When the flow of execution reaches the end of the function, a value is returned from the function to the main code and the flow of execution continues from where it was before calling the function.

In the next PHP script, the function `maximum()` accepts two arguments (numeric values) and returns the greater of the two values.

```php
<?php
function maximum($val1, $val2) {
    $m = $val1;
    if ($val2 > $m) {
        $m = $val2;
    }
    return $m;
}

$a = trim(fgets(STDIN));
$b = trim(fgets(STDIN));
$max = maximum($a, $b);
echo $max;
?>
```

When the PHP script starts running, the first statement executed is the statement `$a = trim(fgets(STDIN))` (this is considered the first statement of the script). Suppose the user enters the values 3 and 8. Below is a trace table that shows the exact flow of execution, how the values of the variables `$a` and `$b` are passed from the main code to the function, and how the function returns its result.

> **Notice:** Please note that there is a one-to-one match between the formal and the actual arguments. The value of argument `$a` is passed to argument `$number1`, the value of argument `$b` is passed to argument `$number2`, and so on.

