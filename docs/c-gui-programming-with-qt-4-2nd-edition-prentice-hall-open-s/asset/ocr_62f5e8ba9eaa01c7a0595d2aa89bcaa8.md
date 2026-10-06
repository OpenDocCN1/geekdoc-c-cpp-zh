required to declare a variable. Read-only variables are declared with const instead of main() function. Another noteworthy feature of the preceding program is that there is not that code that is located outside any function is executed immediately, starting from the top of the file and working down to the bottom.

Unlike C++, semicolons at the end of the statements are generally optional in ECMAScript. Using simplistic rules, the interpreter can insert missing semicolons itself. Despite this, using semicolons ourselves is recommended, to avoid unpleasant surprises.

To run the above, we can use the qscript interpreter located in Qt's examples/script/qscript directory. If the interpreter is called with a filename as a command-line argument, the file is taken to be ECMAScript and is executed; otherwise, an interactive session begins.

If we don't provide an initial value when declaring a variable with var, the default value is undefined, a special value of type Undefined. We can later assign any value of any type to the variable using the assignment operator (=). Consider the following examples:

```
var x;
type x; // returns "undefined"

x = null;
type x; // returns "null"

x = true;
type x; // returns "boolean"

x = 5;
type x; // returns "number"

x = "Hello";
type x; // returns "string"
```

The typeof operator returns a lowercase string representation of the data type associated with the value stored in a variable. ECMAScript defines five primitive data types: Undefined, Null, Boolean, Number, and String. The Undefined and Null are special types for the undefined and null constants, respectively. The Boolean type consists of two values, true and false. The Number type stores floating-point numbers. The String type stores Unicode strings.

Variables can also store objects and functions, corresponding to the data types Object and Function. For example: