+   - Handling input from the command line
+   - Managing formatted output
+   - Working efficiently with strings using the `StringBuilder`

![](bbox=[0.122, 0.203, 0.217, 0.278])

In addition to the examples shown in the rest of this chapter, take a look at the `StringCaseChanging` and `VariousStringTechniques` examples on the Web site.

# Comparing Strings

It’s very common to need to compare two strings. For example, did the user input the expected value? Or maybe you have a list of strings and need to alphabetize them.

If all you need to know is whether two strings are equal (same length and same characters in the same order), you can use the `==` operator (or its inverse, `!=`, or *not equal*):

```
string a = "programming";
string b = "Programming";
if(a == b) ... // True if you don't consider case, false otherwise.
if(a != b) ... // False if you don't consider case, true otherwise.
```

But comparing two strings for anything but equality or inequality is another matter. It doesn’t work to say

```
if(a < b) ...
```

So if you need to ask, Is string A greater than string B? Or is string A less than string B?, you need another approach.

# Equality for all strings: The Compare( ) method

Numerous operations treat a string as a single object — for example, the `Compare( )` method. `Compare( )`, with the following properties, compares two strings as though they were numbers:

+   - If the left-hand string is *greater than* the right string, `Compare(left, right)` returns 1.
+   - If the left-hand string is *less than* the right string, it returns −1.
+   - If the two strings are equal, it returns 0.

The algorithm works as follows when written in *notational C#* (that is, C# without all the details, also known as *pseudocode*):