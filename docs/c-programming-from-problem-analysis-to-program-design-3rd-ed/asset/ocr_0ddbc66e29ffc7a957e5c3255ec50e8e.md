comments, they do not have to span more than one line. Unlike the single-line comment that terminates at the end of the current line when the Enter key is pressed, the multiline comment requires special characters /* and */ to begin and terminate the comment, even if the comment just appears on a single line. Example 1-2 shows an example of a multiline comment.

# Example 1-2

```
/* This is the beginning of a multiline (block) comment. It can go on for several lines or just be on a single line. No additional symbols are needed after the beginning two characters. Notice there is no space placed between the two characters. To end the comment, use the following symbols. */
```

C# does not allow you to nest multiline comments. In other words, you cannot place a block comment inside another block comment. The outermost comment is ended at the same time as the inner comment—as soon as the first */ is typed.

# XML Documentation Comments

A third type of comment uses three forward slashes ///. This is an advanced documentation technique used for XML-style comments. XML (Extensible Markup Language) is a markup language that provides a format for describing data using tags similar to HTML tags. A C# compiler reads the XML documentation comments and generates XML documentation from them.

You will be using the inline // and multiline /* */ comments for the applications you will develop in this book.

# Using Directive

The following statement that appears in Example 1-1, Line 2 permits the use of classes found in the System namespace without having to qualify them with the word "System". This reduces the amount of typing that would be necessary without the directive.

```
Line 2 using System;
```

Using .NET provides the significant benefit of making available more than 2000 classes that make up what is called the Framework class library (FCL). A class contains code that can be reused, which makes programming easier and faster because you don't have to reinvent the wheel for common types of operations. The Framework classes are all available for use by any of the .NET-supported languages, including C#.

Keywords after they are introduced, such as class, are displayed in blue throughout this book. Keywords are words reserved by the system and have special, predefined meanings. The keyword class, for instance, defines or references a C# class.