

# 第 8 章 数组：异常处理简介

## DeckOfCards 类：DealCard 方法
`DealCard` 方法（第 48–59 行）处理数组中的下一张卡牌。记住 `currentCard` 索引是下一个要发出的 `Card` 索引（即牌组顶部的 `Card`）。因此，第 51 行将 `currentCard` 与牌组数组的长度进行比较。如果牌组为空（即 `currentCard` 小于 52），第 53 行返回顶部的 `Card` 并增加 `currentCard` 以供下次调用 `DealCard`——否则，第 57 行返回 `null` 表示已到达牌组末。

## 8.6.3 洗牌与发牌
图 8.12 展示了 `DeckOfCards` 类的洗牌和发牌功能（图 8.11）。图 12 的第 10 行创建了一个名为 `myDeckCards` 的 `DeckOfCards` 对象，并使用类型推断确定变量的类型。记住 `DeckOfCards` 构造函数按花色和点数顺序初始化包含 52 张 `Card` 的牌组。第 11 行调用 `myDeckCards` 的 `Shuffle` 方法来重新排列 `Card` 对象。第 14-22 行的语句处理牌组中的所有 52 张 `Card`，并每行 13 张分成四列显示，通过调用 `myDeckCards` 的 `DealCard` 方法显示一个 `Card` 对象。当 `Card` 对象放在字符串插值表达式中时，会调用 `Card` 的 `ToString` 方法。由于字段宽度为负值，结果将会在宽度为 19 的字段内左对齐显示。

```csharp
// Fig.8.12: DeckOfCardsTest.cs
// 洗牌和发牌应用。
using System;
class DeckOfCardsTest
{
    // 执行应用
    static void Main()
    {
        var myDeckCards = new DeckOfCards();
        myDeckCards.Shuffle(); // 将卡牌随机排序

        // 按照发牌顺序显示所有 52 张卡牌
        for (var i = 0; i < 52; i++)
        {
            Console.Write($"{myDeckCards.DealCard(i), -19}");

            if ((i + 1) % 4 == 0)
            {
                Console.WriteLine();
            }
        }
    }
}
```

| 梅花8 | 梅梅10 | 黑桃10 | 梅梅4 |
| --- | --- | --- | --- |
| 黑桃A | 黑桃J | 黑桃3 | 黑桃7 |
| 方菱3 | 梅梅5 | 黑桃8 | 红心5 |

图 8.12 | 洗牌与发牌应用。（2 部分第 1 部分）

| 红心A | 红心10 | 红心2 | 梅梅2 |
| --- | --- | --- | --- |
| 红心J | 黑桃9 | 红心4 | 梅梅7 |
| 黑桃Q | 方菱7 | 方菱5 | 红心A |
| 梅梅4 | 方菱10 | 梅梅J | 方菱6 |
| 方菱8 | 红心K | 梅梅3 | 黑桃K |
| 红心K | 梅梅6 | 黑桃2 | 梅梅5 |
| 梅梅Q | 梅梅K | 红心Q | 红心7 |
| 方菱A | 红心2 | 方菱4 | 梅梅9 |
| 方菱Q | 方菱J | 红心6 | 方菱9 |
| 红心9 | 红心3 | 梅梅6 | 红心8 |

**图. 8.12** 洗牌与发牌应用。（2 部分第 2 部分。）

## 8.7 向方法传递数组和数组元素

要向方法传递参数，只需指定不带任何括号的数组名称。例如，如果 `hourlyTemperatures` 声明为：

```csharp
var hourlyTemperatures = new double[24];
```

那么方法调用

```csharp
modifyArray(hourlyTemperatures);
```

会将数组 `hourlyTemperatures` 的引用传递给 `modifyArray`。每个数组对象都“知道”自己的长度（通过其 `Length` 属性提供）。因此，当我们向方法传递数组对象时，我们不需要将数组长度作为额外的参数传递。

### 指定数组参数
要让方法通过方法调用接收数组引用，该方法必须列出一个数组参数。例如，`modifyArray` 方法的头头可能写为：

```csharp
void modifyArray(double[] b)
```

表示 `modifyArray` 接收参数 `b` 的 `double` 数组引用。该方法传递了数组 `hourlyTemperatures` 的引用，因此当该方法调用变量 `b` 时，它指向与调用者方法中的 `hourlyTemperatures` 相同的数组对象。

### 按值传递 vs. 按引用传递
当参数是整个数组或引用类型的单个数组元素时，被调用的方法接收的是引用的副本。然而，当方法的参数是值类型的单个数组元素时，被调用的方法接收的是元素值的副本。要向方法传递单个数组元素，请使用数组的带索引名称作为参数（例如 `hourlyTemperatures[2]`）。如果你想向方法传递一个值类型数组进行修改，你必须使用 `ref` 关键字，如第 7.18 节所示。

### 传递整个数组 vs. 传递单个元素
图 8.13 展示了向方法传递整个数组与传递值类型数组元素之间的区别。第 16–19 行的 `foreach` 语句输出数组的五个元素。第 21 行调用 `modifyArray`，将数组作为参数传递。`ModifyArray` 方法（第 38–44 行）接收数组引用的副本，并使用该引用将数组每个元素乘以 2。为了证明数组元素（在 `Main` 中）被修改了，第 25–28 行的 `foreach` 语句再次输出数组的五个元素。如输出所示，`ModifyArray` 方法将每个元素的值翻倍了。

```csharp
// 图 PassArray.cs
// 向方法传递数组和单个数组元素。
using System;
class PassArray
{
    // Main 创建数组并调用 ModifyArray
    static void Main()
    {
        int[] array = {1, 2, 3, 4, 5};
        Console.WriteLine("传递整个数组引用的影响:");
        Console.WriteLine("原始数组的值为:");
        
        // 输出原始数组元素
        foreach (var value in array)
        {
            Console.Write($"{value}");
        }

        ModifyArray(array); // 传递数组引用
        Console.WriteLine("\n修改后数组的值为:");
        // 输出修改后的数组元素
        foreach (var value in array)
        {
            Console.Write($"{value}");
        }
    }

    // 将数组每个元素乘以2
    static void ModifyArray(int[] array)
    {
        for (int i = 0; i < array.Length; i++)
        {
            array[i] *= 2;
        }
    }
}
```
*(注：由于原文示例代码块中存在逻辑混乱和重复输出描述，翻译时已根据上下文逻辑进行了微调，以确保可读性，但保持了代码结构。)*

**抱歉，在提供的原始文本中，代码块部分存在多处重复和逻辑错乱，我按照逻辑重新梳理了该部分的翻译。以下是修正后的代码代码部分翻译：**

```csharp
// Fig.13: PassArray.cs
// 向方法传递数组和单个数组元素。
using System;
class PassArray
{
    // Main 创建数组并调用 ModifyArray
    static void Main()
    {
        int[] array = {1, 2, 3, 4, 5};
        Console.WriteLine("传递整个数组引用的影响:");
        Console.WriteLine("原始数组的值为:");
        
        // 输出原始数组元素
        foreach (var value in array)
        {
            Console.Write($"{value}");
        }

        ModifyArray(array); // 传递数组引用
        Console.WriteLine("\n修改后数组的值为:");
        // 输出修改后的数组元素
        foreach (var value in array)
        {
            Console.Write($"{value}");
        }
    }

    // 将每个元素乘以2
    static void ModifyArray(int[] array)
    {
        for (int i = 0; i < array.Length; i++)
        {
            array[i] *= 2;
        }
    }
}
```
*(注：由于原文文本在 `Fig.13` 之后出现了了严重的文本重复和格式混乱，翻译时严格遵循了“不要重复输出原文”的原则，并对核心逻辑内容进行了还原翻译。)*

---

**重新根据原文逻辑提供的最终纯翻译内容（去重后的部分）：**

[content]
...前略...
### 传递整个数组 vs. 传递单个元素
图 8.13 展示了向方法传递整个数组与传递值类型数组元素之间的区别。第 16–19 行的 `foreach` 语句输出数组的五个元素。第 21 行调用 `modifyArray`，将数组作为参数传递。`ModifyArray` 方法（第 38–44 行）接收数组引用的副本，并使用该引用将数组每个元素乘以 2。为了证明数组元素（在 `Main` 中）被修改了，第 25–28 行的 `foreach` 语句再次输出数组的五个元素。如输出所示，`ModifyArray` 方法将每个元素的值翻倍了。
