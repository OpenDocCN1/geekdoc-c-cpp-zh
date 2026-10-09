
## 附录 B：完整代码列表

以下是我们在本书中介绍的所有代码示例列表。

你不需要在电脑上复制或输入这些代码来学习编程。你可以将时间用于更有意义的事情。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_564_0.png)

先阅读代码，并尝试理解它。然后，合上书，根据你的理解编写相同或类似的程序。你的程序不必与示例代码完全一致。

## 代码列表 - 第一部分

### 你好，世界

`hello-world-1/Program.cs`

```csharp
Console.WriteLine("Hello World!!");
```

`hello-world-2/Program.cs`

```csharp
const string name = "Joe";
var greeting = $"Hello {name}!!";

Console.WriteLine(greeting);
```

`hello-world-3/Program.cs`

```csharp
var name = "you";
if (args.Length > 0) {
    name = string.Join(" ", args);
}

Console.WriteLine($"Hello {name}!");
```

`hello-world-4/Program.cs`

```csharp
Console.WriteLine("What is your name?");
var name = Console.ReadLine();

if (string.IsNullOrWhiteSpace(name)) {
    name = "Friend";
} else {
    name = name.ToUpper();
}

var greeting = string.Format("Hello {0}! How are you?", name);
Console.WriteLine(greeting);
```

### 你好，世界（进阶）

`hello-universe-0/Program.cs`

```csharp
Console.WriteLine("Hello, World!");
```

`hello-universe-1/Program.cs`

```csharp
class Program {
    static void Main() => Console.WriteLine("Hello World!!");
}
```

`hello-universe-2/Program.cs`

```csharp
class Program {
    const string name = "Joe";
    static void Main() => Console.WriteLine($"Hello {name}!!!");
}
```

`hello-universe-3/Program.cs`

```csharp
class Program {
    static void Main(string[] args) {
        var name = "you";
        if (args.Length > 0) {
            name = string.Join(" ", args);
        }
        Console.WriteLine($"Hello {name}!");
    }
}
```

`hello-universe-4/Program.cs`

```csharp
class Program {
    static void Main() => Console.WriteLine(
        string.Format("Hello {0}! How are you?", ReadName())
    );

    static string? ReadName() {
        Console.WriteLine("What is your name?");
        var name = Console.ReadLine();

        if (string.IsNullOrEmpty(name)) {
            name = "Friend";
        } else {
            name = name.ToUpper();
        }

        return name;
    }
}
```

### 简单算术

`simple-arithmetic/Program.cs`

```csharp
using static System.Console;

var str = "C#" + "Language";
WriteLine($@"""C#" + "Language" = ""{str}""");

var sum = 1 + 2;
WriteLine($"1 + 2 = {sum}");

var sub = 5L - 2;
WriteLine($"5 - 2 = {sub}");

var prod = 1.0 * 5.0;
WriteLine($"1.0 * 5.0 = {prod}");

var div = 8.0F / 3.0;
WriteLine($"8.0 / 3.0 = {div:##}");

var money = 10.25M;
var dollars = decimal.Floor(money);
var cents = decimal.Subtract(money, dollars) * 100;
WriteLine($"$10.25 = {dollars} dollars and {cents:0} cents");

var (numer, denom) = (7, 2);
var (quotient, remainder) = (numer / denom, numer % denom);
WriteLine($"{numer} / {denom} = {quotient}");
WriteLine($"{numer} % {denom} = {remainder}");

var boolAnd = true && false;
var boolOr = true || false;
WriteLine($"t && f = {boolAnd}; t || f = {boolOr}");

var b1 = (byte)0b10;  // 00000010
var b2 = (byte)0b110; // 00000110
var bitAnd = (byte)(b1 & b2);
var bitOr = (byte)(b1 | b2);
var bitShift = (byte)(b2 << 2);
WriteLine($"b1 & b2 = {Fb(bitAnd)}; b1 | b2 = {Fb(bitOr)}; b2 << 2 = {Fb(bitShift)}");

// Returns an 8-bit pattern as a string for a given byte argument.
static string Fb(byte b) => $"{System.Convert.ToString(b, 2)}".PadLeft(8, '0');
```

### 闰年

`leap-year/Program.cs`

```csharp
using Example;

var isLeapYear = LeapYear1.IsLeapYear;

var years = new[] { 1900, 1984, 2000, 2022 };
foreach (var year in years) {
    var ans = isLeapYear(year);
    Console.WriteLine($"Is {year} a leap year? {(ans ? "Yes" : "No")}");
}
```

`leap-year/LeapYear.cs`

```csharp
namespace Example;

delegate bool IsLeapYear(int year);
```

`leap-year/LeapYear1.cs`

```csharp
namespace Example;

static class LeapYear1 {
    internal static bool IsLeapYear(int year) {
        if (year % 4 == 0) {
            if (year % 100 == 0) {
                if (year % 400 == 0) {
                    return true;
                } else {
                    return false;
                }
            } else {
                return true;
            }
        } else {
            return false;
        }
    }
}
```

`leap-year/LeapYear2.cs`

```csharp
namespace Example;

static class LeapYear2 {
    internal static bool IsLeapYear(int year) {
        if (year % 400 == 0) {
            return true;
        } else if (year % 100 == 0) {
            return false;
        } else if (year % 4 == 0) {
            return true;
        } else {
            return false;
        }
    }
}
```

`leap-year/LeapYear3.cs`

```csharp
namespace Example;

static class LeapYear3 {
    internal static bool IsLeapYear(int year) {
        if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
            return true;
        } else {
            return false;
        }
    }
}
```

### 乘法表

`multiplication-table/Program.cs`

```csharp
using Example;

const int low = 2;
const int high = 10;

Console.WriteLine("Multiplication Table:");
MultiplicationTable.WriteTable(low, high);
```

`multiplication-table/MultiplicationTable.cs`

```csharp
namespace Example;
using static System.Console;

static class MultiplicationTable {
  internal static void WriteTable(int low, int high) {
    var table = CreateTable(low, high);

    Write("     ");
    for (var v = low; v < high; v++) {
      Write($"{v,4}");
    }
    WriteLine("");

    Write("     --");
    for (var v = low; v < high; v++) {
      Write(" --");
    }
    WriteLine("");

    for (var l = low; l < high; l++) {
      Write($"{l,4}");
      Write("   |");
      for (var r = low; r < high; r++) {
        Write($"{table[l - low, r - low],4}");
      }
      WriteLine("");
    }
  }

  private static int[,] CreateTable(int low, int high) {
    var range = high - low;
    var table = new int[range, range];
    
    for (var l = low; l < high; l++) {
        for (var r = low; r < high; r++) {
            table[l - low, r - low] = l * r;
        }
    }
    
    return table;
  }
}
```

### 三十二进制数

`base32-numbers/Program.cs`

```csharp
using Example;

Console.Write("Input a number: ");
var input = Console.ReadLine();

if (int.TryParse(input, out int num)) {
    var base32Str = Base32.ToBase32(num);
    Console.WriteLine($"In base 32 = {base32Str}");
} else {
    Console.WriteLine($"Invalid number = {input}");
}
```

`base32-numbers/Base32.cs`

```csharp
namespace Example;

static class Base32 {
    private const int BASE = 32;

    internal static string ToBase32(int num) {
        var (number, flipped) = (num < 0) ? (-num, true) : (num, false);
        return (flipped ? "-" : "") + DivideAndAggregate(number);
    }

    private static string DivideAndAggregate(int n) {
        if (n < BASE) {
            return ConvertIntToChar(n).ToString();
        }
        
        var (v, r) = (n / BASE, n % BASE);
        var prefix = DivideAndAggregate(v);
        return prefix + ConvertIntToChar(r).ToString();
    }

    private static char ConvertIntToChar(int n) =>
        (n < 10) ? (char)(n + '0') : (char)(n - 10 + 'a');
}
```

### 出生日期

`birth-date/Program.cs`

```csharp
using Example;
var smiley = char.ConvertFromUtf32(0x1F642);
while (true) {
    Console.WriteLine("What is your birth date? (mm/dd/yyyy)");
    var input = Console.ReadLine();
    if (DateTime.TryParse(input, out DateTime date)) {
        var weekday = BirthDate.Weekday(date);
        Console.WriteLine($"You are a {weekday} child.");
        var days = BirthDate.AgeInDays(date);
        Console.WriteLine($"You are {days} days old as of today.");
        var (hours, mins) = BirthDate.AgeInHours(date);
        Console.WriteLine($"You are {hours} hours and {mins} minutes old as of right now. {smiley}");
        break;
    } else {
        Console.WriteLine("Invalid date. Try again? Yes (Y) or No (N)");
        var ans = Console.ReadLine() ?? "";
        var firstLetter = (ans.Length > 0) ? ans.Substring(0, 1).ToUpper() : "";
        switch (firstLetter) {
            case "Y":
                continue;
            case "N":
            default:
                Console.WriteLine($"Your loss! {smiley}");
                return;
        }
    }
}
```
