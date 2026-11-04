```
```csharp
// RemoveWhitespace -- The RemoveSpecialChars method removes every
// occurrence of the specified characters from the string.
// Note: The rest of the program is not shown here.
public static string RemoveSpecialChars(string input, char[] targets)
{
    // Split the input string up using the target
    // characters as the delimiters.
    string[] substrings = input.Split(targets);

    // output will contain the eventual output information.
    string output = "";

    // Loop through the substrings originating from the split.
    foreach(string substring in substrings)
    {
        output = String.Concat(output, substring);
    }
    return output;
}
```
```

This version uses the `Split()` method to break the input string into a set of substrings, using the characters to be removed as delimiters. The delimiter is not included in the substrings created, which has the effect of removing the character(s). The logic here is much simpler and less error-prone.

The `foreach` loop in the second half of the program puts the pieces back together again using `Concat()`. The output from the program is unchanged.

Pulling the code out into a method further simplifies it and makes it clearer.

# Formatting Your Strings Precisely

The String class also provides the `Format()` method for formatting output, especially the output of numbers. In its simplest form, `Format()` allows the insertion of string, numeric, or Boolean input in the middle of a format string. For example, consider this call:

```
```csharp
string myString = String.Format("{0} times {1} equals {2}", 2, 5, 25);
```
```

The first argument to `Format()` is known as the format string — the quoted string you see. The `{n}` items in the middle of the format string indicate that the nth argument following the format string is to be inserted at that point. `{0}` refers to the first argument (in this case, the value 2), `{1}` refers to the next (that is, 5), and so on.

This returns a string, myString. The resulting string is

```
```text
"2 times 5 equals 10"
```
```