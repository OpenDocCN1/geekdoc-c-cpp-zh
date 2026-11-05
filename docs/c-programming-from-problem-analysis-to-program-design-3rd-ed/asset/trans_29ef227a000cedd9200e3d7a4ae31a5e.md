
采用传引用方式时，内容不会被复制。会复制对数组存储位置的引用（地址），并将该副本存储在变量中。如图 7-7 所示，形式参数 temp 引用与 temperature 相同的内存位置。InputValues( ) 方法中输入到 temp 数组的值存储在 temperature 引用的内存单元中。

## 数组赋值

赋值运算符 = 在用于数组等引用类型时，可能不会像你想象的那样工作。如果定义了额外的数组并进行赋值，则赋值运算符和数组引用相同的元素。单个元素不会被复制到另一个内存位置。考虑在 temperature 数组填入值后可以编写的以下语句：

```csharp
int [ ] t = new int[5];
t = temperature;
t[1] = 44;
```

Figure 7-8 说明了赋值语句的结果。任何对 temperature[1] 的引用都会访问 44。

![](img/e33ae760e23d89eac66541252ad65de8_414_0.png)

Figure 7-8 将数组赋值以引用另一个数组

示例 7-13 包含了图 7-7 和图 7-8 中使用的程序语句的完整代码列表，其中说明了数组作为方法参数的赋值和使用。

### 示例 7-13

```csharp
/* PassingArray.cs    Author: Doyle
 * Demonstrates passing
 * arrays to methods - references
 */
using System;
namespace PassingArray
{
    class PassingArray
    {
        static void Main( )
        {
            int [ ] temperature = new int[5];
            int [ ] t = new int[5];

            InputValues(temperature);

            //Array t will reference the same array
            //as the temperature array.
            t = temperature;
            t[1] = 44;
            Console.WriteLine(temperature[1]);
        }

        public static void InputValues(int [ ] temp)
        {
            string inValue;

            for(int i = 0; i < temp.Length; i++)
            {
                Console.Write("Enter Temperature {0}: ", i + 1);
                inValue = Console.ReadLine( );
                temp[i] = int.Parse(inValue);
            }
        }
    }
}
```

## Params 参数

在第 3 章中，你曾简要了解过 params 参数类型。当方法使用 params 修饰符时，该参数被视为参数数组。它用于表示传递给方法参数的数量可能不同。

![](img/e33ae760e23d89eac66541252ad65de8_416_0.png)

如果在方法头中包含 params 参数，则与其一起使用的数组标识符必须是方法头中列出的最后一个参数。标识符不能定义为 ref 或 out 参数。

关键字 params 仅出现在方法头部的形式参数列表中。通过包含它，方法可以用单个值调用一次。另一次对同一方法的调用可以发送 10 或 100 个值或一个值数组。当包含 params 时，会接受可变数量的参数。这使得方法非常灵活。示例 7-14 显示了如何使用参数数组定义的方法既可以用简单的值参数调用，也可以用数组调用。

### 示例 7-14

```csharp
/* VaryingArguments.cs    Author: Doyle
 * This example demonstrates the use
 * of the params keyword. A varying
 * number of arguments can be sent
 * to a method.
 */
using System;
namespace VaryingArguments
{
    class VaryingArguments
    {
        public static void Main( )
        {
            DisplayItems(1, 2, 3, 5);
            int[] anArray = new int[5] {100, 200,
                                        300, 400, 500};
            DisplayItems(anArray);
            DisplayItems(1500, anArray[1] * anArray[2]);
        }
        public static void DisplayItems(params int[] item)
        {
            for ( int i = 0; i < item.Length; i++ )
            {
                Console.Write(item[i] + "\t");
            }
            Console.WriteLine( );
        }
    }
}
```

第一次调用 `DisplayItems()` 方法包含四个参数 (1, 2, 3, 5)。它们与 `(params int[] item)` 的 `DisplayItems()` 声明相匹配。第二次调用在方法调用期间发送一个数组作为参数。最后一次调用发送两个参数；第一个是 1500，一个常量字面量。最后一次调用的第二个参数是一个涉及 200 乘以 300 的表达式 (`anArray[1] * anArray[2]`)。该结果是一个整数；因此，当 `params` 关键字包含在参数列表中时，所有这些都是可接受的参数。产生的输出如下：

```
1       2       3       5
100     200     300     400     500
1500    60000
```

## 类中的数组

数组可以用作类中的字段或实例变量。通常，基础类型会与其他实例变量一起声明。但空间是在该类的对象被实例化时分配的。考虑 Player 类的以下数据成员列表。除了关于球员的描述性特征外，还定义了一个 pointsScored 数组。例如，球员在第一场比赛中可能得到 10 分，第二场得到 0 分，等等。

```csharp
public class Player
{
    private string lname;
    private string fname;
    private string id;
    private int[] pointsScored;
    private int numberOfGames;
    private double avg;
}
```

在定义 Player 类之后，可以使用任意数量的比赛和每场比赛的得分来实例化该类的对象。当你思考球员的特征时，你会意识到你不能说所有队员都打 50 场比赛或 5 场比赛；因此，pointsScored 数组不会为特定数量的比赛分配空间。因为这是实例成员，所以在构造类的对象时分配空间。这使得类更灵活，可供更多应用程序使用。

因为一名球员可能打了 50 场比赛，而另一名球员只打了 37 场，所以你需要知道要记录多少场比赛的得分。pointsScored[] 数组用于保存球员每场比赛的得分。除了默认构造函数外，还定义了一个构造函数，它接收多个参数，包括球员打的比赛场数。这是通过 numGames 变量从应用程序中作为参数传入的。因此，如果 numGames 的值为 10，则 pointsScored[] 数组的前 10 个元素将保存比赛计数（每场比赛一个）。构造函数包含所有实例变量的参数，除了平均值。这是计算得出的值。

构造函数的声明如下：

```csharp
public Player (string ln, string fn, string iden,
               int [ ] s, int numGames)
```

> 你可能会认为只需使用 `s.Length` 的值来确定比赛场数，而不必传入比赛场数参数。请记住，`Length` 返回维度元素的总数，即使是未使用的元素。`Length` 值并不表示有多少个元素是非零的。

使用 **numGames** 参数为 **pointsScored** 数组分配空间。以下 **Player** 成员方法被使用：

```csharp
public void FillPointsScoredArray(int [ ] s)
{
        pointsScored = new int [numberOfGames];
        for (int i = 0; i < pointsScored.Length; i++)
            pointsScored[i] = s[i];
}
```

在调用前述方法之前，必须构造 **Player class** 的一个 **object**。字段成员 **numberOfGames** 已经关联了一个值。`FillPointsScoredArray( )` 方法体中的第一条语句通过使用该实例字段成员为元素数量分配空间来实例化 **array object**。然后最后一条语句将传入方法中的数组 **s** 的元素复制到实例数组成员 **pointsScored**。

**s** 的长度不能用作循环控制变量，因为它不能准确指示发送到方法中的实际值数量。**Length** 是维度元素的数量，在使用 **Player class** 的应用程序中为 1000。请记住，创建类的目标之一是能够用不同的应用程序重用 **class**。当前的 **Player class** 确定球员的平均得分。可以编写额外的 方法来返回比赛场数、最高分和最低分、球员得分至少为 10 分的比赛场数等等。可以创建一个并行数组将 **pointsScored** 与对手名称关联起来。

**Parallel arrays** 是两个或多个具有关系的数组。该关系是通过使用相同的下标或索引来引用元素而建立的。例如，对手 X 的名称可能存储在 **string** 数组的索引位置 C 中。然后，球员对阵对手 X 的得分将存储在另一个数组的同一索引位置 C 中。并行数组在相关数据<|message|>
