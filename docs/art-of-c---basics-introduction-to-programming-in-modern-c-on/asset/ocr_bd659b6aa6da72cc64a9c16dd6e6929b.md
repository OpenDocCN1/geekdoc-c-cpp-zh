is then initialized with a value "Joe" (a string literal), as indicated by the equal sign (=), which is known as the "assignment operator" in C#.

A string is essentially a sequence of characters. The C#'s built-in string type corresponds to the System.String class on .NET.

The values of the "constants" are determined at compile time, and they do not change during the execution of the program. In C#, the variables of a type string and other "numeric types" like int and float can be declared as const.

On the other hand, the value of a "variable" declared with var can change. For example,

```
```
var greeting = $"Hello {name}!!!!";
```
```

This statement, starting with the keyword var, declares a new variable named greeting, and it initializes the variable with the value given on the right hand side of the assignment operator, at run time.

The expression on the right hand side is what is called the "$-string interpolation". It starts with $" and ends with ". A variable, or an expression in general, enclosed in a pair of curly braces ({} ) is replaced by its value. In this example, the value of name is "Joe". And hence the value of the right hand side string interpolation expression is "Hello Joe!!!".

> A quick note on the terminology: A const constant can be viewed as a special kind of a "variable". Hence we do not always distinguish constants and variables, unless specifically needed.

C# also supports an operation called the "string concatenation". For instance, the above statement can be written as follows:

```
```
var greeting = "Hello " + name + "!!!!";
```
```