# Comparing Strings

+   * Handling input from the command line

+   * Managing formatted output

+   * Working efficiently with strings using the StringBuilder

In addition to the examples shown in the rest of this chapter, take a look at the StringCaseChanging and VariousStringTechniques examples on the Web site.

![](bbox=[0.147, 0.198, 0.219, 0.266])

# Comparing Strings

It's very common to compare two strings. For example, did the user input the expected value? Or maybe you have a list of strings and need to alphabetize them.

If you need to know whether two strings are equal (same length and same characters in the same order), you can use the == operator (or its inverse, != or not equal):

```
string a = "programming";nstring b = "Programming";nif(a == b) // True if you don't consider case, false otherwise.
if(a != b) // False if you don't consider case, true otherwise.
```

But comparing two strings for anything but equality or inequality is another matter. It doesn't work to say

```
if(a < b) ...
```

So you need to ask, Is A greater than string B? Or Is A less than string B?, you need another approach.

# Equality for all strings: The Compare() method

Numerous operations treat a string as a single object — for example, the Compare() method, with the following properties, compares two strings as though they were numbers:

+   * If the left-hand string is greater than the right string, Compare(left, right) returns 1.

+   * If the left string is less than the right string, it returns -1.

+   * If the two strings are equal, it returns 0.

The algorithm works as follows when written in notational C# (that is, C# without all the details, also known as pseudocode):