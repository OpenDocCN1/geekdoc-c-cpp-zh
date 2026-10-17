
```csharp
    } public interface IDisplay {
        void Clear();
    }

    public interface ILEDDisplay : IDisplay {
        void Show(Digit[] digits);
    }
```

在软件设计中，“抽象”是一种非常强大的策略，具有广泛的应用。使用接口来“抽象掉”实现细节是最常见的“抽象”策略之一。

为了具体性，在本课中，我们使用“伪”ASCII 显示。这些类型定义在 `LED.Ascii` 命名空间中。`Number` 记录是不可变的，就像 `Digit` 类型一样。

`led-clock-digital/Ascii/Number.cs` (lines 4-14)
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
`led-clock-digital/Ascii/Number.cs` (lines 61-104)
```csharp
    private static readonly Dictionary<Digit, Number> digits = new() {
        { Digit.Zero, Zero },
```
```csharp
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
            digits.ContainsKey(d) ? digits[d] : None;

75

76     private readonly char[,] leds;

77

78     private Number(char[,] leds) {

79         this.leds = leds;

80     }

81

82     internal int Rows => leds.GetLength(0);
83     internal int Cols => leds.GetLength(1);

84

85     internal char Get(int i, int j) {

86         if (i < 0 || i >= Rows || j < 0 || j >= Cols) {

87             throw new ArgumentOutOfRangeException($"Invalid index: {i},{j}");
88         }
89         return leds[i, j];
90     }

91

92     public override string ToString() {

93         var sb = new StringBuilder();
94         for (var i = 0; i < Rows; i++) {
95             for (var j = 0; j < Cols; j++) {
96                 sb.Append(leds[i, j]);
97             }
98             if (i < Rows - 1) {

```




sb.Append('\n');
}
}
return sb.ToString();
}

另一方面，我们还使用了一种可变类型 `Cell`，它相当于一个用于显示单个数字的显示面板。显然，在任意给定时刻，`Cell` 上的显示内容会根据要显示的实际数字而改变。

### `led-clock-digital/Ascii/Cell.cs` (第 3-34 行)

```csharp

sealed class Cell {

    private readonly char[,] leds;

    internal int RowCount => leds.GetLength(0);

    internal int ColCount => leds.GetLength(1);

    internal Cell() : this(Number.None) { }

    internal Cell(Number number) {

        leds = new char[number.Rows, number.Cols];

        Set(number);

    }

    internal char Get(int i, int j) {

        return leds[i, j];

    }

    internal void Set(Number number) {

        for (var i = 0; i < RowCount; i++) {

            for (var j = 0; j < ColCount; j++) {

                leds[i, j] = number.Get(i, j);

            }

        }

    }

    internal void Reset() {

        for (var i = 0; i < RowCount; i++) {

            for (var j = 0; j < ColCount; j++) {

                leds[i, j] = ' ';

            }

        }

    }

}

```

`Cells` 静态类包含一个扩展方法 `ToEnumerators()`，用于支持“二维”循环，该方法进而使用另一个扩展方法 `ToEnumerator(i)` 来处理每一行 `i`。

### `led-clock-digital/Ascii/Cells.cs` (第 3-20 行)

```csharp

static class Cells {

    internal static IEnumerable<IEnumerable<char>> ToEnumerators(this
        List<Cell> cells) {

        var r = cells[0].RowCount;

        for (var i = 0; i < r; i++) {

            yield return cells.ToEnumerator(i);

        }

    }

    private static IEnumerable<char> ToEnumerator(this List<Cell>
        cells, int i) {

        var len = cells.Count;

        var c = cells[0].ColCount;

        for (var j = 0; j < len * c; j++) {

            var (x, y) = (j / c, j % c);

            yield return cells[x].Get(i, y);

        }

    }

}

```

`LED.Ascii.Display` 类包含了在终端上显示数字的具体实现。

### `led-clock-digital/Ascii/Display.cs` (第 3-5 行)

```csharp

public abstract class Display : IDisplay {

    public abstract void Clear();

}

```

## 27.3. 代码示例 - led-clock-digital

### `led-clock-digital/Ascii/Display.cs` (第 7-41 行)

```csharp

public sealed class LEDDisplay : Display, ILEDDisplay {

    private readonly List<Cell> cells;

    public int Size => cells.Count;

    public LEDDisplay(int size) =>
        cells = Enumerable.Range(0, size).Select(i => new
        Cell(Number.None)).ToList() ?? new();

    public override void Clear() {

        cells.ForEach(c => c.Reset());

        Show();

    }

    private void Show() {

        foreach (var m in cells.ToEnumerators()) {

            foreach (var n in m) {

                Console.Write(n);

            }

            Console.WriteLine();

        }

    }

    public void Show(Digit[] digits) {

        var arr = digits.Select(d => Number.Convert(d)).ToList();

        for (var i = 0; i < Size; i++) {

            if (i < arr.Count) {

                cells[i].Set(arr[i]);

            } else {

                cells[i].Reset();

            }

        }

        Show();

    }

}

```

在此示例中需要注意的一点是，我们使用了“嵌套命名空间”。位于 `Ascii` 文件夹中的示例代码使用了以下文件范围命名空间声明：

```csharp

namespace LED.Ascii;

// ...

```

命名空间 `LED.Ascii` 被“包含”在命名空间 `LED` 中。在 C# 中，你可以使用任意数量的嵌套命名空间。这等价于：

```csharp

namespace LED.Ascii {

    // ...

}

```

进而（根据 C# 正式语法）这等价于：

```csharp

namespace LED {

    namespace Asci i {

        // ...

    }

}

```

通过使用文件范围命名空间（从 C# 10.0 开始可用），我们“节省”了左侧宝贵的空间。（请注意每个命名空间声明中代码主体 (...) 的缩进。）

## 第 28 课 魔方

### 28.1. 问题

魔方在 20 世纪 70 年代初问世时风靡一时。它至今在儿童以及许多爱好者和“速拧者”中依然非常流行。参见 [魔方](https://en.wikipedia.org/wiki/Rubik%27s_Cube)。

这是一个非常有趣的谜题。虽然并不十分“复杂”，但在脑海中对其进行可视化仍然非常困难。正如我们稍后将看到的，魔方所有可能配置的构成的空间具有*三维环面* [https://en.wikipedia.org/wiki/Torus] 的拓扑结构。

现在的问题是，如何在程序中“表示”魔方的配置？特别是，在本课中，我们将处理“打乱”魔方或随机化其配置的问题。

魔方的每一面都可以旋转 90、180 和 270 度。180 度和 270 度旋转可以分别视为两次和三次 90 度旋转。然而，在魔方玩家中，通常将 90 度和 270（-90）度旋转视为两种不同的移动。180 度旋转仍然可以视为其中一种旋转的两步移动。

魔方有六个侧面或“面”（毕竟它是个立方体），因此，从任何给定的配置出发，我们可以执行 12 种移动之一：对 6 个面中的某一个进行顺时针或逆时针 90 度旋转。

6 个面中的每一个都与一种颜色相关联：白色 `W`、蓝色 `B`、红色 `R`、绿色 `G`、橙色 `O` 和黄色 `Y`。白色面和黄色面位于立方体的相对两侧。蓝色面和绿色面位于相对两侧。红色面和橙色面位于相对两侧。

在二维表面上表示三维物体很难，但魔方可以如下绘制：

如果我们把立方体放在表面上，并从顶部向下看，我们会看到白色面，且四个侧面分别是 `G`、`R`、`B` 和 `O`。黄色面位于底部。

立方体面上每个小块被称为“块”。共有 54 个块，即 6 乘以 9（3 乘 3）。有 6 个中心块，12 个棱块，和 8 个角块。

$$54 = 1\times6 + 2\times12 + 3\times8$$

请注意，并非所有块都是独立的。实际上，魔方中只有 26 个独立的部分。6 个中心块是不可移动的。12 个棱块由两个块组成，因此有两种颜色。8 个角块由三个不同颜色的块组成。

> 如果您手头恰好有一个魔方，此时查看一下其中一个可能很有用。

> “阅读”程序比“编写”程序难一个数量级。本课程的示例代码可能对你来说难以阅读和理解。如果你觉得阅读太难，可以跳过这一课。但是，如果你希望挑战最终项目，*魔方挑战*，那么本课中的信息可能会非常有用。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_455_0.png)

### 28.2. 讨论

魔方是一个“真实”的物体。现实世界中的一个物体。它具有状态（例如，哪些块具有哪些颜色）。它有一些允许的操作，例如旋转一个面。

这是一个理想（现实世界）对象，可以作为“对象”（面向对象编程意义上的对象）来表示。魔方具有状态（例如，如所述 54 个块的颜色）。并且，改变其状态的唯一方式是通过一组定义良好的接口（例如，如所述将各面顺时针或逆时针旋转 90 度）。

面向对象编程（OOP）的所有对象都有状态和接口。对于我们开发人员来说，挑战在于在程序中找到现实世界对象的“良好”表示法。（“良好”可能因需求不同而有不同的含义。）

鼓励读者在阅读示例代码之前思考这个问题。首先，我们要做什么？然后，实现我们目标的最佳方式（或“足够好”的方式）是什么？面向对象会有帮助吗？如果有，如何？等等。

（了解继承/多态以及面向对象的几乎所有技术细节，若不懂面向对象编程的基本概念，将意义不大。）

### 28.3. 示例代码片段 - rubiks-cube

主程序测试了一些针对 Rubik's cube 的操作。

**`rubiks-cube/Program.cs`** (lines 5-6)

```csharp

5  var c = new Cube();

6  Console.WriteLine($"c =\n{c}");

```

**`rubiks-cube/Program.cs`** (lines 11-39)

```csharp

11 c.RotateWhite();

12 Console.WriteLine($"c =\n{c}");

13 c.RotateWhite(false);

14 Console.WriteLine($"c =\n{c}");

15

16 c.RotateBlue();

17 Console.WriteLine($"c =\n{c}");

18 c.RotateBlue(false);

19 Console.WriteLine($"c =\n{c}");

20

21 c.RotateRed();

22 Console.WriteLine($"c =\n{c}");

23 c.RotateRed(false);

24 Console.WriteLine($"c =\n{c}");

25

26 c.RotateGreen();

27 Console.WriteLine($"c =\n{c}");

28 c.RotateGreen(false);

29 Console.WriteLine($"c =\n{c}");

30

31 c.RotateOrange();

32 Console.WriteLine($"c =\n{c}");

33 c.RotateOrange(false);

34 Console.WriteLine($"c =\n{c}");

35

36 c.RotateYellow();

37 Console.WriteLine($"c =\n{c}");

38 c.RotateYellow(false);

39 Console.WriteLine($"c =\n{c}");
```
