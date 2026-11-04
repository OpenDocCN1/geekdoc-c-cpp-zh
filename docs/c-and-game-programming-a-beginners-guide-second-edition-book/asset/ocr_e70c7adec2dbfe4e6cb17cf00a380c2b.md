```
```csharp
int winner, number1 = 0, number2 = 0, number3 = 0;

Console.WriteLine("Let's have a horse race.\n"
    + "To play select one of the horses below");

while (char.ToUpper (race) != 'N') {
    Console.WriteLine("(1) for Whitefire\n"
        + "(2) for The Train and, \n"
        + "(3) for Noisy Glue");

    input = Console.ReadLine();

    the_race(&number1, &number2, &number3);
    tie_breaker(&number1, &number2);
    tie_breaker(&number2, &number3);
    tie_breaker(&number1, &number3);

    winner = the_winner(&number1, &number2, &number3);
    Console.Write("And the winner is ");

    if (winner == '1')
        Console.WriteLine("Whitefire");
    else if (winner == '2')
        Console.WriteLine("The Train");
    else
        Console.WriteLine("Noisy Glue");

    Console.Write("Would you like to play again (Y/N)?");
    input = Console.ReadLine();
    race = char.Parse(input);
}
}

static unsafe void the_race(int *number1, int *number2,
    int *number3) {
    Random rnd = new Random();

    *number1 = (int)(rnd.NextDouble() * 100);
    *number2 = (int)(rnd.NextDouble() * 100);
    *number3 = (int)(rnd.NextDouble() * 100);
    Console.Write(".");
}

static unsafe void tie_breaker(int *num1, int *num2) {
    if (*num1 == *num2)
```
```