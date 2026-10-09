
![](img/25af69ec45b3c0b589a8dccd0c2a88be_439_0.png)

## 27.2. Discussion

We will use a "dummy display" on the terminal. But, in theory, we can use the program to control the real digital clock display, depending on what kind "interface" the display exposes as "APT".

Here's an example time display:

```
$ dotnet run
Current time is:
`-   -   -` `_ | ||_ |_` `|_  | _| _|`
Current time is:
`-   -   -` `_ | ||_ |_` `|_  | ||_|`
Current time is:
`-   -   -` `_ | ||_  |` `|_  | _|  |` `^C`
```

The sample app displays a new time every 60 seconds. We killed the program using the interrupt signal (Control+C on Unix, for instance) in this example.

## 27.3. Sample Code Snippets - led-clock-digital

The main program merely calls the async Run() method of an LED.Clock object, which in turn calls the DisplayCurrentTime() method every 60 seconds by default.

```
led-clock-digital/Program.cs (lines 3-4)
`3 var clock = new Clock();`
`4 await clock.Run();`
```

As indicated before, a different Main() method is generated from the top-level statements based on a few conditions: Whether they use the command line arguments or not, whether they return a value at the end, and whether they call any `async` methods with `await`.

The valid signatures of the C# `Main` method are the following:

```
public static void Main();
public static int Main();
public static void Main(string[] args);
public static int Main(string[] args);
public static async Task Main();
public static async Task<int> Main();
public static async Task Main(string[] args);
public static async Task<int> Main(string[] args);
```

Note that 2 times 2 times 2 is 8. One can use any of these 8 as the main method of a program (e.g., in a class or interface). In the case of the top-level statements, as stated, the compiler generates the appropriate `Main()` method.

`Clock` is implemented as a `sealed class`, not as a `struct` or `record`, since we are interested in its behavior, e.g., the "clock-ness", if you will.

```
led-clock-digital/Clock.cs (lines 4-26)

public sealed class Clock {
    const int NumDigits = 4;

    private readonly ILedDisplay display;

    public Clock() => display = new LedDisplay(NumDigits);

    public async Task Run(int milliDelay = 60_000) {
        while (true) {
            Console.WriteLine("Current time is:");
            DisplayCurrentTime();
            await Task.Delay(milliDelay);
            Console.WriteLine();
        }
    }

    public void DisplayCurrentTime() {
        var time = DateTime.Now;
        var str = $"{time.Hour:D2}{time.Minute:D2}";
        var digits = str.Select(c => Digit.Get(c)).ToArray();
        display.Show(digits);
    }
}
```

The Clock class encapsulates the basic characteristics of a "clock". It gets the time, from the simple .NET API DateTime.Now in this case, and it displays the time (on a regular interval). That is a clock.

Note that the implementation of the DisplayCurrentTime() method uses another LINQ method, as defined as an extension method on IEnumerable<T>. The Select() method takes an argument of a delegate type, Func<Char, Digit> in this particular case.

The method is called with a lambda function, c -> Digit.Get(c), to convert a char to the corresponding "Digit". It returns a value of `IEnumerable<Digit>`.

Our hypothetical display device uses `Digits` to communicate the information regarding which LEDs should be turned on or off.

*led-clock-digital/Common/Digits.cs (lines 3-10)*

```
3} public sealed record Digit { 4 public static readonly Digit None = new(new byte[] { 5 0, 0, 0, 0, 0, 0 6 }); 8 public static readonly Digit Zero = new(new byte[] { 9 1, 1, 1, 0, 1, 1, 1 10 });
```

```
led-clock-digital/Common/Digits.cs (lines 48-67)
```
public static Digit Get(char c) =>
    c switch {
        '0' => Zero,
        '1' => One,
        '2' => Two,
        '3' => Three,
        '4' => Four,
        '5' => Five,
        '6' => Six,
        '7' => Seven,
        '8' => Eight,
        '9' => Nine,
        _ => None,
    };

private readonly byte[] leds;

private Digit(byte[] leds) {
    this.leds = leds;
}
```

(Note that we are not including the entire program here. For a full code sample, refer to the appendix.)

A type Digit is essentially a simple wrapper around the type byte[] (for 7 LEDs), again using the composition, and it defines a single public API, the Get() method. The Get() method uses the switch expression to convert a char to one of the ten predefined Digits. For a char that is not a digit/number, we simply return the "default" value for the Digit type, None.

There are a couple of things to note about the Digit type. First, its (only) constructor is private. Nobody can instantiate a Digit. They can only use the predefined digits plus None.

Another thing to note is that `Digit` is a record type. Not a struct type. In general, it is best for a value type not to include any reference type fields. It is generally hard to enforce value semantics on a value that includes any reference variables. In this particular case, however, since there is no way to update internal field, `leds`, since the constructor is private and there are no setters, we could have also used `struct`.

Note the implementation of the constructor. We simply copy the reference of the argument `leds`. If anybody else has an access to the reference variable, they can easily change the values of the elements of `leds`, which is not the behavior we desire.

In general, a better implementation would have been to "copy", or "clone", the argument array and keep the "private copy" internally. As stated, software design is about a tradeoff. Doing so would have been more expensive in terms of the computational requirements.

> The 7 LEDs are arranged in a particular order. Again, a code comment would have been nice in situations like this. Can you guess the mapping between the array indices, 0 ~ 6, and the particular LEDs?

We use the interface, `ILEDDisplay`, for "abstraction". That is, our `Clock` implementation uses the interface and we can "plug" in any `ILEDDisplay` implementations later (possibly, with some minor changes).

In this case, for instance, we may ultimately want to use our `Clock` to interface with real digital LED clocks.

```
led-clock-digital/Common/Display.cs (lines 3-9)
```csharp
    } public interface IDisplay {
        void Clear();
    }

    public interface ILEDDisplay : IDisplay {
        void Show(Digit[] digits);
    }
```

In software design, "abstraction" is a very powerful strategy, with broad applicability. Using interfaces to "abstract away" the implementation details is one of the most common "abstraction" strategies.

For concreteness, in this lesson, we use a "fake" ASCII display. The types are defined in the `LED.Ascii` namespace. The `Number` record is immutable, just like the `Digit` type.

```
led-clock-digital/Ascii/Number.cs (lines 4-14)
```csharp
    sealed record Number {
        internal static readonly Number None = new(new char[],] {
            { ' ', ' ', ' ' },
            { ' ', ' ', ' ' },
            { ' ', ' ', ' ' },
        });
        internal static readonly Number Zero = new(new char[],] {
            { '|', '-', '|' },
            { '|', ' ', '|' },
            { '|', '-', '|' },
        });
```

```
led-clock-digital/Ascii/Number.cs (lines 61-104)
```csharp
    private static readonly Dictionary<Digit, Number> digits = new() {
        { Digit.Zero, Zero },
```

```
```
63         { Digit.One, One },
64         { Digit.Two, Two },
65         { Digit.Three, Three },
66         { Digit.Four, Four },
67         { Digit.Five, Five },
68         { Digit.Six, Six },
69         { Digit.Seven, Seven },
70         { Digit.Eight, Eight },
71         { Digit.Nine, Nine },
72         };
73
74     internal static Number Convert(Digit d) =>
75             digits.ContainsKey(d) ? digits[d] : None;
76
77     private readonly char[,] leds;
78
79     private Number(char[,] leds) {
80         this.leds = leds;
81     }
82
83     internal int Rows => leds.GetLength(0);
84     internal int Cols => leds.GetLength(1);
85
86     internal char Get(int i, int j) {
87         if (i < 0 || i >= Rows || j < 0 || j >= Cols) {
88             throw new ArgumentOutOfRangeException($"Invalid index: {i},{j}");
89         }
90         return leds[i, j];
91     }
92
93     public override string ToString() {
94         var sb = new StringBuilder();
95         for (var i = 0; i < Rows; i++) {
96             for (var j = 0; j < Cols; j++) {
97                 sb.Append(leds[i, j]);
98             }
99             if (i < Rows - 1) {
```
