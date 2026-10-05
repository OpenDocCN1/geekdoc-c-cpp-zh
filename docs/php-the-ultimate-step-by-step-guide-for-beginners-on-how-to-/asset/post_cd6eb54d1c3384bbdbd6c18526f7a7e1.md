
```php
for ($counter<10;$counter++) {
  //check for division by zero
  if ($counter==0) {
    echo "Skipping to avoid division by zero.<br>";
    continue;
  }
  echo "100/$counter ,100/$counter,<br />";
}?>
```

The new output is like in the following sequence:

100/ - 3 - 33-3333333333
100/ - 2 - 50
100/ - 1 - 100
Skipping to maintain a strategic distance from division by zero
100/1 100
100/2 50
100/3 33.33333333333
100/4 25
100/5 20
100/6 16.6666666667
100/7 14.2857142857
100/8 12.5
100/9 11.1111111111

Notice that the loop skipped the $counter value of zero and it regardless proceeded with the next value.

We've now gone through the majority of the major program flow language constructs. We've talked about the building blocks for controlling program flow in your programs. Expressions can be as direct as TRUE or FALSE or as mind boggling as relational comparison with local operators. The expressions consolidated with program flow construct develops like the if statement and switch makes decision-making simple.

We additionally examined while, do ... while, and for for loops. Loops are extremely helpful for basic element web page tasks such as showing the outcomes from a query in an HTML table.

# CHAPTER 7: FUNCTIONS

To compose PHP programs that contain more than only a few pages of code and are still systematized well enough to be valuable, you have to have an in-depth understanding of functions. Functions let you dispose of rehashing the same lines of code again and again in your programs. Functions work by allocating a name called a function name to a lump of code. Subsequently, you execute the code by calling that name. There are many inherent functions in PHP. For instance, print_r is a function that prints coherent data around a variable in plain English as opposed to code. If given a string, number, or float, the quality itself is printed with the print_r function. If given an array, qualities are demonstrated as keys and components. A similar format is utilized for objects. In PHP 5.0, print_r and var_export show secured and private properties of objects.

Run your array from aggregate_info to imap_ping through pdf_open_image. Since there are many of them, we can just cover a few fundamentals in this chapter, although we'll give you enough data that you'll use functions to look like an expert as in a very short time.

You can look http://www.php.net for a thorough list of functions.
Specifically, we'll go over the following:

- How to make a function, give it a name, and execute that function
- How to send values to a function and utilize them in the function
- How to return values from a function and apply them in your code
- How to verify that a function exists before you attempt it

The point of coding when you may split code into a function is a somewhat of a subjective judgment call. Unquestionably, if you discover yourself rehashing a few lines of code again and again, it binds well to pull that code into its function. That will make your code simpler to read as well as protect you from having to make numerous improvements if you choose to do something else with that piece of code, as its then in only one spot, not various spots where you'd need to replace and change it.

A function is a block of code that allows values, forms them, and afterward performs an action. Consider making cakes and baking them in an oven as a function. You put the raw dough into the oven, which makes the dough mixture the input. The oven then bakes the dough mixture; this is the function. The outcome of the function for baking the cakes is the edible, baked cakes. The function may even take other inputs, for example, temperature and baking time. These different inputs are called parameters.

Parameters send data to a function, and afterward the function executes the code. Functions can use anywhere in the range of zero parameters to an entire list. In Illustration 7.1, you'll utilize the echo function to show some text. echo message that you send to it as a parameter. Most functions need you to put your parameters within parentheses, yet echo is a special case to this. Echoing of all variables is about foolproof! Figure 7.1 shows how the outcome of the script shows up in a program.

Illustration 7.1. The pervasive Hello world!

```php
<?php
echo("Hello world!");
?>
```

![](img/8e0a31fe30a159a13fdfed13405b5ed7_88_0.png)

How the echo output looks in the browser window

The echo function basically sends on the "Welcome world!" string to the program/browser once you load the PHP document. echo is in fact a PHP language construct. Basically, this means it has the capacity to work without encasing its parameters in parentheses. It's important to note that true functions need parentheses in most cases.

You can use one of PHP’s numerous inherent functions or identify your own. We’ll talk all the more about identifying your own.

## 7.1 Calling Functions

There are many inherent functions in PHP. The most common way to call a function is by using its name followed by parentheses. If the function requires arguments, these are passed inside the parentheses. For example:

```php
function greet($name) {
  echo "Hello, " . $name . "!";
}

greet("Alice"); // Outputs: Hello, Alice!
```

If a function returns a value using the `return` statement, that value can be assigned to a variable:

```php
function add($a, $b) {
  return $a + $b;
}

$result = add(5, 3); // $result now holds 8
```

Functions can also be called by reference, which allows the function to modify the original variable passed to it. This is done using the ampersand (&) symbol.

```php
function addToValue(&$value) {
  $value += 10;
}

$number = 5;
addTenValue($number); // $number is now 15
```

## 7.2 Defining Functions

To define a function, you use the `function` keyword followed by the name of the function, parentheses, and a block of code. The code within the function is enclosed in curly braces.

```php
function myFunction() {
  // code to be executed
}
```

Functions can also take parameters, which are variables defined within the parentheses.

```php
function myFunction($param1, $param2) {
  // use $param1 and $param2
}
```

You can provide default values for parameters. If no argument is provided when the function is called, the default value is used.

```php
function greet($name = "Guest") {
  echo "Hello, $name!";
}

greet(); // Outputs: Hello, Guest!
greet("Alice"); // Outputs: Hello, Alice!
```

Functions can also return values using the `return` statement. When a `return` statement is encountered, the function stops executing and returns the specified value.

```php
function multiply($a, $b) {
  return $a * $b;
}

$product = multiply(4, 5); // $product now holds 20
```

## 7.3 Scope

Variables in PHP have a local scope. A variable defined inside a function is local to that function and cannot be accessed from outside it.

```php
$x = 5; // Global variable

function myFunction() {
  $x = 10; // Local variable
  echo $x; // Outputs 10
}

myFunction();
echo $x; // Outputs 5
```

To access a global variable from inside a function, you must use the `global` keyword.

```php
$x = 5;

function myFunction() {
  global $x;
  $x = 10;
  echo $x; // Outputs 10
}

myFunction();
```

Alternatively, you can use the `$GLOBALS` array to access global variables.

```php
$x = 5;

function myFunction() {
  echo $GLOBALS['x']; // Outputs 5
}

myFunction();
```
