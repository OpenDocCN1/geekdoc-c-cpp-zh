
# VB.NET

Dim roles As New List(Of String)

```
roles.Add("Administrators")
roles.Add("ContentManagers")
roles.Add("Members")
```

# C#

```
List<string> roles = new List<string>();

roles.Add("Administrators")
roles.Add("ContentManagers")
roles.Add("Members")
```

Not much has changed to make the roles list type safe. However, with the definition of List (Of String) in VB.NET and List<string> in C# the new list is set up to allow only strings to be added through its Add method. This compiles free:

```
roles.Add("Administrators")
```

The following will not compile because 33 is not a string:

```
roles.Add(33)
```

Similar to the generics of strings, you can also create lists to hold other types. For example:

# VB.NET

```
Dim intList As New List(Of Integer)
Dim boolList As New List(Of Boolean)
Dim buttonList As New List(Of Button)
```

# C#

```
List<int> intList = new List<int>();
List<bool> boolList = new List<bool>();
List<Button> buttonList = new List<Button>();
```

> NOTE Because there's a lot to generics than what is shown here, they deserve an entire book on their own. Wrox has written such a book: Professional .NET 2.0 Generics by Tod Goldman (2005; ISBN: 978-0-7645-5984). Although it was originally written for .NET 2.0, you'll find that all the concepts and examples in that book still apply.

Though the Add method is used to add items to a collection, it can be a bit tedious. To make easier, .NET supports collection initializers. With a collection initializer, you declare the collection and add some items in one step. You do this by adding the items in a pair of curly braces (prefixed with the keyword From in VB.NET) as shown in the following example:

# VB.NET

```
Dim myList As New List(Of Integer) From {1, 2, 3, 4, 5}
```

# C#

```
List<int> myList = new List<int>() { 1, 2, 3, 4, 5 };
```

Right after this line, the list is populated with the five integers.

Collection initializers are not limited to the List class or integers. You can use them with other collection types and data types as.

The generics examples you have barely scratch the surface of what is possible with generics. However, when building ASP.NET websites, you often don't need all the advanced stuff that generics offers. The List collection is so useful it had to be discussed here. Without a doubt, you'll use that collection in your own code in one way or another.

# STATEMENTS

To make a program or to do something useful, you need to provide it with code statements that it can execute. Statements cover a wide range of actions, as show this button, send this e-mail, executing this code and when a user clicks that, and so on. However, simply executing these is not enough. You often need to execute some code when a certain condition is true. For example, if a visitor to an e-commerce website is buying more than $100 worth of merchandise at one time, she might get a discount of 10 percent. Otherwise, she'll pay the full price. Conditions or decisions are very important statements in a programming language. Another important set of statements is the loops. Loops enable you to repeat a certain piece of code on iteration. For example, you can have a loop that goes from 1 to 10, performing some action on each iteration. Or you can loop through the products in a shopping cart, summing up their total price, for example.

The final important set of statements is the operators. Operators enable you to do something with your values; or, to be more exact, they enable you to operate on them. For example, you use operators to add or subtract values, concatenate (combine) them, or compare to each other.

The following three sections dig deeper into operators, decision making, and loops.

# Operators

The most important operators can be grouped logically into five different types; these types are covered in this section. Of these five types, the assignment operators are probably the easiest to understand and use.

# Assignment Operators

The assignment operators are used to assign a value to a variable. This value can come from many sources: a constant value, the number 6, the value of another variable, or the result of an expression or a function, which are discussed later. In its simplest form, an assignment operator looks like this, where the number 42 is assigned to the age variable:

```
VB.NET
```

```
Dim age As Integer = 42
```

# C#

```
int age = 42;
```

What if the person this age variable is referring to just had his birthday? You'd need to add 1 to the age value. That's where arithmetic operators come into play.

# Arithmetic Operators

Arithmetic operators enable you to perform most of the familiar calculations on variables and values, like adding, subtracting, and dividing. The following table lists the common arithmetic operators for both VB.NET and C#.

| VB.NET | C# | USAGE |
|---|---|---|
| + | + | Adds two values to each other |
| - | - | Subtracts one value from another |
| * | * | Multiplies two values |
| / | / | Divides two values |
| \ | n/a | Divides two values but always returns a rounded integer |
| ^ | n/a | Raises one value to the power of another |
| Mod | % | Divides two numbers and returns the remainder |

The first four operators probably look familiar, and their usage is pretty straightforward. The following code snippet shows the operations you can perform with these operators:

# VB.NET

```
Dim firstNumber As Integer = 100
Dim secondNumber As Single = 23.5
Dim result As Double = 0
```

```
result = firstNumber + secondNumber      // Results in 123.5
result = firstNumber - secondNumber      // Results in 76.5
result = firstNumber * secondNumber      // Results in 2350
result = firstNumber / secondNumber      // Results in 4.25531914893617
```

# C#

```
int firstNumber = 100;
float secondNumber = 23.5;
double result = 0;
```

```
result = firstNumber + secondNumber;      // Results in 123.5
result = firstNumber - secondNumber;      // Results in 76.5
result = firstNumber * secondNumber;      // Results in 2350
result = firstNumber / secondNumber;      // Results in 4.25531914893617
```

Note that in the C# example you need to add the letter F to the value of 23.5. This tells the compiler you really want it to be a float than a double.

VB.NET supports the \ operator, which basically performs the division and then drops the remainder from the value, effectively rounding the return value down to the nearest integer:

# VB.NET

```
result = firstNumber \ secondNumber   ' Results in 4
```

C# doesn't have a special operator for this. However, when you try to divide two integers, the result is always an integer as well. This means 7 (stored as an int) divided by 2 (stored as an int) will be 3. It's important to realize that this rounding occurs, or you may end up with unexpected results.

The two operators need a bit more explanation. First, the ^ operator — for raising one number to the power of another — is available only in the VB.NET language:

# VB.NET

Dim result As Double

```
result = 2 ^ 3   ' Results in 8 (2 * 2 * 2)
result = 3 ^ 2   ' Results in 9 (3 * 3)
```

C# doesn't support this operator, but you can easily replicate its behavior using Math.Pow, which is made available by the .NET Framework. The following code snippet is equivalent to the preceding one:

# C#

```
result = Math.Pow(2, 3);   // Results in 8 (2 * 2 * 2)
result = Math.Pow(3, 2);   // Results in 9 (3 * 3)
```

Of course Math.Pow is available to VB.NET as well, so if you're using that language, you have two options to choose from:

The final operator is called the modulus operator. It returns the remainder of the division of two numbers, like:

# VB.NET

```
Dim firstNumber As Integer = 17
Dim secondNumber As Integer = 3
Dim result As Integer = firstNumber % secondNumber   ' Results in 2
```

# C#

```
int firstNumber = 17;
int secondNumber = 3;
int result = firstNumber % secondNumber;   // Results in 2
```

Simply put, the modulus operator to subtract the second number from the first as many times as possible and then returns the remainder. The preceding example will succeed five times, subtracting a total of 15, leaving a remainder of 2, which is returned and stored in the result. The modulus operator is often used to determine if a number is odd or even.

When working with operators, it's important to keep their precedence in mind. To see why this is important, consider the following calculation:

```
2 + 10 * 4
```
