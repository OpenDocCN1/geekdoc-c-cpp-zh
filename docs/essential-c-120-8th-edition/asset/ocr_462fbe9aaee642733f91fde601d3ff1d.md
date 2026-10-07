# Chapter 5: Parameters and Methods

Since you have not yet provided any such handling, the program reports the exception to the user as an unhandled exception. Assuming there is no registered debugger the console applications will display the error on the console with a message such as that shown in Output 5.11.

# Output 5.11

```
Hey you!
Enterter your first name: Inigo
ter your age: forty-two

Unhandled Exception: System.FormatException: Input string not in a correct format.
at System.Number.ThrowOverflowFormatException(...)
at System.Number.ParseInt32(String s)
at ...ExceptionHandling.Main()
```

Obviously, such an error is not particularly helpful. To fix this, it is necessary to provide a mechanism that handles the error, perhaps reporting a more meaningful error back to the user.

This process is known as catching an exception. The syntax is demonstrated in Listing 5.27, and the output appears in Output 5.12.

# Listing 5.27: Catching Exception

```
public class ExceptionHandling
{
    public static void Main(string[] args)
    {
        string? firstName;
        string ageText;
        int age;
        int result = 0;

        Console.Write("Enter your first name: ");
        firstName = Console.ReadLine();

        Console.Write("Enter your age: ");
        // Assume not null for clarity
        ageText = Console.ReadLine()!;

        try
        {
            age = int.Parse(ageText);
            Console.WriteLine(
```