> NOTE
> C# does not allow you to nest multiline comments. In other words, you cannot place a block comment inside another block comment. The outermost comment is ended at the same time as the inner comment as soon as the first */ is typed.

# XML Documentation Comments

A third type of comment uses three forward slashes // /. This is an advanced documentation technique used for XML-style comments. XML (Extensible Markup Language) is a markup language that provides a format for describing data using tags similar to HTML tags. A C# compiler reads the XML documentation comments and generates XML documentation from them.

You will be using the inline // and multiline /* */ comments for the applications you will develop in this book.

# Using Directive

The following statement that appears in Example 1-1, Line 2 permits the use of classes found in the System namespace without having to qualify them with the word "System." This reduces the amount of typing that would be necessary without the directive.

```
Line2 using System;
```

Using .NET provides the significant benefit of making available more than 2000 classes that make up what is called the Framework class library (FCL). A class contains code that can be reused, which makes programming easier and faster because you don't have to reinvent the wheel for common types of operations. The Framework classes are all available for use by any of the .NET-supported languages, including C#.

> NOTE
> Keywords after they are introduced, such as class, are displayed in blue throughout this book. Keywords are words reserved by the system and have special, predefined meanings. The keyword class, for instance, defines or references a C# class.

With several thousand .NET Framework classes, it is very unlikely that program developers will memorize the names of all of the classes, let alone the additional names of members of the classes. As you could well imagine, it would be easy for you to use a name in your own application that has already been used in one or more of the Framework classes. Another likely occurrence is that one or more of these Framework classes could use the same name. How would you know which class was being referenced? .NET eliminates this potential problem by using namespaces.