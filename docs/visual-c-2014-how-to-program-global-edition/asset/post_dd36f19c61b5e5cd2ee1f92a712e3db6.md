
# Chapter 16 Strings and Characters: A Deeper Look

```cs
34
35    Console.WriteLine("\n");
36    }
37 }
```

string1 = "hello there"
Length of string1: 11
The string reversed is: ereht olleh
The character array is: hello

**Fig. 16.2** string indexer, Length property and CopyTo method. (Part 2 of 2)

Line 16 uses string property to determine the number of characters in string1. Unlike arrays, strings always know their size.

Lines 21–24 demonstrate the characters of the string in reverse order using the string indexer ([1]), which treats string as an array of chars and returns the character at a specific index in the string. With arrays, the first element of a string has 0.

![](img/57baed2319be0bb1b5f98674846f2711_712_0.png)

> > Common Programming Error 16.1
> Accessing a character that is outside a string's bounds results in an OutOfRangeException.

Line 27 uses string CopyTo to copy the characters of string1 into an array (characterArray). The first argument given to CopyTo is the index from which the method begins copying characters in the string. The second argument is the array into which the characters are copied. The third argument is the index specifying the starting location at which the method begins placing the characters into the array. The last argument is the number of characters that the method will copy from the string. Lines 30–33 show the char array one character at a time.

We used a for loop for characters in lines 21-24 to demonstrate a string's Length property and the string indexer, using foreach to display the string. That loop could have been implemented with foreach and the Reverse extension method as in

```cs
foreach (var element in string1.Reverse())
{
    Console.WriteLine(element);
}
```

Reverse is one of many LINQ extension methods and requires a using directive for the namespace System.Linq.

## 16.5 Comparing strings

The next examples demonstrate various methods for comparing strings. To understand how one string can be "greater than" or "less than", consider the process of alphabetizing a series of names. The reader would, no doubt, place "Jones" before "Smith", because the first letter of "Jones" comes before the first letter of "Smith" in the alphabet. The alphabet is more than just a set of 26 letters—it’s an ordered list of characters in which each letter occurs in a specific position. For example, Z is more than just a letter of the alphabet; it's specifically the twenty-sixth letter of the alphabet. Computers can order characters alphabetically because they're represented internally as numeric codes and those codes are ordered according to the alphabet so, for example, 'a' is less than 'b'—see Appendix C.

**Comparing strings with Equals, CompareTo and the Equality Operator (==)**
Class string provides several ways to compare strings. Figure 16.3 demonstrates methods Equals() and CompareTo to the equality operator (==).

```cs
// Fig. 16.3: StringCompare
// Comparing strings
using System;
class StringCompare {
    static void Main() {
        var string1 = "hello";
        var string2 = "good bye";
        var string3 = "Happy Birthday";
        var string4 = "happy birthday";

        // output values of four strings
        Console.WriteLine($"{string1 = {string1}}" + $"string2 = {string2}" + $"string3 = {string3}" + $"string4 = {string4}");

        // test for equality using Equals method
        if (string1.Equals("hello")) {
            Console.WriteLine("string1 equals \"hello\"");
        } else {
            Console.WriteLine("string1 does not equal \"hello\"");
        }

        // test for equality == ==
        if (string1 == "hello") {
            Console.WriteLine("string1 equals \"hello\"");
        } else {
            Console.WriteLine("string1 does not equal \"hello\"");
        }

        // test for equality comparing case
        if (string.Equals(string3, string4)) // static method {
        }
    }
```

**Fig. 16.3** | Comparing strings. (Part I of 2.)

**

string1 = "hello"
string2 = "good bye"
string3 = "Happy Birthday"
string4 = "happy birthday"

string1 equals "hello"
string1 equals "hello"
string3 does not equal string4

string1.CompareTo(string2) is 1
string2.CompareTo(string1) is -1
string1.CompareTo(string1) is 0
string3.CompareTo(string4) is 1
string4.CompareTo(string3) is -1

Fig. 16.3 | Comparing strings. (Part 2 of 2.)

The condition in line 21 uses string Equals to compare string1 and literal "hello" (the argument) to determine whether they're equal. Method Equals (inherited from object and overridden in string) tests two strings for equality (i.e., checks the strings have identical contents). The method returns true if the objects are equal and false otherwise. In this case, the condition returns true, because string1 references string literal object "hello". Method Equals uses word sorting that do not depend on your system's currently culture. Comparing "hello" with HELLO would return false, because the lowercase letters are different from the correct uppercase letters.

The condition in line 31 uses string's overloaded equality operator (==) to compare string1 with the literal string "hello" for equality. In C#, the equality operator also compares the contents of two strings. Thus, the condition in the if statement evaluates to true, because the values of string1 and "hello" are equal.

Line 41 tests string3 and string4 equal to illustrate that comparisons are indeed case sensitive. Here, static method Equals is used to compare the values of two strings. "Happy Birthday" does not equal "happy birthday", so the comparison fails, and the message "string3 does not equal string4" is output (line 47).

Lines 51–60 use method CompareTo to compare strings. The method returns 0 if the strings are equal, a negative value if the string that CompareTo is less than the string that was passed as an argument and a positive value if the string that invokes CompareTo is greater than the string that passed as an argument.

Notice that CompareTo considers string3 to be greater than string4. The only difference between these two strings is that string3 contains two uppercase letters in positions where string4 contains lowercase letters. The sorting rules vary by culture and sensitive.

## Determining Whether a String Begins or Ends with a Specified String

Figure 16.4 tests whether a string begins or ends with a given string. Method StartWith determines whether a string starts with the string passed to the method as an argument. Method EndWith determines whether a string ends with the string passed to the method as an argument.

```cs
// Fig. 16.4: StringStartEnd.cs
// Demonstrating StartWith and EndWith methods.
using System;
class StringStartEnd
{
    static void Main()
{
        string[] strings = {"started"
```

Fig. 16.4 | Demonstrating StartWith and EndWith methods. (Part 1 of 2).

```cs
31 Console.WriteLine();
32 }
33 }
```

```
"started" starts with "st"
"starting" starts with "st"

"started" ends with "ed"
"ended" ends with "ed"
```

Fig. 16.4 | Demonstrating StartWith and EndWith methods. (Part 2 of 2)

## 16.6 Locating Characters and Substrings in strings

In many apps, it is necessary to search for a character or set of characters in a string. For example, a programmer creating a word processor would provide capabilities for searching through documents. Fig. 16.5 demonstrates various string methods like IndexOf, IndexOfAny, LastIndexOf and LastIndexOfAny, which search for a specific character or substring in a string. We perform all searches in this example on the string letters (9).

```cs
// Fig. 16.5: StringMethods.cs
// Searching for characters and substrings in strings
using System;
class StringIndexMethods
{
    static void Main()
{
        var letters = "abcdefghijklmnopqrstabcdefghijklijklm";
        char[] searchLetters = {'c', 'a', '$'};
        // test IndexOf to locate a character in a string
        Console.WriteLine("First 'c' is located at index " + 
            letters.IndexOf('c'));
        Console.WriteLine("First 'a' starting at 1 is located at index " + 
            letters.IndexOf('a', 1));
        Console.WriteLine("First '$' in the 5 positions starting at 3 " + 
            "$ is located at index " + letters.IndexOf('$', 3, 5));
    }
}
```

Fig. 16.5 | Searching for characters and substrings in strings. (Part 1 of 3).
