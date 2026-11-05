
> 在使用已与另一个变量关联的名称声明局部变量时要谨慎。这通常会导致代码难以阅读，并且更难调试和维护。

与非返回值方法类似，一个或多个数据项可以作为参数传递给这类方法，如示例 3-16 所示。

### 示例 3-16

```csharp
public static double DeterminePrice(double squareYards,
    double pricePerSquareYard )
{
    return (pricePerSquareYard * squareYards);
}
```

对返回值方法的调用需要一个用于返回值的存储位置。如前所述，调用可以放在赋值语句、输出语句中，或任何可以使用值的地方。如果方法有参数，则调用中在括号内包含实际数据。因为在方法头中出现了 static 关键字，所以这些仍然被视为类方法。示例 3-15 和 3-16 中方法的调用如下：

```csharp
double roomLength;
roomLength = GetLength( );
Console.WriteLine(" Total cost of the carpet: {0:C}",
    DeterminePrice(squareYards, pricePerSquareYard));
```

如果将对非返回值方法的调用作为 Write( ) 或 WriteLine( ) 方法的参数放置，将会生成错误。这两个方法都期望从方法中接收回一个值以便显示该值。将对 DeterminePrice( ) 方法的调用作为 WriteLine( ) 方法的参数是合适的，因为 DeterminePrice( ) 方法返回一个 double。

示例 3-13 至 3-16 中出现的方法签名如下。签名由方法名、修饰符和形式参数类型组成。

```csharp
public static DisplayInstructions( );
public static DisplayResults(double, double);
public static GetLength( );
public static DeterminePrice(double, double);
```

使用 CarpetExampleWithClassMethods 类中引入的类方法完成的完整程序列表显示在示例 3-17 中。请注意，程序列表中没有 GetLength( ) 方法。相反，使用名为 GetDimension( ) 的方法来获取长度和宽度。该方法的头包含一个字符串参数，表示正在输入的是哪一侧、长度还是宽度。此方法被调用两次。第一次调用时字符串参数为“Length”，第二次调用时参数为“Width”。每次从 GetDimension( ) 方法返回的值都存储在不同的变量中。

![](img/e33ae760e23d89eac66541252ad65de8_187_0.png)

> 尽可能编写可重用的代码。通常，如果你在设计时多花一点精力思考，就能编写出通用解决方案并在以后获得收益。其简单示例就是编写一个方法 GetDimension( ) 来检索宽度和高度。它会被调用两次，使用不同的消息或参数。

### 示例 3-17

```csharp
/* CarpetExampleWithClassMethods.cs
 * Author: Doyle
 * Calculates the total cost of carpet. User
 * inputs room dimensions and carpet price.
 */
using System;
namespace CarpetExampleWithClassMethods
{
    public class CarpetWithClassMethods
    {
        public static void Main( )
        {
            double roomWidth;
            double roomLength;
            double pricePerSqYard;
            double noOfSqYards;

            DisplayInstructions( );

            // Call GetDimension( ) to get the length
            roomLength = GetDimension("Length");

            // Call GetDimension( ) again to get the
            // width
            roomWidth = GetDimension("Width");
            pricePerSqYard = GetPrice( );
            noOfSqYards =
                DetermineSqYards(roomWidth, roomLength);
            DisplayResults(noOfSqYards,
                pricePerSqYard);
        }

        public static void DisplayInstructions( )
        {
            Console.WriteLine("This program will "
                            + "determine how much "
                            + "carpet to purchase.");
            Console.WriteLine( );
            Console.WriteLine("You will be asked to "
                            + "enter the size of "
                            + "the room");
            Console.WriteLine("and the price of the "
                            + "carpet, in price per"
                            + " square yds.");
            Console.WriteLine( );
        }

        public static double GetDimension(string side )
        {
            string inputValue;       // local variables
            int feet,                // needed only by this
                inches;              // method

            Console.Write("Enter the {0} in feet: ",
                          side);
            inputValue = Console.ReadLine( );
            feet = int.Parse(inputValue);
            Console.Write("Enter the {0} in inches: ",
                          side);
            inputValue = Console.ReadLine( );
            inches = int.Parse(inputValue);

            // Note: cast required to avoid int division
            return (feet + (double) inches / 12);
        }

        public static double GetPrice( )
        {
            string inputValue;       // local variables
            double price;

            Console.Write("Enter the price per Square"
                        + "Yard: ");
            inputValue = Console.ReadLine( );
            price = double.Parse(inputValue);
            return price;
        }

        public static double DetermineSquareYards
                (double width, double length)
        {
            const int SQ_FT_PER_SQ_YARD = 9;

            double noOfSqYards;
            noOfSqYards = length * width
                          / SQ_FT_PER_SQ_YARD;

            return noOfSqYards;
        }

        public static double DeterminePrice
                (double squareYards,
                 double pricePerSquareYard)
        {
            return (pricePerSquareYard * squareYards);
        }

        public static void DisplayResults
                (double squareYards,
                 double pricePerSquareYard)
        {
            Console.WriteLine( );
            Console.Write("Square Yards needed: ");
            Console.WriteLine("{0:N2}", squareYards);
            Console.Write("Total Cost at {0:C}:",
                          pricePerSqYard);
            Console.WriteLine(" per Square Yard: "
                              + "{0:C}",
                              DeterminePrice(squareYards,
                                             pricePerSquareYard));
        }
    }
}
```

图 3-7 显示了当用户为长度输入 16 英尺 3 英寸、宽度输入 14 英尺 7 英寸、价格输入 14.95 时产生的输出。

![](img/e33ae760e23d89eac66541252ad65de8_190_0.png)

图 3-7 CarpetExampleWithClassMethods 的输出

请注意，图 3-7 的最后一行为“Press any key to continue.”。这是因为程序在 Visual Studio 中使用 Debug、Start Without Debugging 选项（Ctrl+F5）运行，而不是 Start Debugging 选项（F5）。这样做是为了在不将对 Read( ) 方法的额外调用作为 Main( ) 方法的最后一条语句添加的情况下保持输出屏幕。控制台窗口的屏幕背景和文本颜色是通过从命令窗口菜单中选择 Properties 选项更改的。

通过调用 Console.Clear( ) 方法清除输入提示。这会清除屏幕并将光标定位在左上角。

## 参数类型

到目前为止所介绍的使用参数的示例使用了值参数。C# 提供了按值调用和按引用调用参数。按值调用是默认类型。在按值调用中，会复制原始值并存储在单独的不同内存位置。如果方法更改了发送给它的变量的内容，这不会影响调用方法中变量存储的原始值。当控制权返回到调用方法时，原始值会被保留。C# 中还有另外三种参数类型：

- ref
- out
- params

params 参数将在第 7 章介绍数组时讨论。params 类型便于向方法发送可变数量的参数。其他两种 ref 和 out 现在很有用。之前你了解到，当调用方法时，只能通过返回类型接收一个数据类型返回。这对于通过方法名接收返回值同样成立。只能指定一种返回类型。然而，考虑一种情况，你可能编写一个方法允许用户输入多个值。如果只能将其中一个值返回给调用段，你将如何决定返回哪一个？其他值会怎样？如果需要方法返回多个值，则可以通过参数返回，特别是通过按引用调用参数。ref 和 out 关键字促进了这一过程。

ref 和 out 都导致方法引用传递给该方法的同一变量。与发送值参数时复制原始值并存储在不同内存位置的情况不同，使用 ref 或 out 时，方法可以访问原始内存位置。两个标识符，即调用方法中的标识符和方法中的标识符，都引用同一内存区域。当控制权返回到调用方法时，对方法中数据所做的任何更改都会反映在该变量中。

当使用 ref 和 out 关键字时，假定为按引用调用。在按引用调用中，你将参数的地址发送给方法。你必须在调用中以及方法头参数列表中都包含 ref 或 out。它们必须匹配。换句话说，你不能在头中使用 ref 而在调用中使用 out。这与 C++ 等语言不同，在这些语言中你只需要在方法头中指示引用参数。C# 中的实际调用也必须包含该关键字。

这些关键字的区别在于，除非在发送给方法之前原始参数已初始化，否则不能使用 ref 关键字。对于 out 不存在此限制。out 关键字对于允许用户在方法中输入变量值并在控制返回时使这些值在调用方法中可用的方法很有用。

> Java 没有引用参数。Java 的对象模拟按引用调用，但该语言不为其原始类型提供按引用调用。

value、ref 和 out 三种类型都在示例 3-18 中演示。

### 示例 3-18

```csharp
/* Parameters.cs
 * Author Doyle
 * This class demonstrates the
 * differences between the
 * default, ref, and out
 * parameter types */
using System;
namespace Parameters
```
