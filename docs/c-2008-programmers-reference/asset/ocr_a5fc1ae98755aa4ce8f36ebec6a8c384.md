# Part I: C# Fundamentals

> > By default, when you use the \n to insert a new line, the cursor is automatically returned to the beginning of the line. However, some legacy applications still require you to insert newline and carriage return characters in strings.

![](bbox=[0.376, 0.208, 0.552, 0.31])

The following table summarizes the different escape sequences you have seen in this section:

| Sequence | Purpose |
| --- | --- |
| \n | New line |
| \r | Carriage return |
| \r\n | Carriage return, New line |
| \" | Quotation marks |
| \\ | Backslash character |
| \t | Tab |

In C# strings can also be @-quoted. Earlier, you saw that to include special characters (such as double-quote, backslash, and so on) in a string you need to use the backslash character to turn off its special meaning:

```
```csharp
string path="C:\\Windows";
```
```

You can actually use the @ character, and prefix the string with it, like this:

```
```csharp
string path=@"C:\Windows";
```
```

Using the @ character makes your string easier to read. Basically, the compiler treats strings that are prefixed with the @ character verbatim — that is, it just accepts all the characters in the string (inside the quotes). To better appreciate this, consider the following example where a string containing an XML snippet is split across multiple lines (with each line ending with a carriage return):

```
```csharp
string XML = @"
    <Books>
        <title>C# 3.0 Programmers' Reference</title>
    </Books>";
Console.WriteLine(XML);
```
```