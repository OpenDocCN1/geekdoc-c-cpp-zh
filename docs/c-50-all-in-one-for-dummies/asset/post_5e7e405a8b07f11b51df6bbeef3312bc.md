
end of the sentence using the String.Concat() method. The program outputs the immediate result just so the user can see what’s going on.

Iterating through an array is a classic way to look for one of various possible values. (I’ll show you another way in the next section, and an even cooler way in Book II.)

Here’s a sample run of the BuildASentence program:

```
Each line you enter will be added to a
sentence until you enter EXIT or QUIT
Enter a string
Programming with

You’ve entered: Programming with
Enter a string
C# is fun

You’ve entered: Programming with C# is fun
Enter a string
(more or less)

You’ve entered: Programming with C# is fun (more or less)
Enter a string
EXIT

Total sentence:
Programming with C# is fun (more or less)
Press Enter to terminate...
```

I’ve flagged my input in bold to make the output easier to read.

## Would you like your compares with or without case?

The Compare() method used in the previous example considers "EXIT" and "exit" to be different strings. However, the Compare() method has a second version that includes a third argument. This argument indicates whether the comparison should ignore the letter case. A true indicates "ignore."

The following version of the lengthy termination section in the BuildASentence example sets quitting to true whether the string passed is uppercase, lowercase, or a combination of the two:

```csharp
// Indicate true if passed either exit or quit,
// irrespective of case.
if (String.Compare("exit", source, true) == 0 ||
    (String.Compare("quit", source, true) == 0)
{
    quitting = true;
}
```

This version is simpler than the previous looping version. This code doesn’t need to worry about case, and it can use a single conditional expression because it now has only two options to consider instead of a longer list: any spelling variation of QUIT or EXIT.

## What If I Want to Switch Case?

You may be interested in whether all of the characters (or just one) in a string are uppercase or lowercase characters. And you may need to convert from one to the other.

### Distinguishing between all-uppercase and all-lowercase strings

I almost hate to bring it up, but you can use the switch command (see Chapter 5 of this minibook) to look for a particular string. Normally, you use the switch command to compare a counting number to some set of possible values; however, switch does work on string objects, as well. This version of the termination section in BuildASentence uses the switch construct:

```csharp
switch(line)
{
    case "EXIT":
    case "exit":
    case "QUIT":
    case "quit":
        return true;
}
return false;
```

This approach works because you’re comparing only a limited number of strings. The for loop offers a much more flexible approach for searching for string values. Using the case-less Compare() in the previous section gives the program greater flexibility in understanding the user.

## Converting a string to upper- or lowercase

Suppose you have a string in lowercase and need to convert it to uppercase. You can use the ToUpper() method:

```csharp
string lowercase = "armadillo";
string upcase = lowercase.ToUpper();  // ARMADILLO.
```

Similarly, you can convert uppercase to lowercase with ToLower().

What if you want to convert just the first character in a string to uppercase? The following rather convoluted code will do it (but you can see a better way in the last section of this chapter):

```csharp
string name = "chuck";
string properName =
    char.ToUpper(name[0]).ToString() + name.Substring(1, name.Length - 1);
```

The idea in this example is to extract the first char in name (that’s name[0]), convert it to a one-character string with ToString(), and then tack on the remainder of name after removing the old lowercase first character with Substring().

You can tell whether a string is uppercased or lowercased by using this scary-looking if statement:

```csharp
if (string.Compare(line.ToUpper(CultureInfo.InvariantCulture),
    line, false) == 0) ... // True if line is all upper.
```

Here the Compare() method is comparing an uppercase version of line to line itself. There should be no difference if line is already uppercase. You can puzzle over the CultureInfo.InvariantCulture gizmo in Help, ’cause I’m not going to explain it here. For “is it all lowercase,” stick a not (!) operator in front of the Compare() call. Alternatively, you can use a loop, as described in the next section.

The StringCaseChanging example on the website illustrates these and other techniques, including a brief explanation of cultures.

![](img/6df7bb88e9302e93)

### Looping through a string

You can access characters in a string using a foreach loop. The following code steps through:

```csharp
string favoriteFood = "cheesurgers";
foreach (char c in favoriteFood)
{
    Console.WriteLine(c);
}
```

## Searching Strings

How can you tell if a string is empty ("") or has null? (null means no value has been assigned yet). Use the IsNullOrEmpty method, like this:

```csharp
bool notThere = string.IsNullOrEmpty(favoriteFood); // False
```

You can set a string to the empty string in two ways:

```csharp
string name = "";
string name = string.Empty;
```

If you want to find a character, you use index notation. Arrays start with zero, so if you want the first character, you ask for [0]. If you want the third, you ask for [2].

```csharp
char thirdChar = favoriteFood[2]; // 'e' in "cheesurgers"
```
