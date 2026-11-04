```
```csharp
class Class1 {
    static void Main() {
        string input = "Y", Horse;
        int iNumber1 = 0, iNumber2 = 0, iNumber3 = 0;

        Console.WriteLine("Let's have a horse race.\n"
            + "To play select one of the horses below");

        while (char.ToUpper(char.Parse(input)) != 'N') {
            Console.WriteLine("(1) for Whitefire\n"
                + "(2) for The Train and, \n"
                + "(3) for Noisy Glue\n");
            Horse = Console.ReadLine();

            TheRace(ref iNumber1);
            TheRace(ref iNumber2);
            TheRace(ref iNumber3);

            TieBreaker(iNumber1, ref iNumber2);
            TieBreaker(iNumber2, ref iNumber3);
            TieBreaker(iNumber1, ref iNumber3);

            Console.Write("And the winner is ");
            if (iNumber1 > iNumber2 && iNumber1 > iNumber3)
                Console.WriteLine("Noisy Glue"); // 3
            else if (iNumber2 > iNumber1 && iNumber2 > iNumber3)
                Console.WriteLine("The Train"); // 2
            else
                Console.WriteLine("Whitefire"); // 1

            Console.WriteLine("Would you like to play again (Y/N)?");
            input = Console.ReadLine();
        }
    }

    static void TheRace(ref int Num) {
        Random rnd = new Random();

        Num = (int)Math.Round(rnd.NextDouble() * 1000);
    }

    static void TieBreaker(int Num1, ref int Num2) {
        if (Num1 == Num2) {
```
```