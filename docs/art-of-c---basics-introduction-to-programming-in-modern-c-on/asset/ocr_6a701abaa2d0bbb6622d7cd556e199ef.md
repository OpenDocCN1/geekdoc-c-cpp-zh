Here’s the implementation of the Millions static class:

meg-millions/Millions.cs

```
```
namespace Mega;

public static class Millions {
    public static void Play() {
        var (numbers, mega) = Input.Read();
        Console.WriteLine($"You selected: numbers = [{string.Join(', ', numbers)}]; Mega number = {mega}");
        
        var (whites, gold) = Game.DrawBalls();
        Console.WriteLine($"White balls drawn = [{string.Join(', ', whites)}]; The golden ball = {gold}");
        
        var prize = Game.DeterminePrize(whites, gold, numbers, mega);
        if (prize > Prize.None) {
            Console.WriteLine($"Congratulations! You won!!! Your prize is {prize}!");
        } else {
            Console.WriteLine($"Thanks for playing Fake Mega Millions!");
        }
    }
}
```
```

Note that we declare the Millions class public in this lesson. Although it is an Executable assembly that we are building here, we can easily change it to the library type if we want to make this game library available to other C# developers.

This class includes one static method, Play(), which is also declared as public.

The static class, Input, handles the user input:

meg-millions/Input.cs