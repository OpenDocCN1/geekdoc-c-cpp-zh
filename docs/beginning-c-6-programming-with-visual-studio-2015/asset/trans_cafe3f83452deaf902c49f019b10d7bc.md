

其次，必须使用已初始化的变量。C# 不允许你假设 ref 参数会在使用它的函数中被初始化。下面的代码同样是非法的：

```
int myNumber;
ShowDouble(ref myNumber);
WriteLine("myNumber = {myNumber}");
```

## Out 参数

除了按引用传递值之外，你还可以使用 `out` 关键字将给定参数指定为 out 参数，其使用方式与 `ref` 关键字相同（作为函数定义和函数调用中参数的修饰符）。实际上，这提供的行为与引用参数几乎完全相同：函数执行结束时参数的值会返回给函数调用中使用的变量。不过，两者之间存在重要差异：

- 将未赋值的变量用作 `ref` 参数是非法的，但你可以将未赋值的变量用作 `out` 参数。
- `out` 参数必须被使用它的函数视为未赋值的值。

这意味着，虽然调用代码可以将已赋值的变量用作 `out` 参数，但该变量中存储的值会在函数执行时丢失。

举个例子，考虑前面展示的 `MaxValue()` 函数的一个扩展版本，该函数返回数组的最大值。稍微修改该函数，使其获得数组中最大值元素的索引。为了简单起见，当有多个元素具有最大值时，只获取该值第一次出现的索引。为此，你通过按如下方式修改函数来添加一个 out 参数：

```
static int MaxValue(int[] intArray, out int maxIndex)
{
    int maxVal = intArray[0];
    maxIndex = 0;
    for (int i = 1; i < intArray.Length; i++)
    {
        if (intArray[i] > maxVal)
        {
            maxVal = intArray[i];
            maxIndex = i;
        }
    }
    return maxVal;
}
```

你可以像这样使用该函数：

```
int[] myArray = { 1, 8, 3, 6, 2, 5, 9, 3, 0, 2 };
int maxIndex;
WriteLine($"The maximum value in myArray is {MaxValue(myArray, out maxIndex)}");
WriteLine($"The first occurrence of this value is at element {maxIndex + 1}");
```

结果如下：

```
The maximum value in myArray is 9
The first occurrence of this value is at element 7
```

与 `ref` 关键字一样，你必须在函数调用中使用 `out` 关键字。

## 变量作用域

在上一节中，你可能一直想知道为什么需要与函数交换数据。原因是 C# 中的变量只能从代码的局部区域进行访问。一个给定的变量被认为具有一个作用域，在这个作用域内它可以被访问。

变量作用域是一个重要的主题，最好通过示例来介绍。下面的“试一试”演示了一种情况：一个变量在一个作用域中定义，却尝试在另一个作用域中使用它。

### 试一试 变量作用域：使用 Ch06Ex01\Program.cs

1. 对之前创建的 Program.cs 中的 Ch06Ex01 进行以下修改：

```
class Program
{
    static void Write()
    {
        WriteLine($"myString = {myString}");
    }
    static void Main(string[] args)
    {
        string myString = "String defined in Main()";
        Write();
        ReadKey();
    }
}
```

2. 编译代码并注意错误列表中出现的错误和警告：

```
The name 'myString' does not exist in the current context
The variable 'myString' is assigned but its value is never used
```

### 工作原理

哪里出了问题？好吧，在主应用程序主体（`Main()` 函数）中定义的变量 `myString` 无法从 `Write()` 函数中访问。

无法访问的原因是变量具有其有效的范围。该范围包括变量定义所在的代码块以及任何直接嵌套的代码块。函数中的代码块与调用它们的代码块是分离的。在 `Write()` 内部，名称 `myString` 是未定义的，而在 `Main()` 中定义的 `myString` 变量超出了作用域——它只能在 `Main()` 内部使用。

```
WriteLine("Now in Write()");
WriteLine($"Local myString = {myString}");
WriteLine($"Global myString = {Program.myString}");
}
static void Main(string[] args)
{
    string myString = "String defined in Main()";
    Program.myString = "Global string";
    Write();
    WriteLine("\nNow in Main()");
    WriteLine($"Local myString = {myString}");
    WriteLine($"Global myString = {Program.myString}");
    ReadKey();
}
```

现在结果如图 6-5 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_148_0.png)

图 6-5

在这里，你添加了另一个名为 `myString` 的变量，这次它位于代码名称层次结构的更高层。该变量定义如下：

```
static string myString;
```

同样，`static` 关键字是必需的。这里不过多深入细节，只需理解在这种类型的控制台应用程序中，对于这种形式的全局变量，你必须使用 `static` 或 `const` 关键字。如果你想修改全局变量的值，则需要使用 `static`，因为 `const` 禁止变量的值被更改。

为了将该变量与 `Main()` 和 `Write()` 中同名的局部变量区分开来，你必须使用完全限定名来限定变量名，如第 3 章所述。这里，你将全局版本称为 `Program.myString`。只有当全局变量和局部变量同名时才有此必要；如果没有局部变量 `myString`，你可以直接使用 `myString` 来引用全局变量，而不必使用 `Program.myString`。当局部变量与全局变量同名时，称全局变量被隐藏了。

全局变量的值在 `Main()` 中通过以下代码设置：

```
Program.myString = "Global string";
```

并在 `Write()` 中通过以下代码访问：

```
WriteLine($"Global myString = {Program.myString}");
```

你可能想知道为什么不用这种技术与函数交换数据，而不是使用前面展示的参数传递。在某些情况下，这确实是一种可以接受的数据交换方式，例如，如果你编写一个用作插件或较大项目中短脚本的单一对象。然而，在许多场景下这并不是一个好主意。使用全局变量最常见的问题与并发管理有关。例如，一个全局变量可以被类中的许多方法或不同线程写入和读取。如果许多线程和方法都可以写入该全局变量，你能确定其中的值包含有效数据吗？如果没有一些额外的同步代码，答案很可能是否定的。此外，随着时间的推移，全局变量的实际意图可能会被遗忘，并在以后出于其他原因被使用。因此，是否使用全局变量的选择取决于所讨论函数的预期用途。

使用全局变量的问题在于，它们通常不适用于“通用”函数，这些函数应该能够处理你提供的任何数据，而不仅仅是特定全局变量中的数据。稍后你将更深入地了解这一点。

## 其他结构中的变量作用域

上一节中提出的其中一点在函数之间的变量作用域之外还有影响：变量的作用域包括它们被定义所在的代码块以及任何直接嵌套的代码块。你可以在本章下载的 VariableScopeInLoops\Program.cs 中找到接下来讨论的代码。这也适用于其他代码块，例如分支和循环结构中的代码块。考虑以下代码：

```
int i;
for (i = 0; i < 10; i++)
{
    string text = "Line " + Convert.ToString(i);
    WriteLine($"{text}");
}
WriteLine($"Last text output in loop: {text}");
```

这里，字符串变量 `text` 是 `for` 循环的局部变量。这段代码无法编译，因为循环外部的 `WriteLine()` 调用试图使用变量 `text`，而 `text` 在循环外部超出作用域。尝试按如下方式修改代码：

```
int i;
string text;
for (i = 0; i < 10; i++)
{
    text = "Line " + Convert.ToString(i);
    WriteLine($"{text}");
}
WriteLine($"Last text output in loop: {text}");
```

这段代码也会失败，因为变量必须先声明并初始化后才能使用，而 `text` 只在 `for` 循环中初始化。当退出循环块时，赋给 `text` 的值会丢失，因为它在块外部未被初始化。但是，你可以进行以下修改：

```
int i;
string text = "";
```

