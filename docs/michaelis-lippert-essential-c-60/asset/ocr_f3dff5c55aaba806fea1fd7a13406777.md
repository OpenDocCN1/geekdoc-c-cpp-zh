# OUTPUT 2.8

```
: )
```

# Strings

A finite sequence of zero or more characters is called a string. The string type in C# is string, whose BCL name is System.String. The string type includes some special characteristics that may be unexpected to developers familiar with other programming languages. In addition to the string literal format discussed in Chapter 1, strings include a “verbatim string” prefix character of @, string interpolation with the $ prefix character, and the fact that strings are immutable.

# Literals

You can enter a literal string into code by placing the text in double quotes (") , as you saw in the HelloWorld program. Strings are composed of characters, and because of this, character escape sequences can be embedded within a string.

In Listing 2.11, for example, two lines of text are displayed. However, instead of using System.Console.WriteLine(), the code listing shows System.Console.Write() with the newline character, \n. Output 2.9 shows the results.

# LISTING 2.11: Using the \n Character to Insert a Newline

```
class DuelOfWits
{
    static void Main()
    {
        System.Console.Write(
            "\"Truly, you have a dizzying intellect.\"" );
        System.Console.Write("\"\n\"Wait 'til I get going!\"\n");
    }
}
```

# OUTPUT 2.9

```
"Truly, you have a dizzying intellect."
"Wait 'til I get going!"
```