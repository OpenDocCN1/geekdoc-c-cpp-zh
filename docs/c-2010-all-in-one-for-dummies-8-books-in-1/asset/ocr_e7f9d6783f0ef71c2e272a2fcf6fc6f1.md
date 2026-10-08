# Getting Input from the Command Line

+   - Contains() returns true if a given substring can be found within the target string:

```
if(favoriteFood.Contains("*ee")) // True
```

+   - And Substring() returns the string (if it's there), or empty (if not):

```
string sub = favoriteFood.Substring(6, favoriteFood.Length - 6);
```

(I go into Substring()) in greater detail later in this chapter.

# Is my string empty?

How can you tell if a target string is empty ("\

```
bool notThere = string.IsNullOrEmpty(favoriteFood); // False
```

Notice how you call IsNullEmpty(): **string.IsNullOrEmpty(s)****

You can set the empty string in two ways:

```
string name = "";
string name = string.Empty;
```

# Getting Input from the Command Line

A common task in console applications is getting the information that the user uses when you prompt her for, say, an interest rate or a name. You need to read the information that comes in as a string. (Everything from the command line comes as a string). Then you need to parse the input to extract a number from it. And sometimes you need to process input numbers.

# Trimming excess white space

First, consider that in some cases, you don't want to mess with any white space on either end of the string. The term white space refers to the characters that don't normally display on the screen, for example, space, newline (\n), and tab (\t). You might also encounter the carriage return character, \r.

You can use the Trim() method to trim off the edges of the string, like this:

```
Get rid of any extra spaces on either end of the string.
random = random.Trim();
```