
program can also send its output to the screen, to an external file, to a printer, etc.

## System.Console

The class named System.Console has various methods and attributes that you can use to read, display, or format text-based information. Three of the most popular attributes of the System.Console class are related to entering and showing data. These attributes are: Console.In, Console.Out, and Console.Error.

These attributes help you in displaying data, reading information, and reporting error messages. C# allows you to use these attributes directly. However, you need to keep in mind that System.Console contains other methods and attributes that can help you with I/O operations.

Important Note: The C# language allows you to modify the default streams of your programs. To do that, you need to use the following methods: Console.SetOut (for the Output stream), Console.SetIn (for the Input Stream), and Console.SetError (for the Error stream).

## The Console Input

Programming languages have a system for entering information into the computer’s console. The C# language, in particular, uses an object called "Console.In" to control its input stream.

Actually, you don’t have to use Console.In directly. The "Console" class offers two methods (i.e. Console.ReadLine and Console.Read) that work with Console.In. You can use these methods to read data from your command prompt.

### The Console.ReadLine Method

This method offers simplicity and convenience for people who want to read data from their console. When you call this method, your program will stop and wait for the user’s input. Then, the user may enter a character or a string and hit "Enter". By pressing the Enter key, the user informs the program that they have entered the needed input. The Console.ReadLine method will read the user’s input, hence the name.

The code given below will show you how Console.ReadLine works:

```csharp
class Test
{
    static void Main()
    {
        System.Console.WriteLine("What is your first name? ");
        string yourfirstName = System.Console.ReadLine();

        System.Console.WriteLine("Please enter your last name? ");
        string yourlastName = System.Console.ReadLine();

        System.Console.WriteLine("Hi, {0} {1}!", yourfirstName, yourlastName);
    }
}
```

If you’ll enter "John" and "Smith" into the command prompt, you’ll get the following message:

![](img/e2e831cc76860601d1e5511399855ee6_29_0.png)

### The Console.Read Method

There are significant differences between Console.Read and Console.ReadLine. First, Console.Read reads a single character only while Console.ReadLine reads the entire expression. Second, Console.Read returns a code rather than the accepted input. If you want to utilize the output as an ordinary character, you should do one of these things:

- Convert the output into a character
- Use the Convert.ToChar method on the result

Important Note: Console.Read will only read a character if the user hits "Enter". When the user presses this key, the program will transfer the input to the standard input buffer and invoke the Console.Read method. Check the example given below:

```csharp
class UsingRead
{
    static void Main()
    {
        int codeRead = 0;
        do
        {
            codeRead = Console.Read();
            if (codeRead != 0)
            {
                Console.Write((char)codeRead);
            }
        }
        while (codeRead != 10);
    }
}
```

### How to Read a Number

C# programs don’t read numbers directly. They need to take the inputs as strings (i.e. through the Console.ReadLine method) and convert them into numbers. The process of converting strings into other data types is known as parsing. All of the primitive data types in the C# language support this process.

## The Console Output

This part of the book will focus on two methods: Console.WriteLine and Console.Write. Both of these methods can print all of the data types in C# language. That means you can use them to display messages on the user’s console.

The following code snippets will teach you how these methods work:

```csharp
Console.WriteLine("I want to learn the C# programming language.");
// This line will print the string inside the parentheses.

Console.WriteLine(100);
// This line will show "100" on the user’s command prompt.

Console.WriteLine(3.14);
// This line will print the double value 3.14 on the user’s console.
```

You can use the Console.WriteLine method to show different kinds of data on the user’s screen. That’s because the Console class has a built-in version of each data type.

The only difference between Console.WriteLine and Console.Write is that the former prints the value within the parentheses and adds a newline character on the console whereas the latter simply shows the information inside the parentheses. Thus, using Console.WriteLine in your codes is like hitting the "Enter" key after showing the message (i.e. The cursor will go to the next line.).

## String Concatenation

The C# language prevents programmers from using operators on string values. Obviously, you can’t perform arithmetic operations on actual words (e.g. fish - dog, power * humans, land / people, etc.). However, C# allows you to concatenate (i.e. combine) multiple string objects to generate a new one. You can do this by using the "+" symbol on your strings. The example given below will illustrate this idea.

```csharp
string gadget = "smartphone";
string example = "I use my " + gadget + " to access " + "the internet.";
Console.WriteLine(example);
```

If you’ll execute that code, the console will display this:

I use my smartphone to access the internet.

## Chapter 6: The Conditional Statements of C#

This chapter will teach you how to use conditional statements in your C# codes. Basically, a conditional statement is a code block that allows you to perform various actions based on the assigned condition/s. Read this material carefully as it contains valuable information that can help you master C# in just 7 days.

### The Operators

In this section, you’ll learn more information about the comparison operators of C#. These operators are extremely important: they can help you in setting the conditions for your own conditional statements.

### The Comparison Operators

C# has different operators that you can use to compare values of the same type. These operators are:

- `<`
- `>`
- `<=`
- `>=`
- `!=`
- `==`

You may use the operators given above to compare C# expressions (e.g. two integers, two variables, two constants, etc.). While using any of these operators, the result will always be a Boolean. Analyze the following examples:

```csharp
int height = 170;
Console.WriteLine(height < 180); // This will give you "true".

string gender = "Male";
Console.WriteLine(gender == "Female"); // This will give you "false".

double valueofPi = 3.14;
Console.WriteLine(valueofPi > 100); // This will give you "false".
```

### The Logical Operators

C# also supports some logical operators. Programmers use these operators to create Boolean (also called "logical") statements. Let’s discuss each logical operator in detail:

### The AND and OR Operators

You can only use the logical AND (i.e. &&) and logical OR (i.e. ||) operators on expressions that involve Boolean values. The logical AND operator will give you "true" if both of the operands are true. For example:

```csharp
bool sample = (1 < 2) && (10 == 10);
```

Since 1 is less than 2 and 10 is equal to 10, the expression will give you true. Since the logical AND operator provides quick results without performing unnecessary analyses, programmers refer to it as a "short-circuit operator". It checks the left section of the statement first. If the evaluation is "false", the operation will immediately stop. The expression can no longer be true since one of the operands is false.

The logical OR (i.e. ||) operator, on the other hand, will give you true if at least one of your operands evaluates to true. For instance:

```csharp
bool sample = (1 < 2) || (10 > 100);
```

This example will give you true since the left-hand operand is true. The logical OR operator is also a "short-circuit operator", since it can give a result even without checking the entire C# statement. In the current example, logical OR will no longer analyze the second operand since the first one is already true. Thus, the condition has already been met.

### The Exclusive OR and Negation Operators

The exclusive OR (i.e. ^) is a full-circuit operator since it needs to check both operands before giving the result. It will give you true ONLY IF one of the operands evaluates to true. Thus, you’ll get false if both of the operands are true. Check the following example:

```csharp
bool sample = (1 < 2) ^ (2 == 2);
```

Since the two expressions are true, exclusive OR will give you false.

The negation operator (i.e. !), however, simply reverses the Boolean value to which it is attached. For instance:

```csharp
bool sample = !(1 < 2);
```

One is less than two. However, since "!" is attached to the Boolean expression, the result will be reversed. That means this expression evaluates to "false".
