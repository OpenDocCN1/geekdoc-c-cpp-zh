composed of multiple declarations in one line, as in the following example:

Int number = 20, Boolean completed = true, string hello = “Hello World!”;

Java variables can be declared without any value at the start; in cases such as these, Java chooses to declare these variables with a particular default value, for example:

Byte a;

Short num;

Boolean answer;

Will result in the values 0, 0, and false, respectively. A more complete list of default values is as follows: the byte, short, int, and long data types will all result in a default value of 0, while the float and double data types will have a default 0.0 value, the char data type will result in ‘\u0000’ value, a string or any other object will have a null default value, and all Booleans will begin with a false default value.

In Java, variables are static when declared, meaning that the programmer must define the data type that the variable will be containing. To illustrate, if we wish to use a variable num to store a number, we would first have to declare the variable: "int num," before we can assign a value, such as "num = 10."

The process above is usually known as and referred to as an "assignment statement," where a value is assigned to the variable as declared by the programmer. However, one prominent thing about how Java, and in fact how most programming languages, works is that in the assignment statement, such as in our example of num = 10, the actual value stored is the one on the right side of the equals sign, the value of 10, and num is just the "marker" to call that stored value. This is why there are many Java programmers that tend to prefer the jargon of "getting" a value rather than "assigning," though