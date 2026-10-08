# 58 Getting Input from the Command Line

```
// Now write out the number times 2.
Console.WriteLine("2 * " + n + " = " + (2 * n));

// Wait for acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.Read();

// IsAllDigits here.
```

The program reads a line of input from the console keyboard. If IsAllDigits() returns false, the program alerts the user. If the program converts the string into a number using an alternative to Convert.ToInt32(aString) — the Int32.Parse(aString) call. Finally, the program outputs both the number and two times the call (the latter to prove that the program did, in fact, convert the string as advertised).

The output from a sample run of the program appears this way:

```
An integer number
IA3
Hey! That isn't a number
Press Enter to terminate...
```

You could let Convert try to convert gradle and handle any exception it may decide to throw. However, a better-than-even chance exists that it will throw an exception but just return incorrect results — for example, returning I1 when presented with IA3. You should validate input data yourself.

![](bbox=[0.135, 0.49, 0.235, 0.645])

You could instead use Int32.TryParse(s, n), which returns false if the parse fails or true if it succeeds. If it does work, the converted number is found in the second parameter, an int that I named n. This won't throw exceptions. See the next section for an example.

# Handling a series of numbers

Often, a program receives a series of numbers in a single line from the keyboard. Using the String.Split() method, you can easily break the string into a number of substrings, for each number, and parse them separately.

The Split() method chops a single string into an array of smaller strings using some delimiter. For example, if you tell Split() to divide a string using a comma, "1,2,3" makes three strings, "1", "2", and "3". The delimiter is whichever character you use to split collections.

The following program uses the Split() method to input a sequence of numbers to be summed. (Again,毕竟 the IsAllDigits() method to save trees.)