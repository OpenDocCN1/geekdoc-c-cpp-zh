

> > **注意** 有趣的是，两个 short 值相乘并不会返回 short 值。因为这个运算的结果很可能超过 32767（short 可以容纳的最大值），所以它实际上返回 int。
> >
> > 转换过程乍一看似乎很复杂，但只要按照运算符优先级顺序将表达式分解成各个部分，你应该就能弄明白。

## 复杂变量类型

除了所有简单变量类型之外，C# 还提供了三种稍微复杂一些（但非常有用）的变量类型：枚举（通常称为 enums）、结构（有时称为 structures）和数组。

### 枚举

到目前为止，你见过的每种类型（`string` 除外）都有一组明确定义的允许值。诚然，在 double 这样的类型中，这个集合非常大，实际上可以视为一个连续区间，但它仍然是一个固定集合。最简单的例子是 bool 类型，它只能取两个值之一：`true` 或 `false`。

在许多其他情况下，你可能希望有一个变量能够从一组固定的结果中取一个值。例如，你可能希望有一个方向（orientation）类型，可以存储 north、south、east 或 west 中的一个值。

在这种情况下，*枚举*会非常有用。枚举在方向类型中正是你想要的：它们允许定义一个类型，该类型可以取你提供的有限值集合中的一个值。因此，你需要做的是创建你自己的枚举类型 orientation，它可以取四个可能值之一。

请注意，这里还涉及一个额外的步骤——你不仅仅声明一个给定类型的变量；你需要声明并详细定义一个用户自定义类型，然后再声明一个这种新类型的变量。

### 定义枚举

可以使用 enum 关键字按下述方式定义枚举：

```
enum <typeName>
{
    <value1>,
    <value2>,
    <value3>,
    ...
    <valueN>
}
```

请注意，这样可能会导致问题，例如在定义之后指定的值（如 <value2> = <value1>）与其他值相同。例如，在下面的代码中，<value4> 将与 <value2> 具有相同的值：

```
enum <typeName> : <underlyingType>
{
    <value1> = <actualVal1>,
    <value2>,
    <value3> = <value1>,
    <value4>,
    ...
    <valueN> = <actualValN>
}
```

当然，如果这正是你想要的行为，那么这段代码没有问题。另外请注意，以循环方式赋值会导致错误：

```
enum <typeName> : <underlyingType>
{
    <value1> = <value2>,
    <value2> = <value1>
}
```

下面的“试一试”演示了所有这些内容的一个示例。该代码定义并使用了一个名为 orientation 的枚举。

### 试一试 使用枚举：Ch05Ex02\Program.cs

- 1. 创建一个名为 Ch05Ex02 的新控制台应用程序，并将其保存到目录 C:\BegVCSharp\Chapter05 中。
- 2. 将以下代码添加到 Program.cs 中：

```
namespace Ch05Ex02
{
    enum orientation : byte
    {
        north = 1,
        south = 2,
        east = 3,
        west = 4
    }
    class Program
    {
        static void Main(string[] args)
        {
            orientation myDirection = orientation.north;
            WriteLine($"myDirection = {myDirection}");
            ReadKey();
        }
    }
}
```

### 定义结构

结构使用 struct 关键字按下述方式定义：

```
struct <typeName>
{
    <memberDeclarations>
}
```

<memberDeclarations> 部分包含变量声明（称为结构的数据成员），其格式与通常情况几乎相同。每个成员声明采用以下形式：

```
<accessibility> <type> <name>;
```

为了允许调用结构的代码访问结构的数据成员，可以为 <accessibility> 使用关键字 public。例如：

```
struct route
{
    public orientation direction;
    public double      distance;
}
```

定义好结构类型后，可以通过定义新类型的变量来使用它：

```
route myRoute;
```

此外，你可以通过句点字符访问这个复合变量的数据成员：

```
myRoute.direction = orientation.north;
myRoute.distance  = 2.5;
```

下面的“试一试”演示了这一点，其中使用了上一个“试一试”中的 orientation 枚举以及前面展示的 route 结构。然后在代码中操作该结构，让你感受结构的工作方式。

### 试一试 使用结构：Ch05Ex03\Program.cs

- 1. 创建一个名为 Ch05Ex03 的新控制台应用程序，并将其保存到目录 C:\BegVCSharp\Chapter05 中。
- 2. 将以下代码添加到 Program.cs 中：

```
namespace Ch05Ex03
{
    enum orientation: byte
    {
        north = 1,
        south = 2,
        east = 3,
        west = 4
    }
    struct route
    {
        public orientation direction;
        public double distance;
    }
    class Program
    {
        static void Main(string[] args)
        {
            route myRoute;
            int myDirection = -1;
            double myDistance;
            WriteLine("1) North\n2) South\n3) East\n4) West");
            do
            {
                WriteLine("Select a direction:");
                myDirection = ToInt32(ReadLine());
            }
            while ((myDirection < 1) || (myDirection > 4));
            WriteLine("Input a distance:");
            myDistance = ToDouble(ReadLine());
            myRoute.direction = (orientation)myDirection;
            myRoute.distance = myDistance;
            WriteLine($"myRoute specifies a direction of {myRoute.direction} " +
            $"and a distance of {myRoute.distance}");
            ReadKey();
        }
    }
}
```

- 3. 执行代码，输入 1 到 4 之间的数字选择一个方向，然后输入一个距离。结果如图 5-7 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_118_0.png)

图 5-7

### 工作原理

结构（struct）与枚举一样，在代码主体之外声明。你的 route 结构就声明在 namespace 声明内部，并与其使用的 orientation 枚举一同声明：

```
enum orientation: byte
{
    north = 1,
    south = 2,
    east = 3,
    west = 4
}
```

此外，如果你愿意，可以组合使用这两种初始化方法：

```csharp
int[] myIntArray = new int[5] { 5, 9, 10, 2, 99 };
```

使用这种方法时，大小必须匹配。例如，你不能编写以下代码：

```csharp
int[] myIntArray = new int[10] { 5, 9, 10, 2, 99 };
```

这里，数组被定义为有 10 个成员，但只定义了 5 个，所以编译会失败。这带来的一个副作用是，如果你使用变量来定义大小，那么该变量必须是常量：

```csharp
const int arraySize = 5;
int[] myIntArray = new int[arraySize] { 5, 9, 10, 2, 99 };
```

如果省略 const 关键字，这段代码将无法编译。

与其他变量类型一样，不需要在声明数组的同一行对其进行初始化。下面这样做完全合法：

```csharp
int[] myIntArray;
myIntArray = new int[5];
```

在下面的“试一试”中，你将使用本节引言中的示例创建并使用一个字符串数组。

### 试一试 使用数组：Ch05Ex04\Program.cs

- 1. 创建一个名为 Ch05Ex04 的新控制台应用程序，并将其保存到目录 C:\BegVCSharp\Chapter05 中。
- 2. 将以下代码添加到 Program.cs 中：
- 3. 执行代码。结果如图 5-8 所示。

```csharp
static void Main(string[] args)
{
    string[] friendNames = { "Todd Anthony", "Kevin Holton",
        "Shane Laigle" };
    int i;
    WriteLine($"Here are {friendNames.Length} of my friends:");
    for (i = 0; i < friendNames.Length; i++)
    {
        WriteLine(friendNames[i]);
    }
    ReadKey();
}
```

![](img/cf72ea860016d2d680fc085fc06f265a_121_0.png)

