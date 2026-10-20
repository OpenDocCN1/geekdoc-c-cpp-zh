
## How to work with nullable reference types

In chapter 4, you learned how to declare and work with value types that can contain null values. Because reference types can contain null values by default, you don’t have to use any special techniques to work with them like you do value types. However, C# 8.0 introduced a new feature called nullable reference types that lets you change the default for reference types to be non-nullable. That way, you can be sure when you refer to a reference type that it doesn’t contain a null value.

Before you can use the nullable reference types feature, you have to enable it. In most cases, you’ll want to enable it for an entire project. To do that, you can use the procedure shown at the top of figure 9-9.

You can also enable nullable reference types for an individual file. To do that, you have to add a #nullable preprocessor directive at the beginning of the file like the one shown in the first example. A preprocessor directive provides conditional information to the compiler that determines how a file is compiled.

Although the default for reference types is for them to be non-nullable when you enable nullable reference types, you’ll still want to use reference types that can contain null values in some cases. To declare a reference type that can contain a null value, you code a question mark (?) after the type as shown by the first statement in the second example. This works the same as it does for nullable value types.

When you enable nullable reference types, the compiler will display warnings when you use nullable and non-nullable variables incorrectly. If, for example, you try to get the length of a nullable variable as shown in the second statement and the compiler can’t determine that you’ve assigned a non-null value to that variable, it will display a warning that the variable may be null. This figure lists other common situations when warnings are displayed. These warnings are intended to help you identify problem areas in your code so you can fix them. For example, before you get the length of a variable that may contain a null value, you should check to be sure it isn’t null as shown in the third statement. This is true regardless of whether the nullable reference types feature is enabled.

In some cases, the compiler won’t be able to tell whether or not a nullable variable might contain a null value, and it will display a warning. If you’re sure that the variable won’t contain a null value, though, you can suppress the warning. To do that, you code an exclamation mark (!) after the name of the variable as shown in the fourth statement.

Although the code in the rest of this book assumes that nullable reference types haven’t been enabled, you should realize that this is an important new feature of C#. Because of that, you should experiment with it when you get a chance. To help you get started with that, you’ll use nullable reference types in one of the exercises at the end of this chapter.

## How to enable nullable reference types at the project level
- 1. In the Solution Explorer, right-click on the project name and select Properties.
- 2. Select the Build Category.
- 3. From the Nullable drop-down list, select Enable.

## How to enable nullable reference types at the file level

```csharp
#nullable enable
using System.Windows.Forms;
.
.
.
```

## How to work with nullable reference types

```csharp
string? message = null;             // declare a nullable reference type
int length = message.Length;         // message may be null warning
if (message != null)                 // check that the message isn't null
    int length = message.Length;
int length = message!.Length;        // stop compiler from displaying warning
```

## Common situations when warnings are displayed
- When you assign or pass a null value to a non-nullable reference type.
- When you assign or pass a nullable reference type to a non-nullable one.
- When you refer to a nullable reference type that may be null.
- When a non-nullable field of a new object isn’t initialized to a non-null value.

## Description
- By default, reference types can contain null values. If that’s not what you want, you can enable *nullable reference types* at the project or file level as shown above. This feature is available only with .NET Core 3.0 and later.
- If you enable nullable reference types, you have to explicitly identify reference types that can contain null values. To do that, you code a question mark (?) immediately after the keyword for the type just like you do for value types.
- When you use nullable reference types, the compiler tries to determine when nullable and non-nullable variables are used incorrectly and then displays a warning.
- If a warning is displayed indicating that a nullable variable may contain a null value and you’re sure it won’t, you can code an exclamation mark (!) after the variable name to keep the warning from being displayed.
- Before referring to a nullable variable, you should check that it doesn’t contain a null value.

## How to use the StringBuilder class

When you use the String class to create a string, the string has a fixed length and value. In other words, the String class creates strings that are *immutable*. Then, when you assign a new value to a string variable, the original String object is deleted and it’s replaced with a new String object that contains the new value.

Another way to work with strings, though, is to use the StringBuilder class. Then, you create StringBuilder objects that are *mutable* so you can add, delete, or replace characters in the objects. This makes it easier to write some types of string-handling routines, and these routines run more efficiently. As a result, you should use the StringBuilder class for string-handling routines that append, insert, remove, or replace characters in strings, especially if you’re working with long strings that use significant system resources.

In figure 9-10, you can see some of the most useful properties and methods for working with a string that’s created from the StringBuilder class. As you can see, you can use an index to refer to a character in a StringBuilder object, and you can use the Length property to get the number of characters in a string just as you can with a String object. You can also use the Insert(), Remove(), and Replace() methods with StringBuilder objects. However, instead of returning a new string, these methods change the existing string.

When you create a StringBuilder object, you can code one or two arguments that assign an initial value, an initial capacity, or both. The statements in the first example illustrate how this works. Here, the first statement doesn’t include any arguments, so the StringBuilder object is created with a default capacity of 16 characters and an initial value of an empty string. The second statement creates a StringBuilder object with an initial capacity of 10. The third and fourth statements are similar, but they specify an initial value for the object.

The second example in this figure shows how you can use five methods of the StringBuilder class. Here, the first statement creates a StringBuilder object with an initial capacity of 10, and the second statement appends a 10-character phone number to the object. The third and fourth statements insert periods into the string to format the number. The fifth statement removes the area code and the period that follows it. The sixth statement replaces the remaining period with a hyphen. And the last statement converts the characters stored in the StringBuilder object to a string.

This example also shows how a StringBuilder object automatically increases its capacity when necessary. Here, the StringBuilder object has a capacity of 10 when it’s created, and this capacity remains at 10 until the first period is inserted. Then, to be able to store the 11 characters, the StringBuilder object automatically doubles its capacity to 20.
