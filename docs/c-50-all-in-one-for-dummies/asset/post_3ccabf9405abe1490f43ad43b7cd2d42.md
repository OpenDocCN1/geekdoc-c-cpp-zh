
Parsing characters out of a string is another topic I don't like to mention, for fear that programmers will abuse this technique. In some cases, programmers are too quick to jump into the middle of a string and start pulling out what they find there. This is particularly true of C++ programmers because that's the only way they could deal with strings — until the addition of a string class.

The ReadLine() method used for reading from the console returns a string object. A program that expects numeric input must convert this string. C# provides just the conversion tool you need in the Convert class. This class provides a conversion method from string to each built-in variable type. Thus, this code segment reads a number from the keyboard and stores it in an int variable:

```
string s = Console.ReadLine();  // Keyboard input is string data
int n = Convert.ToInt32(s);     // but you know it's meant to be a number.
```

The other conversion methods are a bit more obvious: ToDouble(), ToFloat(), and ToBoolean().

ToInt32() refers to a 32-bit, signed integer (32 bits is the size of a normal int), so this is the conversion method for ints. ToInt64() handles the size of a long.

When Convert() encounters an unexpected character type, it can generate unexpected results. Thus, you must know for sure what type of data you're processing and ensure that no extraneous characters are present.

Although I haven't fully discussed methods yet (see Book II), here's one anyway. The following method returns true if the string passed to it consists of only digits. You can call this method prior to converting into a type of integer, assuming that a sequence of nothing but digits is probably a legal number.

To be truly complete, you need to include the decimal point for floating-point variables and include a leading minus sign for negative numbers — but hey, you get the idea.

Here's the method:

```
// IsAllDigits -- Return true if all characters
//   in the string are digits.
public static bool IsAllDigits(string raw)
{
    // First get rid of any benign characters at either end;
    // if there's nothing left, you don't have a number.
    string s = raw.Trim();  // Ignore white space on either side.
    if (s.Length == 0) return false;
    // Loop through the string.
    for(int index = 0; index < s.Length; index++)
    {
        // A nondigit indicates that the string probably isn't a number.
        if (Char.IsDigit(s[index]) == false) return false;
    }
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_81_0.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_81_1.png)

```
// No nondigits found; it's probably okay.
return true;
}
```

The method IsAllDigits() first removes any harmless white space at either end of the string. If nothing is left, the string was blank and could not be an integer. The method then loops through each character in the string. If any of these characters turns out to be a nondigit, the method returns false, indicating that the string is probably not a number. If this method returns true, the probability is high that the string can be converted into an integer successfully.

The following code sample inputs a number from the keyboard and prints it back out to the console. (I omitted the IsAllDigits() method from the listing to save space, but I've boldfaced where this program calls it.)

![](img/6df7bb88e9302e98442acc219cfbd7fc_82_0.png)

```
// IsAllDigits -- Demonstrate the IsAllDigits method.
using System;
namespace IsAllDigits
{
class Program
{
public static void Main(string[] args)
{
// Input a string from the keyboard.
Console.WriteLine("Enter an integer number");
string s = Console.ReadLine();
// First check to see if this could be a number.
if (!IsAllDigits(s)) // Call the special method.
{
Console.WriteLine("Hey! That isn't a number");
}
else
{
// Convert the string into an integer.
int n = Int32.Parse(s);
// Now write out the number times 2.
Console.WriteLine(2 * " " + n + " = " + (2 * n));
}
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
// IsAllDigits here.
}
}
```

The program reads a line of input from the console keyboard. If IsAllDigits() returns false, the program alerts the user. If not, the program converts the string into a number using an alternative to Convert.ToInt32(aString) — the Int32.Parse(aString) call. Finally, the program outputs both the number and two times the number (the latter to prove that the program did, in fact, convert the string as advertised).

The output from a sample run of the program appears this way:

```
Enter an integer number
1A3
Hey! That isn't a number
Press Enter to terminate...
```

You could let Convert try to convert garbage and handle any exception it may decide to throw. However, a better-than-even chance exists that it won’t throw an exception but will just return incorrect results — for example, returning 1 when presented with 1A3. You should validate input data yourself.

You could instead use Int32.TryParse(s, n), which returns false if the parse fails or true if it succeeds. If it does work, the converted number is found in the second parameter, an int that I named n. This won’t throw exceptions. See the next section for an example.

# Handling a series of numbers

Often, a program receives a series of numbers in a single line from the keyboard. Using the String.Split() method, you can easily break the string into a number of substrings, one for each number, and parse them separately.

The Split() method chops a single string into an array of smaller strings using some delimiter. For example, if you tell Split() to divide a string using a comma (,) as the delimiter, "1,2,3" becomes three strings, "1", "2", "3".

```
// ParseWithSplit -- Input a series of numbers
// parse them into integers and output the sum.
using System;
namespace ParseWithSplit
{
    class Program
    {
        public static void Main(string[] args)
        {
            // Prompt the user to input a sequence of numbers.
            Console.WriteLine("Input a series of numbers separated by commas:");
            // Read a line of text.
            string input = Console.ReadLine();
            // Split the line upon commas or spaces.
            char[] dividers = {',', ' '};
            string[] segments = input.Split(dividers);
            int sum = 0;

            foreach(string s in segments)
            {
                // Skip empty segments.
                if (s.Length > 0)
                {
                    // Skip strings that aren't numbers.
                    if (IsAllDigits(s))
                    {
                        // Convert the string into a 32-bit int.
                        int num = 0;
                        if (Int32.TryParse(s, out num))
                        {
                            // Output each number
                            Console.WriteLine("Next number = {0}", num);
                            // Add this number into the sum.
                            sum += num;
                        }
                    }
                }
            }
            // Output the sum.
            Console.WriteLine("Sum = {0}", sum);
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }

        // IsAllDigits here.
        public static bool IsAllDigits(string raw)
        {
            // First get rid of any benign characters at either end;
            // if there's nothing left, you don't have a number.
            string s = raw.Trim();  // Ignore white space on either side.
            if (s.Length == 0) return false;
            // Loop through the string.
            for(int index = 0; index < s.Length; index++)
            {
                // A nondigit indicates that the string probably isn't a number.
                if (Char.IsDigit(s[index]) == false) return false;
            }
            // No nondigits found; it's probably okay.
            return true;
        }
    }
}
```

Here's the output of a typical run:

```
Input a series of numbers separated by commas:
1,2, a, 3 4

Next number = 1
Next number = 2
Next number = 3
Next number = 4
Sum = 10
Press Enter to terminate...
```

The program splits the list, accepting commas, spaces, or both as separators. It successfully skips over the a to generate the result of 10. In a real-world program, however, you probably don't want to skip over incorrect
