To throw an exception, you simply prefix the exception instance with the keyword `throw`. The type of exception used is obviously the type that best describes the circumstances surrounding the error that caused the exception.

For example, consider the `TextNumberParser.Parse()` method in Listing 11.1.

# **LISTING 11.1: Throwing an Exception**

```
public sealed class TextNumberParser
{
    public static int Parse(string textDigit)
    {
        string[] digitTexts =
            { "zero", "one", "two", "three", "four",
              "five", "six", "seven", "eight", "nine" };

        int result = Array.IndexOf(
            digitTexts,
            // Leveraging C# 2.0's null coalesce operator
            textDigit??
            // Leveraging C# 7.0's throw expression
            throw new ArgumentNullException(nameof(textDigit)))
            .ToLower());
        if (result < 0)
        {
            // Leveraging C# 6.0's nameof operator
            throw new ArgumentException(
                "The argument did not represent a digit",
                nameof(textDigit));
        }

        return result;
    }
}
```

In the call to `Array.IndexOf()`, we leverage a C# 7.0 throw expression when the `textDigit` argument is null. Prior to C# 7.0, throw expressions were not allowed; only throw statements were allowed. As a result, two separate statements were required: one checking for null and the other to throw the exception. You could not embed the throw within the same statement as a null coalescing operator, for example.

Instead of throwing `System.Exception`, it is more appropriate to throw `ArgumentException` because the type itself indicates what went wrong and includes special parameters for identifying which parameter was at fault.