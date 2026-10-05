For example, score, footballTeam, _score, and FootballTeam are all valid variables, but only the first two are recommended.

# Declaring variables

Variables hold values. C# has many different types of values that it can store and process: integers, floating-point numbers, and strings of characters, to name three. When you declare a variable, you must specify the type of data it will hold.

You declare the type and name of a variable in a declaration statement. For example, the statement that declares that the variable age holds int (integer) values. As always, you must terminate the statement with a semicolon.

```
int age;
```

The variable type int is the name of one of the primitive C# types, integer, which is a whole number. (You'll learn about several primitive data types later in this chapter.)

> Note
If you're a Visual Basic programmer, you should note that C# does not allow implicit variable declarations. You must explicitly declare all variables before you use them.

After you've declared your variable, you can assign it a value. The statement that follows assigns age the value 42. Again, note that the semicolon is required.

```
age = 42;
```

The equal sign (=) is the assignment operator, which assigns the value on its right to the variable on its left. After this assignment, you can use the age variable in your code to refer to the value it holds. The next statement writes the value of the age variable (42) to the console:

```
Console.WriteLine(age);
```