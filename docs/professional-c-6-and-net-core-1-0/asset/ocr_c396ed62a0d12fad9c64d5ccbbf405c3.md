searches based on the examples in this section. For example, Find2 looks for any string that contains a at the beginning of a word and ions at the end:

```
public static void Find2(string text)
{
    string pattern = @"\ba\S*ions\b";
    MatchCollection matches = Regex.Matches(text, pattern,
        RegexOptions.IgnoreCase);
    WriteMatches(text, matches);
}
```

Along with this is a simple Main method that you can edit to select one of the Find<n> methods:

```
public static void Main()
{
    Find2();
    ReadLine();
}
```

The code also needs to make use of the RegularExpressions namespace:

```
using System;
using System.Text.RegularExpressions;
```

Running the example with the Find2 method shown previously gives these results:

```
No. of matches: 2
Index: 243,     String: additions,     .5.1 additions, as
Index: 469,     String: applications,  web applications imme
```

# Matches, Groups, and Captures

One nice feature of regular expressions is that you can group characters. It works the same way as compound statements in C#. In C#, you can group any number of statements by putting them in braces, and the result is treated as one compound statement. In regular expression patterns, you can group any characters (including meta-characters and escape sequences), and the result is treated as a single character. The only difference is that you use parentheses instead of braces. The resultant sequence is known as a group.

For example, the pattern (an)+ locates any occurrences of the sequence an. The + quantifier applies only to the previous character, but because you have grouped the characters together, it now applies to repeats of an treated as a unit. This means that if you apply (an)+ to the input text, bananas came to Europe late in the annals of history, the anan from bananas is identified; however, if you write an+, the program selects the ann from annals, as well as two separate sequences of an from bananas. The expression (an)+ identifies occurrences of an, anan, ananan, and so on, whereas the expression an+ identifies occurrences of an, ann, annn, and so on.