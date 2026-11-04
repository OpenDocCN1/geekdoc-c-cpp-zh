
```
Index was outside the bounds of the array.
responses[9] == 14
```

| 评分 | 频数 |
|---|---|
| 1 | 3 |
| 2 | 4 |
| 3 | 8 |
| 4 | 2 |
| 5 | 2 |

**图 8.9** | 投票分析应用。（第 2 部分，共 2 部分。）

## *frequency* 数组

我们使用六元素数组 `frequency`（第 12 行）来统计每个响应出现的次数。每个元素用作一种可能的调查响应类型的计数器——`frequency[1]` 统计将食物评为 1 的学生人数，`frequency[2]` 统计将食物评为 2 的学生人数，依此类推。

### 8.5.1 汇总结果

第 16–28 行从数组 `responses` 中一次读取一个响应，并递增计数器 `frequency[1]` 到 `frequency[5]` 中的一个；我们忽略 `frequency[0]`，因为调查响应仅限于 1–5 的范围。循环中的关键语句位于第 20 行。该语句根据 `responses[answer]` 的值递增相应的频率计数器。

让我们逐步分析 foreach 语句的前几次迭代：

- 当计数器 answer 为 0 时，`responses[answer]` 的值是 `responses[0]` 的值（即 1——见第 10 行）。在这种情况下，`frequency[responses[answer]]` 被解释为 `frequency[1]`，并且 `frequency[1]` 递增 1。为了计算该表达式，我们从*最内层*括号中的值（answer，当前为 0）开始。将 answer 的值代入表达式，然后计算下一组括号（`responses[answer]`）。该值用作 frequency 数组的索引，以确定要递增哪个计数器（在本例中为 `frequency[1]`）。
- 下一次循环时，answer 为 1，`responses[answer]` 的值是 `responses[1]` 的值（即 2——见第 10 行），因此 `frequency[responses[answer]]` 被解释为 `frequency[2]`，从而使 `frequency[2]` 递增。
- 当 answer 为 2 时，`responses[answer]` 的值是 `responses[2]` 的值（即 5——见第 10 行），因此 `frequency[responses[answer]]` 被解释为 `frequency[5]`，从而使 `frequency[5]` 递增，依此类推。

无论调查中处理多少个响应，汇总结果都只需要一个六元素数组（其中我们*忽略*元素零），因为所有正确的响应值都在 1 到 5 之间，而六元素数组的索引值为 0–5。在图 8.9 的输出中，频数列只汇总了 responses 数组中 20 个值中的 19 个——数组 `responses` 的最后一个元素包含一个*不正确*的响应，该响应*未*被计入。第 16–28 行可以简化：将第 16 行改为

```
foreach (var response in responses)
```

将第 20 行改为

```
++frequency[response];
```

并修改第 25–26 行显示的错误消息。

### 8.5.2 异常处理：处理不正确的响应

异常表示程序执行期间发生的问题。异常处理使你能够创建容错程序，这些程序可以解决（或处理）异常。在许多情况下，这允许程序继续执行，就像没有遇到问题一样。例如，即使其中一个响应超出范围，Student Poll 应用仍然显示结果（图 8.9）。更严重的问题可能会阻止程序继续正常执行，转而要求程序向用户通知该问题，然后终止。当运行时或方法检测到问题时，例如无效的数组索引或无效的方法参数，它会抛出异常——也就是说，发生异常。这里的异常由运行时抛出。在 10.2 节中，你将看到如何抛出自己的异常。

### 8.5.3 try 语句

要处理异常，请将可能抛出异常的任何代码放在 try 语句中（图 8.9，第 18–27 行）。try 块（第 18–21 行）包含可能抛出异常的代码，catch 块（第 22–27 行）包含在发生异常时处理该异常的代码。你可以有多个 catch 块，以处理相应 try 块中可能抛出的不同类型的异常。当第 20 行正确递增 frequency 数组的某个元素时，第 22–27 行会被忽略。分隔 try 块和 catch 块主体的花括号是必需的。

### 8.5.4 执行 catch 块

当程序在 responses 数组中遇到值 14 时，它会尝试将 1 加到 frequency[14] 上，但 frequency[14] 不存在——frequency 数组只有六个元素。由于运行时执行数组边界检查，因此会生成异常——具体来说，第 20 行会抛出 IndexOutOfRangeException，以通知程序此问题。此时 try 块终止，catch 块开始执行——如果你在 try 块中声明了任何变量，它们将不再存在，因此在 catch 块中无法访问它们。

catch 块声明异常参数的类型（IndexOutOfRangeException）和名称（ex）。catch 块可以处理指定类型的异常。在 catch 块内部，你可以使用参数的标识符与捕获的异常对象交互。获取错误消息并显示它。消息显示后，异常被视为已处理，程序继续执行 catch 块右花括号之后的下一语句。在本例中，程序到达 foreach 语句的末尾（第 28 行），因此继续执行循环的下一次迭代。我们将在第 10 章再次使用异常处理，然后第 13 章会更深入地介绍异常处理。

**错误预防提示 8.1**

*在编写访问数组元素的代码时，请确保数组索引始终大于或等于 0 且小于数组的长度。这有助于防止程序中出现 IndexOutOfRangeExceptions。*

## 8.6 案例研究：洗牌与发牌模拟

到目前为止，本章的示例使用的都是值类型元素的数组。本节使用随机数生成和引用类型元素的数组——即表示扑克牌的对象——来开发一个模拟洗牌和发牌的类。然后，这个类可用于实现玩纸牌游戏的应用。

我们首先开发 Card 类（图 8.10），它表示一张扑克牌，具有牌面（例如 "Ace"、"Deuce"、"Three"、……、"Jack"、"Queen"、"King"）和花色（例如 "Hearts"、"Diamonds"、"Clubs"、"Spades"）。接下来，我们开发 DeckOfCards 类（图 8.11），它创建一副 52 张扑克牌，其中每个元素都是一个 Card 对象。然后，我们构建一个应用（图 8.12），它使用 DeckOfCards 类的洗牌和发牌功能。

### 8.6.1 Card 类与仅 Getter 的自动实现属性

Card 类（图 8.10）包含两个自动实现的字符串属性——Face 和 Suit——它们存储对特定 Card 的牌面值和花色名的引用。在 C# 6 之前，自动实现的属性需要同时具有 get 和 set 访问器。Face 和 Suit 被声明为 C# 6 的仅 getter 自动实现属性，客户端代码只能使用它们获取每个属性的值。此类属性为只读。仅 getter 自动实现属性只能在其声明中或该类型的所有构造函数中初始化。在声明中初始化自动实现属性是另一项 C# 6 功能，称为自动属性初始化器。为此，请在属性声明后加上 = 和初始值，如下所示

```
Type PropertyName { get; set; } = initializer;
```

你也可以在声明中初始化实例变量。

```
// Fig. 8.10: Card.cs
// Card class represents a playing card.
class Card
{
    private string Face { get; } // Card's face ("Ace", "Deuce", ...)
    private string Suit { get; } // Card's suit ("Hearts", "Diamonds", ...)

    // two-parameter constructor initializes card's Face and Suit
    public Card(string face, string suit)
    {
        Face = face; // initialize face of card
        Suit = suit; // initialize suit of card
    }
}
```

图 8.10 | Card 类表示一张扑克牌。（第 1 部分，共 2 部分。）

