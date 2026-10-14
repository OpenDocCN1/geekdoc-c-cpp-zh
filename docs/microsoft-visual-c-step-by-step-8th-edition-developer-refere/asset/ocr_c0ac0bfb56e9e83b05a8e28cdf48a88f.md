```
int age;
```

The variable type *int* is the name of one of the *primitive* C# types, *integer*, which is a whole number. (You’ll learn about several primitive data types later in this chapter.)

# Note

If you are a Visual Basic programmer, you should note that C# does not allow implicit variable declarations. You must explicitly declare all variables before you use them.

After you’ve declared your variable, you can assign it a value. The statement that follows assigns *age* the value 42. Again, note that the semicolon is required.

```
age = 42;
```

The equal sign (=) is the *assignment* operator, which assigns the value on its right to the variable on its left. After this assignment, you can use the *age* variable in your code to refer to the value it holds. The next statement writes the value of the *age* variable (42) to the console:

```
Console.WriteLine(age);
```

# Tip

If you leave the mouse pointer over a variable in the Visual Studio 2015 Code and Text Editor window, a ScreenTip indicates the type of the variable.

# Working with primitive data types

C# has a number of built-in types called *primitive data types*. The following table lists the most commonly used primitive data types in C# and the range of values that you can store in each.