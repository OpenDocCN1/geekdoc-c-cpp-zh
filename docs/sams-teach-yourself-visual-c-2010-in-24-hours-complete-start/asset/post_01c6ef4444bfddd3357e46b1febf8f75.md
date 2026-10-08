
- Trimming and padding strings
- Creating substrings, concatenating strings, and splitting strings based on specific characters
- Removing and replacing characters
- Performing string containment and comparison operations
- Converting string case

**Q. What is the benefit of the StringBuilder class?**

**A.** The StringBuilder class enables you to create and manipulate a string that is mutable and is most often used for string concatenation inside a loop.

**Q. What are regular expressions?**

**A.** Regular expressions are a pattern that describes a set of strings that are optimized for text manipulation.

## Workshop

### Quiz

1. What is string interning and why is it used?
2. Using a verbatim string literal, must an embedded double-quote character be escaped?
3. What is the recommended way to test for an empty string?
4. What is the difference between the `IndexOf` and `IndexOfAny` methods?
5. Do any of the string manipulation functions result in a new string being created?
6. What will the output of the following statement be and why?
```csharp
int i = 10;
Console.WriteLine(i.ToString("P"));
```
7. What will the output of the following statement be and why?
```csharp
DateTime today = new DateTime(2009, 8, 23);
Console.WriteLine(today.ToString("MMMM"));
```
8. What will the output of the following Console.WriteLine statements be?
```csharp
Console.WriteLine("{0}", 10);
Console.WriteLine("{0, 3}", 10);
Console.WriteLine("{0: d4}", 10);
```
```csharp
int a = 24;
int b = -24;

Console.WriteLine(a.ToString("##(##)"));
Console.WriteLine(b.ToString("##(##)"));
```
9. What is the benefit of using a `StringBuilder` for string concatenation inside a loop?
10. What does the following regular expression pattern mean?
```
[\\w-]+@([\\w-]+\.|)+(\\w-)+
```

# Answers

1. String interning is used by the C# compiler to eliminate duplicate string literals to save space at runtime.
2. The double-quote character is the only character that must be escaped using a verbatim string literal so that the compiler can determine where the string ends.
3. The recommended way to test for an empty string is to use the static `String.IsNullOrEmpty` method.
4. The `IndexOf` method reports the index of the first occurrence found of a single character or string, whereas the `IndexOfAny` method reports the first occurrence found of any character in a set of characters.
5. Yes, because strings are immutable, all the string manipulation functions result in a new string being created.
6. The output will be "1,000.00 %" because the "P" numeric format specifier results in the number being multiplied by 100 and displayed with a percent symbol.
7. The "MMMM" custom date and time format specifier represents the full name of the month, so the output will be "August".
8. The output will be as follows:
   ```text
   10
     10
   0010
   24
   (24)
   ```
9. Because the `StringBuilder` represents a mutable string, using it for string concatenation inside a loop prevents multiple temporary strings from being created during each iteration to perform the concatenation.
10. This is a simple regular expression for parsing a string as an email address. Broken down, it means "Match any word character one or more times followed by the @ character followed by a group containing any word character one or more times followed by a period (.) character, where that group is repeated one or more times, followed by any word character one or more times."

# Exercises

1. Add a read-only string property to the `Contact` class of the `AddressBook` project named `DisplayAs`. The `get` accessor should use `String.Format` to return the `FirstName` and `LastName` properties in the order indicated by the `DisplayStyle` property.
2. Override the `ToString` method on `PhoneNumber` to return a properly formatted phone number using a `StringBuilder`. If the `CountryCode` or `Extension` properties do not have valid values, they should be excluded. (Any nonzero value for `CountryCode` is valid and any nonempty string value for `Extension` is valid.)
3. Implement a `Validate` method on `PhoneNumber` that uses the static `RegEx.IsMatch` method to validate the phone number. Use the result of calling `this.ToString` as the input value for the `IsMatch` method. The regular expression pattern should look like:
   ```
   ^(\+[2-9]\d{3})? \d{7}( \d{4})? [2-9]\d{2}-\d{4}$
   ```

<!-- This page intentionally left blank -->

# HOUR 9
## Working with Arrays and Collections

**What You’ll Learn in This Hour:**

- Single and Multidimensional Arrays
- Jagged Arrays
- Array Indexing
- Array Initialization
- Indexers
- Collections
- Collection Interfaces
- Collection Initializers

The majority of problems solved by computer programs involve working with large amounts of data. Sometimes there is a lot of individual and unrelated datum, but many times, there are large amounts of related datum. C# provides a rich set of collection types that enable you to manage large amounts of data.

An array is the simplest type of collection and is the only one that has direct language support. Although the other collection types offer more flexibility than arrays, including the ability to create your own specialized collections, they are generally used in similar ways.

Over the next hour, you learn to work with different types of arrays, including multi-dimensional and jagged arrays. When you understand how to work with arrays, you move to using some of the different collection classes provided by the .NET Framework, in which there are more than 40 different classes, base classes, and interfaces.

# Arrays

An array is a numerically indexed collection of objects that are all the same type. Although C# provides direct language support for creating arrays, the common type system means that you are implicitly creating a type of System.Array. As a result, arrays in C# are reference types, and the memory allocated to refer to the array itself is allocated on the managed heap. However, the elements of the array, which are the individual items contained in the array, are allocated based on their own type.

In its simplest form, the declaration of a variable of array type looks like:

`type[] identifier;`

## By the Way

### Arrays

Arrays in C# are different from arrays in C because they are actually objects of type System.Array. As a result, C# arrays provide the power and flexibility afforded by classes through properties and methods with the simple syntax offered by C style arrays.

The type indicates the type of each element that will be contained in the array. Because the type is declared only once, all the elements in the array must be of that same type. The square brackets are the **index operator** and tell the compiler that you are declaring an array of the given type; they are the only difference between an array declaration and a regular variable declaration. In contrast to other languages, such as C, the size of a dimension is specified when the array is instantiated rather than when it is declared.

To create an array that can contain five integer values, you can specify it like this:

`int[] array = new int[5];`

## Watch Out!

### Array Sizes

In C# the size of an array, obtained through the Length property, is the total number of elements in all the dimensions of the array, not the upper bound of the array. Because C# uses a zero-based indexing scheme for arrays, the first element in an array is at position 0. Therefore, the following statement declares an array of 5 elements with indices 0 through 4:

`int[] array = new int[5];`

The length of the array is 5, but the upper bound is 4.

This type of array declaration creates a single-dimensional rectangular array. The length of each row in a rectangular array must be the same size. This restriction results in a rectangular shape and is what gives rectangular arrays their name. To
