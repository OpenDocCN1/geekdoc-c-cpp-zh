
## Predefined Reference Types

C# supports two predefined reference types, `object` and `string`, described in the following table.

| Name | .NET Type | Description |
|---|---|---|
| `object` | System.Object | The root type. All other types (including value types) are derived from `object`. |
| `string` | System.String | Unicode character string |

## The object Type

Many programming languages and class hierarchies provide a root type, from which all other objects in the hierarchy are derived. C# and .NET are no exception. In C#, the `object` type is the ultimate parent type from which all other intrinsic and user-defined types are derived. This means that you can use the `object` type for two purposes:

- You can use an `object` reference to bind to an object of any particular subtype. For example, in Chapter 8, “Operators and Casts,” you see how you can use the `object` type to box a value object on the stack to move it to the heap; `object` references are also useful in reflection, when code must manipulate objects whose specific types are unknown.
- The `object` type implements a number of basic, general-purpose methods, which include `Equals`, `GetHashCode`, `GetType`, and `ToString`. Responsible user-defined classes might need to provide replacement implementations of some of these methods using an object-oriented technique known as *overriding*, which is discussed in Chapter 4, “Inheritance.” When you override `ToString`, for example, you equip your class with a method for intelligently providing a string representation of itself. If you don’t provide your own implementations for these methods in your classes, the compiler picks up the implementations in object, which might or might not be correct or sensible in the context of your classes.

You examine the object type in more detail in subsequent chapters.

## The string Type

C# recognizes the string keyword, which under the hood is translated to the .NET class, System.String. With it, operations like string concatenation and string copying are a snap:

```
string str1 ="Hello";
string str2 ="World";
string str3 = str1 + str2; // string concatenation
```

Despite this style of assignment, string is a reference type. Behind the scenes, a string object is allocated on the heap, not the stack; and when you assign one string variable to another string, you get two references to the same string in memory. However, string differs from the usual behavior for reference types. For example, strings are immutable.

Making changes to one of these strings creates an entirely new string object, leaving the other string unchanged. Consider the following code (code file StringSample/Program.cs):

```
using static System.Console;

class Program
{
    static void Main()
    {
        string s1 ="a string";
        string s2 = s1;
        WriteLine("s1 is " + s1);
        WriteLine("s2 is " + s2);
        s1 ="another string";
        WriteLine("s1 is now " + s1);
        WriteLine("s2 is now " + s2);
    }
}
```

The output from this is as follows:

```
s1 is a string
s2 is a string
s1 is now another string
s2 is now a string
```

Changing the value of s1 has no effect on s2, contrary to what you’d expect with a reference type! What’s happening here is that when s1 is initialized with the value a string, a new string object is allocated on the heap. When s2 is initialized, the reference points to this same object, so s2 also has the value a string. However, when you now change the value of s1, instead of replacing the original value, a new object is allocated on the heap for the new value. The s2 variable still points to the original object, so its value is unchanged. Under the hood, this happens as a result of operator overloading, a topic that is explored in Chapter 8. In general, the string class has been implemented so that its semantics follow what you would normally intuitively expect for a string.

String literals are enclosed in double quotation marks (`"`); if you attempt to enclose a string in single quotation marks, the compiler takes the value as a char and throws an error. C# strings can contain the same Unicode and hexadecimal escape sequences as chars. Because these escape sequences start with a backslash, you can’t use this character unescaped in a string. Instead, you need to escape it with two backslashes (`\\`):

```
string filepath ="C:\\ProCSharp\\First.cs";
```

Even if you are confident that you can remember to do this all the time, typing all those double backslashes can prove annoying. Fortunately, C# gives you an alternative. You can prefix a string literal with the at character (@) and all the characters after it are treated at face value; they aren’t interpreted as escape sequences:

```
string filepath = @"C:\ProCSharp\First.cs";
```

This even enables you to include line breaks in your string literals:

```
string jabberwocky = @"'Twas brillig and the slithy toves
Did gyre and gimble in the wabe.";
```

In this case, the value of jabberwocky would be this:

```
'Twas brillig and the slithy toves
Did gyre and gimble in the wabe.
```

C# 6 defines a new string interpolation format that is marked by using the $ prefix. You’ve previously seen this prefix in the section “Working with Variables.” You can change the earlier code snippet that demonstrated string concatenation to use the string interpolation format. Prefixing a string with $ enables you to put curly braces into the string that contains a variable—or even a code expression. The result of the variable or code expression is put into the string at the position of the curly braces:

```
public static void Main()
{
    string s1 ="a string";
    string s2 = s1;
    WriteLine($"s1 is {s1}");
    WriteLine($"s2 is {s2}");
    s1 ="another string";
    WriteLine($"s1 is now {s1}");
    WriteLine($"s2 is now {s2}");
}
```

> NOTE Strings and the features of string interpolation are covered in detail in Chapter 10, “Strings and Regular Expressions.”

## Controlling Program Flow

This section looks at the real nuts and bolts of the language: the statements that allow you to control the *flow* of your program rather than execute every line of code in the order it appears in the program.

### Conditional Statements

Conditional statements enable you to branch your code depending on whether certain conditions are met or what the value of an expression is. C# has two constructs for branching code: the `if` statement, which tests whether a specific condition is met, and the `switch` statement, which compares an expression with several different values.

### The if Statement

For conditional branching, C# inherits the C and C++ `if.else` construct. The syntax should be fairly intuitive for anyone who has done any programming with a procedural language:

```
if (condition)
    statement(s)
else
    statement(s)
```

If more than one statement is to be executed as part of either condition, these statements need to be joined into a block using curly braces ({ . }). (This also applies to other C# constructs where statements can be joined into a block, such as the `for` and `while` loops):

```
bool isZero;
if (i == 0)
{
    isZero = true;
    WriteLine("i is Zero");
}
else
{
    isZero = false;
    WriteLine("i is Non-zero");
}
```

If you want to, you can use an `if` statement without a final `else` statement. You can also combine `else if` clauses to test for multiple conditions (code file `IfStatement/Program.cs`):

```
using static System.Console;

namespace Wrox
{
    class Program
    {
        static void Main()
        {
            WriteLine("Type in a string");
            string input;
            input = ReadLine();
            if (input =="")
```
