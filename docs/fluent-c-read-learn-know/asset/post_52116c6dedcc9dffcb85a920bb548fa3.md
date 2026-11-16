
## MATH CLASS

We've seen that all of the numeric types support the basic arithmetic operators, and that the Decimal type exposes some functions that are useful for financial calculations. The .NET Framework also has a class that exposes static methods and a couple of static fields that you can use to perform more advanced calculations.

We've seen a few static members before, but just to remind you: Because the members of the Math class are static, you don't need to instantiate it; you can simply call these methods using the name of the class: Math.PI.

Most of the methods of the Math class are moderately advanced mathematical functions like Log10(), which returns the logarithm base 10 of the provided number, and Cosh(), which returns the hyperbolic cosine. I'm going to assume that if you need one of these functions, you'll know how to use it. But Math also provides a couple of methods that are generally useful when you're comparing numeric values.

Max() and its partner Min() return the greater or lesser of two values. They can save some typing and processing time:

```
a = Max(x, y);
```

IS EQUIVALENT TO

```
if (x > y)
 a = x;
 else
 a = y;
```

The Math class also exposes the same four Round() methods that are exposed by the Decimal type. There are overloads for Decimal and Double types, while its partner the Truncate() method, which is also overloaded to accept either a Decimal or a Double, simply discards the fractional portion of the number, without rounding.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_337_0.png)

## REVIEW

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_338_0.png)

What .NET Framework type should you use to represent each of the following types of numeric data, unless you have a good reason not to?

- Whole Numbers
- Real Numbers
- Currency

In what class would you look for a static method to perform an advanced mathematical function?

List three reasons you should avoid using unsigned numeric types if possible:

## CHARACTER DATA

Except for a few idiosyncrasies, numeric data is represented and manipulated in C# and the .NET Framework more or less like it's represented and handled in the real world.

The same can't be said for character data. As you probably know, computers store data as zeros or ones. (Actually, they store data in a bunch of tiny little capacitors, but we think of them as zeros and ones.) In order to represent an alphabet, the individual characters must be ENCODED.

In the .NET Framework, characters are encoded using the Unicode standard, which has replaced the older ASCII encoding as an industry standard. The basic units of encoding character data in the .NET Framework are System.Char (most people pronounce this as “char” like burnt wood, not “care” like “character”), which represents a single character, and System.String, which represents an array of characters. (We’ll discuss the Array type in the next chapter. It’s the most basic of a group of classes that allow you to treat zero or more instances of an object as a single entity.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_339_0.png)

## PUT ON YOUR THINKING HAT

The System.Char structure exposes a large set of static and instance methods for manipulating characters. Using the Object Browser, can you write the statements and method calls that perform the following operations? (Remember, you can press F1 while a method name is selected to get more information about it.)

- Create an instance of a Char named MyChar and set its value to ‘x’:
- Determine whether MyChar contains a digit:
- Convert MyChar into a lowercase letter:
- Determine whether Char1 or Char2 comes first in the alphabet:

## HOW'D YOU DO?

In C#, character literals are delimited by single quote characters. Be careful not to use the double quote (") because that makes your character a String.

Create an instance of Char called MyChar and set its value to 'x'

```
Char MyChar = 'x';
```

Determine whether MyChar contains a digit

```
Char.IsDigit(MyChar)
```

Because IsDigit() and ToLower() are static methods, you call them on the class itself, not the instance.

Convert MyChar into a lowercase letter

```
Char.ToLower(MyChar)
```

Determine whether Char1 or Char2 comes first in the alphabet

```
Char1.CompareTo(Char2)
```

You could also have written this as Char2.CompareTo(Char1)

CompareTo() is an instance method, so you use normal method syntax rather than calling the method on the class.

## MAKE A NOTE

A Char represents a single logical character, but you should be aware that a single logical character might map to more than one Unicode character, characters, for example, require two characters. This is primarily an issue when you need to compare characters from different languages. If this applies to you, you'll find lots of useful example on MSDN. Search for 'Unicode'.

## STRINGS

In the computer world, a sequence of characters is called a String. (Think “string of beads” not “piece of string” and that might make more sense to you.) In the .NET Framework, they’re represented by the System.String structure. Like any value type, you can instantiate a String directly or by calling one of its constructors.

```
String MyString = "Hello";
```

Make sure to use double quotes here. Single quotes delimit a Char, not a String. If you use them, the code will work, but it will call an extra (unnecessary) conversion operation.

Notice the single quotes: this one is a Char.

```
String MyString = new String('a', 10);
```

The String structure has 8 different constructors that allow you to instantiate it in different ways. This one creates a String that duplicates the character argument the specified number of times, so in the case, MyString will contain “aaaaaaaaaa”.

## ESCAPING TEXT

Sometimes you need a String to contain characters that either can’t be entered directly, like a tab or a new line, or that have special meaning, like a backslash (\) or the double-quote character ("). In order to do so, you have to ESCAPE the characters, that is, tell the compiler to treat them as characters, not C# symbols.

There are two ways to escape characters in C#. You can escape a single character by preceding it with a backslash. So, for example, to create a String that contains the text: John said, “My Documents\Files\", you’d use the following statement:

```
String MyString = "John said, \"My Documents\\Files\\\";
```

In some situations, you can put an @ sign (“@”) in front of the whole string, but this doesn’t work to escape the double-quote character:

```
String MyString = @"My Documents\Files\";
```

For non-printing characters like a tab or new line, you can use one of the escape literals:

- \t .tab
- \r return
- \n .new line
- \b backspace

## COMPARING STRINGS

The value of a String is the text it contains, and in most cases comparisons work exactly as you'd expect them to:

```csharp
String String1 = "Hello";
String String2 = "Hello";
Boolean TheSame = (String1 == String2);
```

The variable TheSame here will be true.

But what if string1 contains “Hello” and String2 contains “hello”? Are they equal?
By default, the answer is no, because the String structure performs an ordinal string
operation, which means, in effect, that it compares the numeric values of each char in
the string. You may have noticed that Windows Explorer sorts “File 20” before “File 5”.
That’s because it does an ordinal comparison, and “2” is less than “5”.

But the String structure exposes overloads of most of its methods that accept a member
of the StringComparison enumeration as a parameter. The StringComparison enumeration
allows you to specify precisely what you want to have happen, and best practice dictates
that you should always use one of these overloads, just to make your intentions perfectly
clear. The StringComparison enumeration contains the following members:

| Member | Description |
| :--- | :--- |
| CurrentCulture | Performs case-sensitive operations based on the culture set in Windows |
| CurrentCultureIgnoreCase | Performs case-insensitive operations based on the culture set in Windows |
| InvariantCulture | Performs case-sensitive operations using an invariant culture |
| InvariantCultureIgnoreCase | Performs case-insensitive operations using an invariant culture |
| Ordinal | Performs case-sensitive ordinal operations |
| OrdinalIgnoreCase | Performs case-insensitive ordinal operations |

```csharp
Boolean TheSame = String1.Equals(String2,
StringComparison.InvariantCultureIgnoreCase);
```
