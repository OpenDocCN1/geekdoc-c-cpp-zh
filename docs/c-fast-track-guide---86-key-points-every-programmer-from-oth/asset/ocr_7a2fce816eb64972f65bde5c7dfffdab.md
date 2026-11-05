# 42. EASIER STRING FORMATTING WITH INTERPOLATED STRINGS

Interpolated strings make it easier to build strings with variables, replacing the older and harder-to-read string formatting methods.

Here's how you can combine variables and text in a clean and readable way using $"...".

[Code Example]

```
string name = "Alice";
int age = 30;
// Interpolated string using variables inside the string
string message = $"Hello, my name is {name} and I am {age} years old.";
Console.WriteLine(message);
```

[Execution Result]

Hello, my name is Alice and I am 30 years old.

Traditionally, C# developers used methods like string.Format() or concatenation (+) to combine strings and variables, which can be hard to read:

```
string msg = "Hello, my name is " + name + " and I am " + age + " years old.";
```

But interpolated strings—introduced in C# 6—make this much cleaner and more readable.

Use the $ symbol before a string literal to start interpolation.

Place variables or expressions inside {} directly in the string.