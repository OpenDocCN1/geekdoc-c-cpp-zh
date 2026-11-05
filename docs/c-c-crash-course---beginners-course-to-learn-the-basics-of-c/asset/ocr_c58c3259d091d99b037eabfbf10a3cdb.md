You can use the Console.WriteLine method to show different kinds of data on the user’s screen. That’s because the Console class has a built-in version of each data type.

The only difference between Console.WriteLine and Console.Write is that the former prints the value within the parentheses and adds a newline character on the console whereas the latter simply shows the information inside the parentheses. Thus, using Console.WriteLine in your codes is like hitting the “Enter” key after showing the message (i.e. The cursor will go to the next line.).

# String Concatenation

The C# language prevents programmers from using operators on strings values. Obviously, you can’t perform arithmetic operations on actual words (e.g. fish – dog, power * humans, land / people, etc.). However, C# allows you to concatenate (i.e. combine) multiple string objects to generate a new one. You can do this by using the “+” symbol on your strings. The example given below will illustrate this idea.

```
string gadget = "smartphone";
string example = "I use my " + gadget + " to access " + "the internet.";
Console.WriteLine(example);
```

If you’ll execute that code, the console will display this:

I use my smartphone to access the internet.