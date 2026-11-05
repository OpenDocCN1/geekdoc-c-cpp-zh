
```
public double DetermineTotalCost( )
{
    return (pricePerSqYard * noOfSqYards);
}
// One of the overloaded mutator methods
public void SetNoOfSqYards(double length,
                           double width)
{
    const int SQ_FT_PER_SQ_YARD = 9;

    noOfSqYards = length * width
                 / SQ_FT_PER_SQ_YARD;
}
// One of the overloaded mutator methods
public void SetNoOfSqYards
            (double squareYards)
{
    noOfSqYards = squareYards;
}
// Accessor method
public double GetNoOfSqYards( )
{
    return noOfSqYards;
}
public override string ToString( )
{
    return "Price Per Square Yard: " +
           pricePerSqYard.ToString("C") +
           "\nTotal Square Yards: " +
           noOfSqYards.ToString("F1") +
           "\nTotal Price: " +
           DetermineTotalCost().ToString("C");
}
}
```

以下文件使用了 CarpetCalculator 类：

```
/* CarpetCalculatorApp.cs
 * Author: Doyle
 * This class instantiates an object
 * of the CarpetCalculator class. It
 * demonstrates how to access and use
 * the members of the class.
 */
using System;
namespace Carpet
{
    public class CarpetCalculatorApp
    {
        public static void Main( )
        {
            CarpetCalculator berber =
                new CarpetCalculator(17.95);
            double roomWidth;
            double roomLength;
            DisplayInstructions( );
            // Call GetDimension( ) to get the length
            roomLength = GetDimension("Length");
            // Call GetDimension( ) again to get the width
            roomWidth = GetDimension("Width");
            berber.SetNoOfSqYards
                (roomLength, roomWidth);
            berber.PricePerSqYard = 25.99;
            Console.Clear( );
            Console.Write(berber);
            Console.ReadLine();
        }
        static void DisplayInstructions( )
        {
            Console.WriteLine("This program will"
                + " determine how much "
                + "carpet to purchase.");
            Console.WriteLine( );
            Console.WriteLine("You will be asked to "
                + "enter the size of the "
                + "room and the price of the");
            Console.WriteLine("carpet, in price per "
                + "square yds.");
            Console.WriteLine( );
        }
        static double GetDimension(string side)
        {
            string inputValue;    // local variables
            int feet,             // needed only by this
                inches;           // method
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
    }
}
```

在回顾示例 4-18 时，注意 CarpetCalculator 类中定义了一个名为 PricePerSqYard 的属性。该属性与 pricePerSqYard 数据成员相关联，而该数据成员以 private 访问模式定义。回想一下，数据成员使用驼峰命名法命名，而属性标识符遵循帕斯卡命名法约定；因此，它们名称的唯一区别在于第一个字符。pricePerSqYard 可以在定义它的类中引用，但由于它以 private 访问模式定义，因此不能在定义类之外引用。

在第二个类 CarpetCalculatorApp 中，实例化了 CarpetCalculator 类的一个对象。对象标识符为 berber。该对象使用 new 运算符实例化，如下所示：

~~~
CarpetCalculator berber = new CarpetCalculator(17.95);
~~~

由于将 double 值 17.95 作为参数发送给构造函数，因此使用单参数构造函数。17.95 传入 price，并且该值被放入私有数据成员 pricePerSqYard，如下面的构造函数所示：

~~~
public CarpetCalculator(double price)
{
    pricePerSqYard = price;
}
~~~

为了在 CarpetCalculatorApp 类中更改 berber 的 pricePerSqYard，必须使用属性 PricePerSqYard。私有 pricePerSqYard 数据成员在第二个类中不可访问。通过下面所示的语句将 pricePerSqYard 更改为 25.99：

~~~
berber.PricePerSqYard = 25.99;
~~~

PricePerSqYard 属性具有 get 和 set 子句。为了使实例化 CarpetCalculator 类对象的类能够更改对象的 PricePerSqYard，它们使用与该公共属性关联的 set 子句。对象的私有数据成员的值（即 pricePerSqYard）通过公共属性的 get 子句检索。

接下来，在 CarpetCalculatorApp 类的 Main( ) 方法中，调用了修改器方法 SetNoOfSqYards( )。注意，此方法与上面的属性引用一样，必须通过对象调用。它同样提供公共访问模式；因此，它在实例化 CarpetCalculator 类对象的类中可用。本例中的对象是 berber。本可以为 noOfSqYards 定义公共属性，而不是修改器方法。公共属性 NoOfSqYards 将与私有 noOfSqYards 数据成员关联。

示例 4-18 的 Main( ) 中最后一个值得注意的语句是 Console.Write (berber) 语句。这里，CarpetCalculator 类中定义的 ToString ( ) 方法会随 berber 对象自动调用。CarpetCalculator 类为该对象的 ToString ( ) 方法提供了新定义。关键字 override 用在 CarpetCalculator 类的方法标头上。

图 4–7 显示了当用户输入房间长度为 17 英尺 10 英寸、宽度为 14 英尺 6 英寸时，上述应用程序的输出。

![](img/e33ae760e23d89eac66541252ad65de8_246_0.png)

**图 4–7**  使用实例方法的 Carpet 示例输出

本章介绍了大量内容。接下来的编程示例将使用其中的大多数新概念。

## 编程示例：REALESTATEINVESTMENT（房地产投资）

本示例演示了方法在程序中的使用。其中同时使用了静态方法和实例方法。解决方案中包含了 C# 新增的属性。问题说明如图 4-8 所示。

租赁投资产生了多少现金流利润？创建一个应用程序，以确定用作租赁的房地产投资的现金流。

设计一个面向对象的解决方案。使用两个类。

对于房地产物业类，房屋建造年份、购买价格和街道地址等特征将有助于标识对象的当前状态。房地产对象还具有每月租金收入金额和每月支出特征。包含一个方法，根据从每月租金收入中扣除每月总支出，确定每月收益或现金流。

在第二个类中，实例化房地产物业类的一个对象。调用使用建造年份、购买价格和街道地址创建对象的构造函数。允许用户输入年度税费和保险费用。还应考虑每月公用事业费用。在此应用程序类中，根据输入值计算每月支出。设置房地产物业对象中的相应数据字段。

在应用程序类中编写代码，以显示物业地址和给定月份的预期现金流。

图 4-8 RealEstateInvestment 示例的问题说明

## 分析问题

应回顾图 4-8 中的问题说明，并确保理解问题定义。必须向程序中输入多个值。这些值必须作为 `string` 变量输入，然后解析为数值字段，以便执行算术运算。

将开发两个独立的类。为房地产 `object` 创建一个单独的 `class`，可使该 `class` 被许多不同的应用程序使用。一个应用程序是生成显示该投资现金流的清单。其他应用程序可能包括确定总投资金额或投资地点。如果房地产对象的特征被抽象出来，许多应用程序都可以重用该 `class`。

## 变量

表 4-2 和表 4-3 列出了 RealEstateInvestment 问题所需的数据项。

### 表 4-2 RealEstateInvestment 类的实例变量

| 数据项说明 | 类型 | 标识符 |
|---|---|---|
| 房屋建造年份 | `int` | yearBuilt |
| 房屋位置 | `string` | streetAddress |
| 原始购买价格 | `double` | purchasePrice |
| 平均每月总支出 | `double` | monthlyExpense |
| 每月租金收入 | `double` | incomeFromRent |

使用 RealEstateInvestment `class` 的 `class` 也需要数据。如问题说明所述，应用程序 `class` 允许用户输入支出值。表 4-3 标识了应用程序 `class` 所需的一些局部变量。

### 表 4-3 物业应用程序类的局部变量

| 数据项说明 | 类型 | 标识符 |
|---|---|---|
| 每年保险费用 | `double` | insurance |
| 每年税费金额 | `double` | taxes |
| 估计每月公用事业费用 | `double` | utilities |
| 用于输入值的字符串值 | `string` | inValue |

## 常量

租赁费率设置为常量值。标识符和预设常量值将为 `RENTAL_AMOUNT = 1000.00`。
