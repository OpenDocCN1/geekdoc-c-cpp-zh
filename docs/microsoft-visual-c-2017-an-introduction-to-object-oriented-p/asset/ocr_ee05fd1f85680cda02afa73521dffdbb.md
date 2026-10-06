# Overloading Methods

**Overloading** involves the ability to write multiple versions of a method using the same name. When you make a purchase at a store, you might use one of "pay" methods they accept, cash, a credit card, or a check. The "pay" method works differently depending on the type of currency sent to it, but all of the transactions are called "pay." When you overload a C# method, you write multiple method implementations with the same name but different parameter lists. A method's name and parameter list constitute the **signature**.

In this book, you have seen `WriteLine()` method used with a string and a numeric parameter. You can use it with no parameter to output a blank line. You have also seen the method used with several parameters when using a format string with several variables. Therefore, you know `WriteLine()` is an overloaded method.

Some C# operators are overloaded. For example, a + between two numeric values indicates addition, but a single + to the left of a value means the value is positive. The + has different meanings based on the operands used with it. In the chapter "Using Classes and Objects," you will learn to overload operators to make them mean what you want with your own classes.

The compiler understands which method to use based on the arguments used in a method call. For example, suppose that you want a method to display a `string` surrounded by a border. The method receives a `string` and uses the `string` length to determine how many asterisks to to construct a border around the string. Figure 8-16 shows a program that performs the method.

**Figure 8-16** The BorderDemo program**