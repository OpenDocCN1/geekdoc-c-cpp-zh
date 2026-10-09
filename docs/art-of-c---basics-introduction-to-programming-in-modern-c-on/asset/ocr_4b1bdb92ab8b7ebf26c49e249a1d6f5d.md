```
var input = Console.ReadLine();
if (ushort.TryParse(input, out ushort number) &&
IsVaidMegaNumber(number)) {
    mega = number;
    break;
} else {
    Console.WriteLine("Input a number in the range from 1 to
    25.");
    continue;
}
return mega;
}
private static bool IsVaidNumber(ushort num) => (num >= 1) && (num
<= 70);
private static bool IsVaidMegaNumber(ushort num) => (num >= 1) &&
(num <= 25);
}
```

# mega-millions/Game.cs

```
namespace Mega;
public static class Game {
    internal const int NumWhiteBalls = 5;
    private static readonly Random rand;
    static Game() => rand = new Random();
    public static (ushort[], ushort) DrawBalls() {
        var whites = new ushort[NumWhiteBalls];
        for (var i = 0; i < NumWhiteBalls; i++) {
            whites[i] = (ushort)(rand.Next(75) + 1);
        }
        var gold = (ushort)(rand.Next(25) + 1);
```