
```
compare(string s1, string s2)
{
    // Loop through each character of the strings until
    // a character in one string is greater than the
    // corresponding character in the other string.
    foreach character in the shorter string
        // quit if (s1's character > s2's character when treated as a number)
        return 1
        if (s2's character < s1's character)
            return -1
    // Okay, every letter matches, but if the string s1 is longer,
    // then it's greater.
    if s1 has more characters left
        return 1
    // If s2 is longer, it's greater.
    if s2 has more characters left
        return -1
    // If every character matches and the two strings are the same
    // length, then they are "equal."
    return 0
}
```

Thus, "abcd" is greater than "abbd", and "abcde" is greater than "abcd". More often than not, you don't care whether one string is greater than the other, but only whether the two strings are equal.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_74_0.png)

You do want to know which string is bigger when performing a sort.

The Compare() operation returns 0 when two strings are identical. The following test program uses the equality feature of Compare() to perform a certain operation when the program encounters a particular string or strings.

BuildASentence prompts the user to enter lines of text. Each line is concatenated to the previous line to build a single sentence. This program exits if the user enters the word EXIT, exit, QUIT, or quit.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_74_1.png)

```
// BuildASentence -- The following program constructs sentences
// by concatenating user input until the user enters one of the
// termination characters. This program shows when you need to look for
// string equality.
using System;
namespace BuildASentence
{
    public class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine("Each line you enter will be "
                + "added to a sentence until you "
                + "enter EXIT or QUIT");
            // Ask the user for input; continue concatenating
            // the phrases input until the user enters exit or
            // quit (start with an empty sentence).
            string sentence = "";
            for ( ; ; )
            {
```

~~~csharp
// Get the next line.
Console.WriteLine("Enter a string ");
string line = Console.ReadLine();
// Exit the loop if line is a terminator.
string[] terms = { "EXIT", "exit", "QUIT", "quit" };
// Compare the string entered to each of the
// legal exit commands.
bool quitting = false;
foreach (string term in terms)
{
    // Break out of the for loop if you have a match.
    if (String.Compare(line, term) == 0)
    {
        quitting = true;
    }
}
if (quitting == true)
{
    break;
}
// Otherwise, add it to the sentence.
sentence = String.Concat(sentence, line);
// Let the user know how she's doing.
Console.WriteLine("\nYou've entered: " + sentence);
}
Console.WriteLine("\n\nTotal sentence:\n" + sentence);
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
}
~~~

After prompting the user for what the program expects, the program creates an empty initial sentence string called sentence. From there, the program enters an infinite loop.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_75_0.png)

The controls while(true) and for(;;) loop forever, or at least long enough for some internal break or return to break you out. The two loops are equivalent, and in practice, you'll see them both. (Looping is covered in Chapter 5 of this minibook.)

BuildASentence prompts the user to enter a line of text, which the program reads using the ReadLine() method. Having read the line, the program checks to see whether it is a terminator using the boldfaced lines in the preceding example.

The termination section of the program defines an array of strings called terms and a bool variable quitting, initialized to false. Each member of the terms array is one of the strings you're looking for. Any of these strings causes the program to quit faster than a programmer forced to write COBOL.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_75_1.png)

The program must include both "EXIT" and "exit" because Compare() considers the two strings different by default. (The way the program is written, these are the only two ways to spell exit. Strings such as "Exit" and "eXit" aren't recognized as terminators.) You can also use other string operations to check for various spellings of exit. I show you this in the next section.

The termination section loops through each of the strings in the array of target strings. If Compare() reports a match to any of the terminator phrases, quitting is set to true. If quitting remains false after the termination section and line is not one of the terminator strings, it is concatenated to the end of the sentence using the String.Concat() method. The program outputs the immediate result just so the user can see what's going on.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_76_0.png)

TIP Iterating through an array is a classic way to look for one of various possible values. (I'll show you another way in the next section, and an even cooler way in Book II.)

Here's a sample run of the BuildASentence program:

```
Each line you enter will be added to a
sentence until you enter EXIT or QUIT
Enter a string
Programming with

You've entered: Programming with
Enter a string
C# is fun

You've entered: Programming with C# is fun
Enter a string
(more or less)

You've entered: Programming with C# is fun (more or less)
Enter a string
EXIT

Total sentence:
Programming with C# is fun (more or less)
Press Enter to terminate...
```

I've flagged my input in bold to make the output easier to read.

## Would you like your compares with or without case?

The Compare() method used in the previous example considers "EXIT" and "exit" to be different strings. However, the Compare() method has a second version that includes a third argument. This argument indicates whether the comparison should ignore the letter case. A true indicates "ignore."

The following version of the lengthy termination section in the BuildASentence example sets quitting to true whether the string passed is uppercase, lowercase, or a combination of the two:

```
    // Indicate true if passed either exit or quit,
    // irrespective of case.
    if (String.Compare("exit", source, true) == 0) ||
        (String.Compare("quit", source, true) == 0)
    {
        quitting = true;
    }
```

This version is simpler than the previous looping version. This code doesn't need to worry about case, and it can use a single conditional expression because it now has only two options to consider instead of a longer list: any spelling variation of QUIT or EXIT.

## What If I Want to Switch Case?

You may be interested in whether all of the characters (or just one) in a string are uppercase or lowercase characters. And you may need to convert from one to the other.

### Distinguishing between all-uppercase and all-lowercase strings

I almost hate to bring it up, but you can use the switch command (see Chapter 5 of this minibook) to look for a particular string. Normally, you use the switch command to compare a counting number to some set of possible values; however, switch does work on string objects, as well. This version of the termination section in BuildASentence uses the switch construct:

```
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

This approach works because you're comparing only a limited number of strings. The for loop offers a much more flexible approach for searching for string values. Using the case-less Compare() in the previous section gives the program greater flexibility in understanding the user.

### Converting a string to upper- or lowercase

Suppose you have a string in lowercase and need to convert it to uppercase. You can use the ToUpper() method:
