# After execution, the RAM looks like this.

![](bbox=[0.336, 0.088, 0.696, 0.266])

> **Remember!** While a PHP script is running a variable can hold various values, but only one value at a time. When you assign a value to a variable, this value remains stored until you assign a new value. The old value is lost.

A variable is one of the most important elements in computer science because it helps you interact with data stored in the main memory (RAM). Soon, you will learn all about how to declare and use variables in PHP.

# 5.2 What is a Constant?

Sometimes you may need to use a value that cannot change while the program is running. Such a value is called a “constant.” In simple terms, you could say that a constant is a locked variable. This means that when a program begins to run and a value is assigned to the constant, nothing can change the value of the constant while the program is running. For example, in a financial program an interest rate can be declared as a constant.

A descriptive name for a constant can also improve the readability of your program and help you avoid errors. For example, let’s say that you are using the value 3.14159265 (but not as a constant) at many points throughout your program. If you make an error when typing the number, this will produce the wrong results. But, if this value is given a name, any typographical error in the name is detected by PHP, and you are notified with an error message.

In a flowchart, you can represent the action of setting a constant equal to a value with the equals sign, (=).

![](bbox=[0.389, 0.784, 0.632, 0.866])

> **Notice:** This book uses the reserved word `Const` to distinguish a constant from a variable.