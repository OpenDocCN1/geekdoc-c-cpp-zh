# How to declare and initialize a string

```
```csharp
string message1 = "Invalid data entry.";
string message2 = "";
string message3 = null;
```
```

# How to join strings

```
```csharp
string firstName = "Bob";                 // firstName is "Bob"
string lastName = "Smith";                // lastName is "Smith"
string name = firstName + " " + lastName;  // name is "Bob Smith"
```
```

# How to join a string and a number

```
```csharp
double price = 14.95;
string priceString = "Price: $" + price;   // priceString is "Price: $14.95"
```
```

# How to append one string to another string

```
```csharp
string firstName = "Bob";                 // firstName is "Bob"
string lastName = "Smith";                // lastName is "Smith"
string name = firstName + " ";             // name is "Bob "
name = name + lastName;                     // name is "Bob Smith"
```
```

# How to append one string to another with the += operator

```
```csharp
string firstName = "Bob";                 // firstName is "Bob"
string lastName = "Smith";                // lastName is "Smith"
string name = firstName + " ";             // name is "Bob "
name += lastName;                           // name is "Bob Smith"
```
```

# Description

+   - A *string* can consist of any characters in the character set including letters, numbers, and special characters like $, *, &, and #.
+   - To specify the value of a string, you can enclose text in double quotes. This is known as a *string literal*.
+   - To assign an *empty string* to a string, you can code a set of double quotes with nothing between them. This usually indicates that the value of the string is known, but the string doesn’t contain any characters.
+   - To assign a *null value* to a string, you can use the *null* keyword. This means that the value of the string is unknown.
+   - To join, or *concatenate*, a string with another string or a value data type, use a plus sign. If you concatenate a value data type to a string, C# will automatically convert the value to a string so it can be used as part of the string.
+   - When you *append* one string to another, you add one string to the end of another. To do that, you can use assignment statements.
+   - The += operator is a shortcut for appending a string expression to a string variable.