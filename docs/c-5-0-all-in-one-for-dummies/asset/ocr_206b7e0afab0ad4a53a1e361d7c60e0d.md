# ### Is my string empty?

How can you tell if a target string is empty ("") or has the value null? (null means that no value has been assigned yet, not even to the empty string.) Use the `IsNullOrEmpty()` method, like this:

```
```csharp
bool notHere = string.IsNullOrEmpty(favoriteFood);  // False
```
```

Notice how you call `IsNullOrEmpty()`: `string.IsNullOrEmpty(s)`.

You can set a string to the empty string in these two ways:

```
```
string name = "";
string name = string.Empty;
```
```

# ## Getting Input from the Command Line

A common task in console applications is getting the information that the user types when you prompt her for, say, an interest rate or a name. You need to read the information that comes in as a string. (Everything coming from the command line comes as a string.) Then you sometimes need to parse the input to extract a number from it. And sometimes you need to process lots of input numbers.

# ### Trimming excess white space

First, consider that in some cases, you don't want to mess with any white space on either end of the string. The term *white space* refers to the characters that don't normally display on the screen — for example, space, newline (or \n), and tab (\t). You may sometimes also encounter the carriage return character, \r.

You can use the `Trim()` method to trim off the edges of the string, like this:

```
```
// Get rid of any extra spaces on either end of the string.
random = random.Trim();
```
```

Class `String` also provides `TrimFront()` and `TrimEnd()` methods for getting more specific, and you can pass an array of chars to be included in the trimming along with white space. For example, you might trim a leading currency sign, such as '$'. Cleaning up a string can make it easier to parse. The trim methods return a new string.

# ### Parsing numeric input

A program can read from the keyboard one character at a time, but you have to worry about newlines and so on. An easier approach reads a string and then parses the characters out of the string.