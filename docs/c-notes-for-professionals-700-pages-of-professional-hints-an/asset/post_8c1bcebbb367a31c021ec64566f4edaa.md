
```csharp
var prefixedIfNecessary = $"{integerValue:D5}";
// String value is "00057"
```

Live Demo on .NET Fiddle

## Section 15.5: Simple Usage

```csharp
var name = "World";
var str = $"Hello, {name}!";
//str now contains: "Hello, World!";
```

### Behind the scenes

Internally this

```
$"Hello, {name}!"
```

Will be compiled to something like this:

```csharp
string.Format("Hello, {0}!", name);
```

## Chapter 16: String Escape Sequences

### Section 16.1: Escaping special symbols in string literals

### Backslash

```csharp
// The filename will be c:\myfile.txt in both cases
string filename = "c:\\myfile.txt";
string filename = @"c:\myfile.txt";
```

The second example uses a verbatim string literal, which doesn't treat the backslash as an escape character.

### Quotes

```csharp
string text = "\"Hello World!\", said the quick brown fox.";
string verbatimText = @"""Hello World!"", said the quick brown fox.";
```

Both variables will contain the same text.

> "Hello World!", said the quick brown fox.

### Newlines

Verbatim string literals can contain newlines:

```csharp
string text = "Hello\r\nWorld!";
string verbatimText = @"Hello
World!";
```

Both variables will contain the same text.

### Section 16.2: Unicode character escape sequences

```csharp
string sqrt = "\\u221A"; // √
string emoji = "\\U0001F601"; // ?
string text = "\\u0022Hello World\\u0022"; // "Hello World"
string variableWidth = "\\x22Hello World\\x22"; // "Hello World"
```

### Section 16.3: Escaping special symbols in character literals

### Apostrophes

```csharp
char apostrophe = '\'';
```

### Backslash

```csharp
char oneBackslash = '\\';
```

### Section 16.4: Using escape sequences in identifiers

Escape sequences are not restricted to string and char literals.

Suppose you need to override a third-party method:

```csharp
protected abstract IEnumerable<Texte> ObtenirŒuvres();
```

and suppose the character Œ is not available in the character encoding you use for your C# source files. You are lucky, it is permitted to use escapes of the type \u#### or \U######## in identifiers in the code. So it is legal to write:

```csharp
protected override IEnumerable<Texte> Obtenir\u0152uvres()
{
    // ...
}
```

and the C# compiler will know Œ and \u0152 are the same character.

(However, it might be a good idea to switch to UTF-8 or a similar encoding that can handle all characters.)

### Section 16.5: Unrecognized escape sequences produce compile-time errors

The following examples will not compile:

```csharp
string s = "\c";
char c = '\c';
```

Instead, they will produce the error Unrecognized escape sequence at compile time.

## Chapter 17: StringBuilder

### Section 17.1: What a StringBuilder is and when to use one

A StringBuilder represents a series of characters, which unlike a normal string, are mutable. Often times there is a need to modify strings that we've already made, but the standard string object is not mutable. This means that each time a string is modified, a new string object needs to be created, copied to, and then reassigned.

```csharp
string myString = "Apples";
myString += " are my favorite fruit";
```

In the above example, myString initially only has the value "Apples". However, when we concatenate " are my favorite fruit", what the string class does internally needs to do involves:

- Creating a new array of characters equal to the length of myString and the new string we are appending.
- Copying all of the characters of myString into the beginning of our new array and copying the new string into the end of the array.
- Create a new string object in memory and reassign it to myString.

For a single concatenation, this is relatively trivial. However, what if needed to perform many append operations, say, in a loop?

```csharp
string myString = "";
for (int i = 0; i < 10000; i++)
    myString += " "; // puts 10,000 spaces into our string
```

Due to the repeated copying and object creation, this will bring significantly degrade the performance of our program. We can avoid this by instead using a StringBuilder.

```csharp
StringBuilder myStringBuilder = new StringBuilder();
for (int i = 0; i < 10000; i++)
    myStringBuilder.Append(' ');
```

Now when the same loop is run, the performance and speed of the execution time of the program will be significantly faster than using a normal string. To make the StringBuilder back into a normal string, we can simply call the ToString() method of StringBuilder.

However, this isn't the only optimization StringBuilder has. In order to further optimize functions, we can take advantage of other properties that help improve performance.

```csharp
StringBuilder sb = new StringBuilder(10000); // initializes the capacity to 10000
```

If we know in advance how long our StringBuilder needs to be, we can specify its size ahead of time, which will prevent it from needing to resize the character array it has internally.

```csharp
sb.Append('k', 2000);
```

Though using StringBuilder for appending is much faster than a string, it can run even faster if you only need to add a single character many times.

Once you have completed building your string, you may use the ToString() method on the StringBuilder to convert it to a basic string. This is often necessary because the StringBuilder class does not inherit from string.

For example, here is how you can use a StringBuilder to create a string:

```csharp
string RepeatCharacterTimes(char character, int times)
{
    StringBuilder builder = new StringBuilder("");
    for (int counter = 0; counter < times; counter++)
    {
        //Append one instance of the character to the StringBuilder.
        builder.Append(character);
    }
    //Convert the result to string and return it.
    return builder.ToString();
}
```

In conclusion, StringBuilder should be used in place of string when many modifications to a string need to be made with performance in mind.

### Section 17.2: Use StringBuilder to create string from a large number of records

```csharp
public string GetCustomerNamesCsv()
{
    List<CustomerData> customerDataRecords = GetCustomerData(); // Returns a large number of records, say, 10000+
    StringBuilder customerNamesCsv = new StringBuilder();
    foreach (CustomerData record in customerDataRecords)
    {
        customerNamesCsv
            .Append(record.LastName)
            .Append(',')
            .Append(record.FirstName)
            .Append(Environment.NewLine);
    }
    return customerNamesCsv.ToString();
}
```

## Chapter 18: Regex Parsing

| Name | Details |
|---|---|
| Pattern | The string pattern that has to be used for the lookup. For more information: msdn |
| RegexOptions [Optional] | The common options in here are Singleline and Multiline. They are changing the behaviour of pattern-elements like the dot (.) which won't cover a NewLine (\n) in Multiline-Mode but in SingleLine-Mode. Default behaviour: msdn |
| Timeout [Optional] | Where patterns are getting more complex the lookup can consume more time. This is the passed timeout for the lookup just as known from network-programming. |

### Section 18.1: Single match

```csharp
using System.Text.RegularExpressions;

string pattern = ":(.*?) :";
string lookup = "--:text in here:--";

// Instantiate your regex object and pass a pattern to it
Regex rgxLookup = new Regex(pattern, RegexOptions.Singleline, TimeSpan.FromSeconds(1));
// Get the match from your regex-object
Match mLookup = rgxLookup.Match(lookup);

// The group-index 0 always covers the full pattern.
// Matches inside parentheses will be accessed through the index 1 and above.
string found = mLookup.Groups[1].Value;
```

Result:

```
found = "text in here"
```

### Section 18.2: Multiple matches

```csharp
using System.Text.RegularExpressions;

List<string> found = new List<string>();
string pattern = ":(.*?) :";
string lookup = "--:text in here:--another one:--third one:---!123:fourth:";

// Instantiate your regex object and pass a pattern to it
Regex rgxLookup = new Regex(pattern, RegexOptions.Singleline, TimeSpan.FromSeconds(1));
MatchCollection mLookup = rgxLookup.Matches(lookup);

foreach (Match match in mLookup)
{
    found.Add(match.Groups[1].Value);
}
```

Result:

```
found = new List<string>() { "text in here", "another one", "third one", "fourth" }
```
