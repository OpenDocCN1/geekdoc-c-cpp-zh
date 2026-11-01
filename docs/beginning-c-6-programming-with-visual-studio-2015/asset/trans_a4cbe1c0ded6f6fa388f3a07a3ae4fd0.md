

- 将以下代码添加到 Farm.cs 中：

```
public class Farm<T> : IEnumerable<T> where T : Animal
{
  public void Add(T animal) => animals.Add(animal);
  ...
}
```

- 运行应用程序。结果如图 13-11 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_400_0.png)

图 13-11

## 工作原理

此示例将对象初始化器和集合初始化器组合在一起，通过一步操作创建并填充对象集合。它使用了你在前几章中见过的 farmyard 对象集合，不过为了让初始化器能用于这些类，需要做两处修改。

首先，你从派生自基类 Animal 的类中移除构造函数。可以移除这些构造函数，因为它们设置了动物的 Name 属性，而你将改用对象初始化器来设置该属性。或者，你也可以添加默认构造函数。无论哪种情况，使用默认构造函数时，Name 属性会根据基类中的默认构造函数进行初始化，其代码如下：

```
public Animal()
{
  name = "The animal with no name";
}
```

然而，当对象初始化器与派生自 Animal 的类一起使用时，请记住，初始化器设置的任何属性都是在对象实例化之后、也就是在基类构造函数执行之后才设置的。如果在对象初始化器中提供了 Name 属性的值，该值将覆盖这个默认值。在示例代码中，除了添加到集合中的一项外，其余所有项的 Name 属性都被设置了。

其次，你向 Farm 类添加了一个 Add() 方法。这是为了应对以下形式的一系列编译器错误：

```
'Ch13Ex04.Farm<Ch13Ex04.Animal>' does not contain a definition for 'Add'
```

该错误揭示了集合初始化器底层功能的一部分。在幕后，编译器会为你在集合初始化器中提供的每一项调用集合的 Add() 方法。Farm 类通过一个名为 Animals 的属性公开了一个 Animal 对象集合。编译器无法猜测这正是你想要填充的属性（通过 Animals.Add()），因此代码会失败。为了解决这个问题，你向该类添加了一个 Add() 方法，该方法通过对象初始化器进行初始化。

不过，你也可以使用标准数组初始化器来实现这一点：

```
var myArray = new int?[] { 4, null, 2 };
```

最后一点：标识符 var 并不是一个禁止用作类名的标识符。这意味着，例如，如果你的代码中有一个名为 var 的类在作用域内（在同一个命名空间或引用的命名空间中），那么你就不能使用 var 关键字进行隐式类型化。

就其本身而言，类型推断并不是特别有用，因为在本节你看到的代码中，它只会让事情变得更复杂。使用 var 会使你难以一眼看出给定变量的类型。但是，你将在本章后面看到，推断类型的概念很重要，因为它是其他技术的基础。下一个主题——匿名类型，就是一个必须使用推断类型的例子。

## 匿名类型

编程一段时间后，你可能会发现，尤其是在数据库应用程序中，你会花费大量时间创建简单、乏味的数据表示类。拥有一组除了公开属性之外什么都不做的类族是很常见的。本章前面展示的 Curry 类就是一个完美的例子：

```csharp
public class Curry
{
    public string MainIngredient { get; set; }
    public string Style { get; set; }
    public int Spiciness { get; set; }
}
```

这个类不执行任何操作——它只是存储结构化数据。用数据库或电子表格的术语来说，你可以将这个类视为表示表中的一行。一个能够容纳此类实例的集合类，则可以表示表或电子表格中的多行。

这是对类的完全可接受的使用方式，但编写这些类的代码可能会变得单调乏味，而且对底层数据模式的任何修改都要求你添加、删除或修改定义这些类的代码。

匿名类型是简化这种编程模型的一种方式。匿名类型背后的思想是，你可以不使用定义这些简单的数据存储类型，而是利用 C# 编译器根据你想要存储的数据自动创建类型。

前面的 Curry 类型可以按如下方式实例化：

```csharp
Curry curry = new Curry
{
    MainIngredient = "Lamb",
    Style = "Dhansak",
    Spiciness = 5
};
```

或者，你也可以使用匿名类型，如以下代码所示：

```csharp
var curry = new
{
    MainIngredient = "Lamb",
    Style = "Dhansak",
    Spiciness = 5
};
```

这里有两个区别。首先，使用了 var 关键字。这是因为匿名类型没有你可以使用的标识符。在内部，它们确实有一个标识符，你稍后会看到，但该标识符在你的代码中不可用。其次，new 关键字后面没有指定类型名称。这正是编译器知道你想要使用匿名类型的方式。

IDE 会检测匿名类型定义并相应地更新 IntelliSense。对于前面的声明，你可以看到匿名类型，如图 13-14 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_404_0.png)

图 13-14

在这里，变量 curry 的类型在内部是 `a`。显然，你不能在代码中使用这个类型——它甚至不是一个合法的标识符名称。这个 ` ` 只是 IntelliSense 中用来表示匿名类型的符号。IntelliSense 还允许你检查匿名类型的成员，如图 13-15 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_404_1.png)

图 13-15

请注意，这里显示的属性被定义为只读属性。这意味着如果你想在数据存储对象中更改属性的值，你不能使用匿名类型。

匿名类型的其他成员实现方式，将在下面的“试一试”中演示。

## 试一试 使用匿名类型：Ch13Ex05\Program.cs

- 创建一个名为 Ch13Ex05 的新控制台应用程序，并将其保存在目录 C:\BegVCSharp\Chapter13 中。

- 按如下方式修改 Program.cs 中的代码：

```csharp
static void Main(string[] args)
{
    var curries = new[]
    {
        new { MainIngredient = "Lamb", Style = "Dhansak", Spiciness = 5 },
        new { MainIngredient = "Lamb", Style = "Dhansak", Spiciness = 5 },
        new { MainIngredient = "Chicken", Style = "Dhansak", Spiciness = 5 }
    };
    WriteLine(curries[0].ToString());
    WriteLine(curries[0].GetHashCode());
    WriteLine(curries[1].GetHashCode());
    WriteLine(curries[2].GetHashCode());
    WriteLine(curries[0].Equals(curries[1]));
    WriteLine(curries[0].Equals(curries[2]));
    WriteLine(curries[0] == curries[1]);
    WriteLine(curries[0] == curries[2]);
    ReadKey();
}
```

- 运行应用程序。结果如图 13-16 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_405_0.png)

图 13-16

## 工作原理

在此示例中，你创建了一个匿名类型对象的数组，然后使用该数组对匿名类型提供的成员执行测试。创建匿名类型对象数组的代码如下：

```csharp
var curries = new[]
{
    new { MainIngredient = "Lamb", Style = "Dhansak", Spiciness = 5 },
    ...
};
```

这里使用了一个隐式类型化为匿名类型的数组，结合了本节和本章前面的“类型推断”部分的语法。结果是，curries 变量包含了匿名类型的三个实例。

创建此数组后，代码首先输出在匿名类型上调用 ToString() 的结果：

```
WriteLine(curries[0].ToString());
```

这会产生以下输出：

```
{ MainIngredient = Lamb, Style = Dhansak, Spiciness = 5 }
```

匿名类型中 ToString() 的实现会输出为该类型定义的每个属性的值。

接下来，代码对数组的三个对象分别调用 GetHashCode()：

```
WriteLine(curries[0].GetHashCode());
WriteLine(curries[1].GetHashCode());
WriteLine(curries[2].GetHashCode());
```

实现后，GetHashCode() 应根据对象的状态为对象返回一个唯一的整数。数组中的前两个对象具有相同的属性值，因此状态相同。这些调用的结果是这两个对象得到的整数相同，但第三个对象得到的整数不同。输出如下：

```
1789653062
1789653062
2116426892
```

接下来，调用 Equals() 方法，先比较第一个对象和第二个对象，再比较第一个对象和第三个对象：

```
WriteLine(curries[0].Equals(curries[1]));
WriteLine(curries[0].Equals(curries[2]));
```

结果如下：

```
True
False
```

匿名类型中 Equals() 的实现会比较对象的状态。如果一个对象的每个属性值与另一个对象上对应的属性值相同，则结果为 true。

然而，当你使用 == 运算符时，情况并非如此。如前面章节所示，== 运算符比较的是对象引用。最后一段代码执行了与上一段代码相同的比较，但使用的是 == 而不是 Equals()：

```
WriteLine(curries[0] == curries[1]);
WriteLine(curries[0] == curries[2]);
```

