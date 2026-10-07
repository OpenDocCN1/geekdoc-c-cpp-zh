Starting with C# 7.0, it is no longer necessary to declare a variable before using it as an out argument. Using this feature, the declaration for number is shown in Listing 2.36.

# LISTING 2.36: TryParse() with Inline Declaration in C# 7.0

```
// double number;
string input;

Console.Write("Enter a number: ");
input = Console.ReadLine();
if (double.TryParse(input, out double number))
{
    Console.WriteLine($"{input was parsed successfully to {number}.");
}
else
{
    // Note: number scope is here too (although not assigned)
    Console.WriteLine("The text entered was not a valid number.");
}

Console.WriteLine($"{number} currently has the value: {number}");
```

Notice that the data type of number is specified following the out modifier before the variable it declares. The result is that the number variable is available from both the true and false consequences of the if statement and even outside the if statement.

The key difference between Parse() and TryParse() is that TryParse() won't throw an exception if it fails. Frequently, the conversion from a string to a numeric type depends on a user entering the text. It is expected, in such scenarios, that the user will enter invalid data that will not parse successfully. By using TryParse() rather than Parse(), you can avoid throwing exceptions in expected situations. (The expected situation in this case is that the user will enter invalid data, and we try to avoid throwing exceptions for expected scenarios.)