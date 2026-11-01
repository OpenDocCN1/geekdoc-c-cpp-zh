
## The FormattableVector Example

Now that you know how format strings are constructed, in this section you extend the Vector example from Chapter 7 so that you can format vectors in a variety of ways. You can download the code for this example from www.wrox.com; the filename is FormattableVector.cs. With your new knowledge of the principles involved now in hand, you will discover that the actual coding is quite simple. All you need to do is implement IFormattable and supply an implementation of the ToString() overload defined by that interface.

The format specifiers you are going to support are:

- **N** — Should be interpreted as a request to supply a quantity known as the Norm of the Vector. This is just the sum of squares of its components, which for mathematics buffs happens to be equal to the square of the length of the Vector, and is usually displayed between double vertical bars, like this: ||34.5||.
- **VE** — Should be interpreted as a request to display each component in scientific format, just as the specifier E applied to a double indicates (2.3E+01, 4.5E+02, 1.0E+00).
- **IJK** — Should be interpreted as a request to display the vector in the form 23i + 450j + 1k.
- Anything else should simply return the default representation of the Vector (23, 450, 1.0).

To keep things simple, you are not going to implement any option to display the vector in combined IJK and scientific format. However, you will make sure to test the specifier in a case-insensitive way, so that you allow ijk instead of IJK. Note that it is entirely up to you which strings you use to indicate the format specifiers.

To achieve this, you first modify the declaration of Vector so it implements IFormattable:

```csharp
struct Vector: IFormattable
{
    public double x, y, z;
    // Beginning part of Vector
}
```

Now you add your implementation of the two-parameter ToString() overload:

```csharp
public string ToString(string format, IFormatProvider formatProvider)
{
    if (format == null)
    {
        return ToString();
    }

    string formatUpper = format.ToUpper();

    switch (formatUpper)
    {
        case "N":
            return "|| " + Norm().ToString() + " ||";
        case "VE":
            return String.Format("{0:E}, {1:E}, {2:E}", x, y, z);
        case "IJK":
            StringBuilder sb = new StringBuilder(x.ToString(, 30));
            sb.AppendFormat(" i + ");
            sb.AppendFormat(y.ToString());
            sb.AppendFormat(" j + ");
            sb.AppendFormat(z.ToString());
            sb.AppendFormat(" k");
            return sb.ToString();
        default:
            return ToString();
    }
}
```

Microsoft ported it onto Windows, where up until now it has been used mostly with scripting languages. Today, regular expressions are supported by a number of .NET classes in the namespace `System.Text.RegularExpressions`. You can also find the use of regular expressions in various parts of the .NET Framework. For instance, you will find that they are used within the ASP.NET Validation server controls.

If you are not familiar with the regular expressions language, this section introduces both regular expressions and their related .NET classes. If you are already familiar with regular expressions, you will probably want to just skim through this section to pick out the references to the .NET base classes. You might like to know that the .NET regular expression engine is designed to be mostly compatible with Perl 5 regular expressions, although it has a few extra features.

## Introduction to Regular Expressions

The regular expressions language is designed specifically for string processing. It contains two features:

- A set of `escape codes` for identifying specific types of characters. You will be familiar with the use of the * character to represent any substring in DOS expressions. (For example, the DOS command `Dir Re*` lists the files with names beginning with `Re`.) Regular expressions use many sequences like this to represent items such as any one character, a word break, one optional character, and so on.
- A system for grouping parts of substrings and intermediate results during a search operation.

With regular expressions, you can perform quite sophisticated and high-level operations on strings. For example, you can:

- Identify (and perhaps either flag or remove) all repeated words in a string (for example, “The computer books books” to “The computer books”)
- Convert all words to title case (for example, “this is a Title” to “This Is A Title”)
- Convert all words longer than three characters to title case (for example, “this is a Title” to “This is a Title”)
- Ensure that sentences are properly capitalized
- Separate the various elements of a URI (for example, given `http://www.wrox.com`, extract the protocol, computer name, file name, and so on)

Of course, all these tasks can be performed in C# using the various methods on `System.String` and `System.Text.StringBuilder`. However, in some cases, this would require writing a fair amount of C# code. If you use regular expressions, this code can normally be compressed to just a couple of lines. Essentially, you instantiate a `System.Text.RegularExpressions.Regex` object (or, even simpler, invoke a static `Regex()` method), pass it the string to be processed, and pass in a regular expression (a string containing the instructions in the regular expressions language), and you’re done.

A regular expression string looks at first sight rather like a regular string, but interspersed with escape sequences and other characters that have a special meaning. For example, the sequence `\b` indicates the beginning or end of a word (a word boundary), so if you wanted to indicate you were looking for the characters th at the beginning of a word, you would search for the regular expression, `\bth` (that is, the sequence word boundary–t–h). If you wanted to search for all occurrences of th at the end of a word, you would write `th\b` (the sequence t–h–word boundary). However, regular expressions are much more sophisticated than that and include, for example, facilities to store portions of text that are found in a search operation. This section merely scratches the surface of the power of regular expressions.

![](img/d7d2ffa0a76feaab821930e95daace93_279_0.png)

Suppose your application needed to convert U.S. phone numbers to an international format. In the United States, the phone numbers have this format: 314-123-1234, which is often written as (314) 123-1234. When converting this national format to an international format you have to include +1 (the country code of the United States) and add brackets around the area code: +1 (314) 123-1234. As find-and-replace operations go, that is not too complicated. It would still require some coding effort if you were going to use the String class for this purpose (which would mean that you would have to write your code using the methods available from System.String). The regular expressions language allows you to construct a short string that achieves the same result.

This section is intended only as a very simple example, so it concentrates on searching strings to identify certain substrings, not on modifying them.

## The RegularExpressionsPlayaround Example

For the rest of this section, you develop a short example, called RegularExpressionsPlayaround, that illustrates some of the features of regular expressions and how to use the .NET regular expressions engine in C# by performing and displaying the results of some searches. The text you are going to use as your sample document is an introduction to a Wrox Press book on ASP.NET (Professional ASP.NET 4.0 in C# and VB, Wiley Publishing, 2010, ISBN 978-0-4705-0220-4).

```csharp
const string myText =
@"This comprehensive compendium provides a broad and thorough investigation of all
aspects of programming with ASP.NET. Entirely revised and updated for the fourth
release of .NET, this book will give you the information you need to
master ASP.NET and build a dynamic, successful, enterprise Web application.";
```

> This code is valid C# code, despite all the line breaks. It nicely illustrates the utility of verbatim strings that are prefixed by the @ symbol.

This text is referred to as the input string. To get your bearings and get used to the regular expressions of .NET classes, you start with a basic plain text search that does not feature any escape sequences or regular expression commands. Suppose that you want to find all occurrences of the string ion. This search string is referred to as the pattern. Using regular expressions and the Text variable declared previously, you could write this:

```csharp
const string pattern = "ion";
MatchCollection myMatches = Regex.Matches(myText, pattern,
    RegexOptions.IgnoreCase |
    RegexOptions.ExplicitCapture);

foreach (Match nextMatch in myMatches)
{
    Console.WriteLine(nextMatch.Index);
}
```

This code uses the static method Matches() of the Regex class in the System.Text.RegularExpressions namespace. This method takes as parameters some input text, a pattern, and a set of optional flags taken from the RegexOptions enumeration. In this case, you have specified that all searching should be case-insensitive. The other flag, ExplicitCapture, modifies the way that the match is collected in a way that, for your purposes, makes the search a bit more efficient — you see why this is later (although it does have other uses that we won't explore here). Matches() returns a reference to a MatchCollection object. A match is the technical term for the results of finding an instance of the pattern in the expression. It is represented by the class System.Text.RegularExpressions.Match. Therefore, you return a MatchCollection that contains all the matches, each represented by a Match object. In the preceding code, you simply iterate over the collection and use the Index property of the Match class, which returns the index in the input text of
