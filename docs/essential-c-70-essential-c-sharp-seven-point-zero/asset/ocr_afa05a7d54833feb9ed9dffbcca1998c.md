```
```
else
{
    System.Console.WriteLine(
        "The text entered was not a valid number.");
}
```
```

Output 2.18 shows the results of Listing 2.29.

# **OUTPUT 2.18**

> ```
Enter a number: forty-two
The text entered was not a valid number.
```

The resultant value that the code parses from the input string is returned via an out parameter—in this case, number.

It is worth pointing out that, starting with C# 7.0, it is no longer necessary to declare a variable before using it as an out argument. Using this feature, the declaration for number is shown in Listing 2.30.

# **LISTING 2.30: Using TryParse() with Inline out Declaration in C# 7.0**

```
```csharp
// double number;
string input;

System.Console.Write("Enter a number: ");
input = System.Console.ReadLine();
if (double.TryParse(input, out double number))
{
    System.Console.WriteLine(
        $"{input} was parsed successfully to {number}.");
}
else
{
    // Note: number scope is here too (although not assigned)
    System.Console.WriteLine(
        "The text entered was not a valid number.");
}
```
```

Notice that the data type of number is specified following the out modifier and before the variable that it declares. The result is that the number variable is available from both the true and false consequence of the if statement but not outside the if statement.

The key difference between Parse() and TryParse() is that TryParse() won’t throw an exception if it fails. Frequently, the conversion from a string to a numeric type depends on a user entering the text. It is