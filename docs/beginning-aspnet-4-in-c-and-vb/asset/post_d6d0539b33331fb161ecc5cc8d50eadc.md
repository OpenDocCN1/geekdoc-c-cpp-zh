
The following table lists some of the main special characters or escape sequences that you can use. It is not comprehensive, but a fuller list is available in the MSDN documentation.

| SYMBOL | MEANING | EXAMPLE | MATCHES |
|---|---|---|---|
| ^ | Beginning of input text | ^B | B, but only if first character in text |
| $ | End of input text | x$ | X, but only if last character in text |
| . | Any single character except the newline character (\n) | i.ation | isation, ization |
| * | Preceding character may be repeated zero or more times | ra*t | rt, rat, raat, raaat, and so on |
| + | Preceding character may be repeated one or more times | ra+t | rat, raat, raaaa and so on, but not rt |
| ? | Preceding character may be repeated zero or one time | ra?t | rt and rat only |
| \s | Any whitespace character | \sa | [space]a, \ta, \na (\t and \n have the same meanings as in C#) |
| \S | Any character that isn't whitespace | \SF | aF, rF, cF, but not tF |
| \b | Word boundary | ion\b | Any word ending in ion |
| \B | Any position that isn't a word boundary | \B X \B | Any X in the middle of a word |

If you want to search for one of the meta-characters, you can do so by escaping the corresponding character with a backslash. For example, . (a single period) means any single character other than the newline character, whereas \. means a dot.

You can request a match that contains alternative characters by enclosing them in square brackets. For example, [1|c] means one character that can be either 1 or c. If you wanted to search for any occurrence of the words map or man, you would use the sequence ma[n|p]. Within the square brackets, you can also indicate a range, for example [a-z], to indicate any single lowercase letter, [A-Z] to indicate any uppercase letter between A and Z (including the letters A and Z themselves), or [0-9] to represent a single digit. If you want to search for an integer (that is, a sequence that contains only the characters 0 through 9), you could write [0-9]+.

> The use of the + character indicates there must be at least one such digit, but there may be more than one — so this would match 9, 83, 854, and so on.

## Displaying Results

In this section, you code the `RegularExpressionsPlayaround` example, so you can get a feel for how the regular expressions work.

The core of the example is a method called `WriteMatches()`, which writes out all the matches from a `MatchCollection` in a more detailed format. For each match, it displays the index of where the match was found in the input string, the string of the match, and a slightly longer string, which consists of the match plus up to ten surrounding characters from the input text — up to five characters before the match and up to five afterward. (It is fewer than five characters if the match occurred within five characters of the beginning or end of the input text.) In other words, a match on the word messaging that occurs near the end of the input text quoted earlier would display and messaging of d (five characters before and after the match),

but a match on the final word data would display g of data. (only one character after the match), because after that you get to the end of the string. This longer string lets you see more clearly where the regular expression locates the match:

```
static void WriteMatches(string text, MatchCollection matches)
{
    Console.WriteLine("Original text was: \n\n" + text + " \n");
    Console.WriteLine("No. of matches: " + matches.Count);

    foreach (Match nextMatch in matches)
    {
        int index = nextMatch.Index;
        string result = nextMatch.ToString();
        int charsBefore = (index < 5) ? index : 5;
        int fromEnd = text.Length - index - result.Length;
        int charsAfter = (fromEnd < 5) ? fromEnd : 5;
        int charsToDisplay = charsBefore + charsAfter + result.Length;

        Console.WriteLine("Index: {0}, \tString: {1}, \t{2}",
            index, result,
            text.Substring(index-charsBefore, charsToDisplay));
    }
}
```

The bulk of the processing in this method is devoted to the logic of figuring out how many characters in the longer substring it can display without overrunning the beginning or end of the input text. Note that you use another property on the Match object, Value, which contains the string identified for the match. Other than that, RegularExpressionsPlayaround simply contains a number of methods with names such as Find1, Find2, and so on, which perform some of the searches based on the examples in this section. For example, Find2 looks for any string that contains a at the beginning of a word:

```
static void Find2()
{
    string text = @"This comprehensive compendium provides a broad and thorough investigation of all aspects of programming with ASP.NET. Entirely revised and updated for the 3.5 Release of .NET, this book will give you the information you need to master ASP.NET and build a dynamic, successful, enterprise Web application.";
    string pattern = @"\b a";
    MatchCollection matches = Regex.Matches(text, pattern, RegexOptions.IgnoreCase);
    WriteMatches(text, matches);
}
```

Along with this comes a simple Main() method that you can edit to select one of the Find<n>() methods:

```
static void Main()
{
    Find1();
    Console.ReadLine();
}
```

The code also needs to make use of the RegularExpressions namespace:

```
using System;
using System.Text.RegularExpressions;
```

Running the example with the Find2() method shown previously gives these results:

RegularExpressionsPlayaround
Original text was:

This comprehensive compendium provides a broad and thorough investigation of all aspects of programming with ASP.NET. Entirely revised and updated for the 3.5

## 10

## Collections

## WHAT'S IN THIS CHAPTER?

- Understanding collection interfaces and types
- Working with lists, queues, and stacks
- Working with linked and sorted lists
- Using dictionaries and sets
- Using bit arrays and bit vectors
- Evaluating performance

In Chapter 6, "Arrays and Tuples," you read about arrays and the interfaces implemented by the Array class. The size of arrays is fixed. If the number of elements is dynamic, you should use a collection class.

List<T> is a collection class that can be compared to arrays. But there are also other kinds of collections: queues, stacks, linked lists, and dictionaries.

> Version 1.0 of the .NET Framework included non-generic collection classes such as ArrayList and Hashtable. CLR 2.0 added support for generics and generic collection classes. The focus of this chapter is on the newer group of collection classes and mainly ignores the old ones, as they are rarely needed with new applications.

## COLLECTION INTERFACES AND TYPES

Most collection classes can be found in the System.Collections and System.Collections.Generic namespaces. Generic collection classes are located in the System.Collections.Generic namespace. Collection classes that are specialized for a specific type are located in the System.Collections.Specialized namespace. Thread-safe collection classes are in the System.Collections.Concurrent namespace.

Of course, there are also other ways to group collection classes. Collections can be grouped into lists, collections, and dictionaries based on the interfaces that are implemented by the collection class.

The following examples use the members of the class Racer as elements to be added to the collection to represent a Formula-1 racer. This class has five properties: Id, FirstName, LastName, Country, and the number of Wins. With the constructor of the class, the name of the racer and the number of wins can be passed to set the members. The method ToString() is overridden to return the name of the racer. The class Racer also implements the generic interface IComparable<T> for sorting racer elements and IFormattable

```csharp
[Serializable]
public class Racer : IComparable<Racer>, IFormattable
{
    public int Id { get; private set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Country { get; set; }
    public int Wins { get; set; }
    public Racer(int id, string firstName, string lastName, string country = null, int wins = 0)
    {
        this.Id = id;
        this.FirstName = firstName;
        this.LastName = lastName;
        this.Country = country;
        this.Wins = wins;
    }

    public override string ToString()
    {
        return String.Format("{0} {1}", FirstName, LastName);
    }

    public string ToString(string format, IFormatProvider formatProvider)
    {
        if (format == null) format = "N";
        switch (format.ToUpper())
        {
            case "N": // name
                return ToString();
            case "F": // first name
                return FirstName;
            case "L": // last name
                return LastName;
            case "W": // Wins
                return String.Format("{0}, Wins: {1}", ToString(), Wins);
            case "C": // Country
                return String.Format("{0}, Country: {1}", ToString(), Country);
            case "A": // All
                return String.Format("{0}, {1} Wins: {2}", ToString(), Country, Wins);
            default:
                throw new FormatException(String.Format(formatProvider, "Format {0} is not supported", format));
        }
    }

    public string ToString(string format)
    {
        return ToString(format, null);
    }

    public int CompareTo(Racer other)
```
