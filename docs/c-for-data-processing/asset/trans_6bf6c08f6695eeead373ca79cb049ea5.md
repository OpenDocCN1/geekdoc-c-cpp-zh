

```csharp
using System;
class MethodDemo
{
    static void doit()
    {
        Console.WriteLine("Hello");
    }
    public static void Main()
    {
        doit();
        doit();
    }
}
```

在主方法中，我调用了两次 doit。每次调用该方法时，作为方法体的代码块中的代码就会执行。在本例中，它只包含一条语句，即在控制台上打印 "Hello"。运行上述程序的结果将是：

```
Hello
Hello
```

因此，我们可以使用方法避免重复编写相同的代码。只需将代码放入方法体中，然后在需要时调用它即可。

## 3.1.2 参数

此时，方法已经很有用，因为它们让我们可以在程序的许多位置使用相同的语句块。然而，如果允许方法带有参数，它们会变得更加有用。

参数是一种将值传入方法调用的手段。方法会获得需要处理的数据。例如，考虑下面的代码：

```csharp
using System;
class MethodDemo
{
    static void silly(int i)
    {
        Console.WriteLine("i is : " + i);
    }
    public static void Main()
    {
        silly(101);
        silly(500);
    }
}
```

方法 silly 有一个整数参数。在这个方法体的代码块中，我们可以将参数 i 当作整数变量使用。当方法开始时，为参数提供的值会被复制到该参数中。这意味着程序运行时我们会得到如下输出：

```
i is : 101
i is : 500
```

## 3.1.3 返回值

方法还可以向调用者返回值。你已经使用过这个特性，ReadLine 和 Parse 方法都会返回我们在程序中用过的结果：

```csharp
using System;

class ReturnDemo
{
    static int sillyReturnPlus(int i)
    {
        i = i + 1;
        Console.WriteLine("i is : " + i);
        return i;
    }

    public static void Main()
    {
        int res;
        res = sillyReturnPlus(5);
        Console.WriteLine("res is : " + res);
    }
}
```

sillyReturnPlus 方法接收参数的值，并返回该值加一。

方法返回的值可以在程序中任何使用该类型变量的地方使用。换句话说，调用 sillyReturnPlus 可以代替一个整数。看看你能否算出下面这段代码会显示什么：

```csharp
res = sillyReturnPlus(5) + sillyReturnPlus(7) + 1;
Console.WriteLine("res is : " + res);
```

实际上，忽略方法返回的值也是可以的，但这其实是一件毫无意义的事情：

```csharp
sillyReturnPlus(5); // 可以编译，但没有任何用处
```

## 3.1.4 一个有用的方法

现在我们可以开始编写真正有用的方法了：

```csharp
static double readValue(
    string prompt, // 向用户显示的提示
    double low,    // 允许的最小值
    double high    // 允许的最大值
)
{
    double result = 0;
    do
    {
        Console.WriteLine(prompt +
            " between " + low +
            " and " + high);
        string resultString = Console.ReadLine();
        result = double.Parse(resultString);
    } while ((result < low) || (result > high));
    return result;
}
```

readValue 方法被告知要使用的提示信息以及允许的最低值和最高值。然后它可以用来读取值并确保这些值在范围内。我们可以使用这个方法读取任何内容，并确保提供的值在特定范围内。

```csharp
double windowWidth = readValue(
    "Enter width of window: ", MIN_WIDTH, MAX_WIDTH);

double age = readValue("Enter your age: ", 0, 70);
```

第一次调用 readValue 获取窗口的宽度。第二次读取一个介于 0 到 70 之间的年龄。

### 程序员要点：用方法进行设计

方法是程序员工具箱中非常有用的部分。它们构成了开发过程的重要一环。一旦你弄清楚了客户的需求并收集了元数据，就可以开始考虑如何将程序分解为各个方法。通常你会发现，在编写代码时，你在重复某个特定的操作。如果是这样，你应该考虑将该操作提取出来，移入一个方法中。这是一个好主意，原因有两个：

- 1. 它避免你编写相同的代码两次。
- 2. 如果代码中发现错误，你只需在一个地方修复。

移动代码并创建方法被称为重构。这将在我们之后进行的软件工程中占据重要地位。

### 方法的局限性

方法非常擅长完成工作，但由于其工作方式，它可能会有些局限。例如，如果我想编写一个方法，读取一个人的姓名和年龄，就会遇到问题。从我们目前所见的方法来看，它们只能返回一个值。所以我可以编写一个返回人名的方法，或者编写一个返回年龄的方法。但我无法编写一个同时返回两个值的方法，因为方法只能返回一个值。当你尝试时你会发现，改变参数的值并不会改变传入的变量的值。这是因为，除非你另有指定，否则只有参数的值被传入方法调用中。

## 3.1.5 按值传递参数

那么，我说的“按值传递参数”是什么意思呢？考虑以下代码：

```csharp
static void addOneToParam(int i)
{
    i = i + 1;
    Console.WriteLine("i is : " + i);
}
```

方法 addOneToParam 给参数加一，打印结果，然后返回：

```csharp
int test = 20;
addOneToParam(test);
Console.WriteLine("test is : " + test);
```

上面这段 C# 代码以变量 test 作为参数调用该方法。运行时它会打印出如下内容：

```
i is : 21
test is : 20
```

理解这里发生的事情非常重要。在调用 addOneToParam 时使用的是 test 的值。程序会计算出作为参数传入方法调用的表达式的结果，然后将这个值传给调用。这意味着你可以编写如下调用：

```csharp
test = 20;
addOneToParam(test + 99);
```

这会打印出：

```
i is : 120
```

按值传递非常安全，因为方法所做的一切都不会影响调用它的代码中的变量。然而，当我们要创建一个返回多个值的方法时，这就成了限制。

## 3.1.6 按引用传递参数

*理解引用是如何工作的非常重要。如果你不理解这些，你就不能自称为合格的程序员！*

幸运的是，C# 提供了一种方式，不是将变量的值传入方法，而是提供对该变量的引用。在方法内部，不是使用变量的值，而是使用引用来获取实际的变量本身。实际上，传入方法的不是变量的内容，而是变量在内存中的位置或地址。

因此，在我们上面的调用中，编译器不会传入“20”，而是生成代码传入“内存位置 5023”（假设变量 test 实际存储在 5023）。方法使用这个内存位置，而不是值。换句话说：

> “如果按引用传递，对参数的修改会改变你传入引用的那个变量。”

如果你觉得引用令人困惑，你并不孤单。然而，我们在现实生活中一直在使用引用，而且毫无问题。如果你说“把地毯送到高街 23 号”，你就是在给送货员一个引用。在程序中使用引用也是如此。程序会说“从位置 5023 获取值”，而不是“值是 1”。

考虑以下代码：

```csharp
static void addOneToRefParam(ref int i)
{
    i = i + 1;
    Console.WriteLine("i is: " + i);
}
```

请注意，关键字 ref 已添加到参数信息中。

```csharp
test = 20;
addOneToRefParam(ref test);
Console.WriteLine("test is: " + test);
```

上面的代码调用了新方法，并且在参数前面也加了 ref 关键字。在这种情况下，输出如下：

```
i is 21
test is: 21
```

在这种情况下，方法调用修改了变量的内容。注意，C# 在参数是引用时会很谨慎。你必须在方法声明和调用方法时都加上 ref 关键字。

### 程序员要点：记录你的副作用

方法对其周围环境所做的更改称为方法的副作用。换句话说，当有人调用我们的 addOneToRefParam 方法时，它会产生“副作用”，即改变方法本身之外的一些东西（也就是按引用传递的参数的值）。

一般来说，你必须小心副作用，因为阅读你程序的人必须知道你的方法以这种方式做出了更改。

## 3.1.7 将参数作为“out”引用传递

当你将参数作为引用传递时，你是在赋予方法对它的完全控制权。有时你并不希望这样。相反，你只想允许方法改变变量。当我们想读取用户的姓名和年龄时就是这种情况。参数的原始值对方法来说无关紧要。相反，它只是想将结果传递给它们。在这种情况下，我可以将 ref 替换为关键字 out：

