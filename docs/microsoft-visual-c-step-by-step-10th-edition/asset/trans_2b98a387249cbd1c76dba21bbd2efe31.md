

# 访问一系列数组元素

C# 允许你使用形式为 $x..y$ 的索引从数组中检索连续的元素。返回的是从元素 $x$ 开始到 $y$ 结束的序列——这一点很重要——它**不包含** $y$。结果是包含所检索元素的另一个数组。在下面的示例中，从 names 数组中获取元素 0 和 1 所在的数组子集：

点击此处查看代码图像

```
var names = new[] { { Name = "John", Age = 57 },
new { Name = "Diana", Age = 57 },
new { Name = "James", Age = 30 },
new { Name = "Francesca", Age = 26 } };

var subset = names[0..2];
```

该子集包含 John 和 Diana 的值（元素 0 和 1）。范围的第一个数字必须小于或等于第二个数字；否则你将得到 System.ArgumentOutOfRangeException。如果范围的第一个数字和第二个数字相同，结果是一个长度为 0 的数组。

你还可以指定形式为 $^y$ 的表达式作为起始元素。在这种情况下，将从元素 $x$ 向后计算 $y-1$ 个元素（尽管元素仍然按正向顺序检索的）。在下面的语句中，数组包含 Diana、James 和 Francesca 的值（从元素 3 向后开始，或者说 $4-1$ 个元素）：

```
var subset = names[..4];
```

# 遍历数组

所有数组实际上都是 .NET 库中 System.Array 类的实例，该类定义了一些有属性和方法。例如，你可以查询 Length 属性来发现数组包含多少元素，并使用 for 语句遍历数组的所有元素。下面的示例代码将引脚的数组值写入控制台：

点击此处查看代码图像

```
int[] pins = { 9, 3, 7, 2 };
for (int index = 0; index < pins.Length; index++)
{
  int pin = pins[index];
  Console.WriteLine(pin);
}
```

> 注意 Length 是一个属性而不是方法，这就是为什么当你在调用它时不需要使用括号的缘。你将在第 15 章“实现属性以访问字段”中学习属性。

新程序员经常忘记数组从元素 0 开始，并且最后一个元素的编号为 Length–1。幸运的是，C# 提供了 foreach 语句，通过它你可以遍历数组的元素，而不必担心这些问题。例如，这里是将之前的 for 语句重写为等效的 foreach 语句：

点击查看代码图像

```
int[] pins = { 9, 3, 7, 2 };

foreach (int pin in pins)
{
  Console.WriteLine(pin);
}
```

foreach 语句声明了一个迭代变量（在本例中为 int pin），它会自动获取数组中每个元素的值。该变量的类型必须与数组中元素的类型匹配。foreach 语句是遍历数组的首选方法；它直接表达了代码的意图，并且去除了所有的 for 循环脚架。然而，在某些情况下，你会发现必须回退到 for 语句：

- foreach 语句遍历整个数组。如果你只想遍历数组的已知部分（例如前半部分）或跳过某些元素（例如每第三个元素），使用 for 语句更简单。

- foreach 语句始终从索引 0 遍历到索引 Length–1。如果你想反向遍历或按其他序列遍历，使用 for 语句更简单。

- 如果循环体需要元素的索引而不仅仅是元素的值，你必须使用 for 语句。

- 如果你需要修改数组的元素，你必须使用 for 语句。这是因为 foreach 语句的迭代变量是数组每个元素的只读副本。

> 提示 使用 foreach 语句尝试遍历长度为 0 的数组是完全安全的。

你可以将变量声明为 var，让 C# 编译器根据数组中元素的类型来确定变量的类型。如果你实际上不知道输入数组的类型，例如当数组包含匿名对象时，这特别有用。下面的示例演示了你如何遍历之前显示的家庭成员数组：

点击此处查看代码图像

```
var names = new[] { new { Name = "John", Age = 57 },
new { Name = "Diana", Age = 57 },
new { Name = "James", Age = 30 },
new { Name = "Francesca", Age = 26 } };

foreach (var familyMember in names)
{
    Console.WriteLine("Name: {familyMember.Name}, Age: {familyMember.Age}");
}
```

# 将数组作为方法的参数或返回值传递

你可以定义接受数组作为参数的方法或将其作为返回值传递的方法。

将数组作为参数传递的语法与声明数组非常相似。例如，接下来的代码示例定义了一个名为 ProcessData 的方法，它接受整数数组作为参数。方法体遍历数组并对每个元素执行某些特定的处理：

点击此处查看代码图像

```csharp
public void ProcessData(int[] data)
{
    foreach (int i in data)
    {
        ...
    }
}
```

数组是引用对象，因此如果你在像 ProcessData 这样的方法内部修改了作为参数传递的数组的内容，则修改对于该数组的所有引用都是可见的，包括作为参数传递的原始参数。

要从方法返回数组，你只需指定数组的类型作为返回类型。在方法中，你创建并填充数组。下面的示例提示用户输入数组的大小，然后是每个元素的数据。方法创建的数组作为返回值返回：

点击此处查看代码图像

```csharp
public int[] ReadData()
{
    Console.WriteLine("How many elements?");
    string reply = Console.ReadLine();
    int numElements = int.Parse(reply);

    int[] data = new int[numElements];
    for (int i = 0; i < numElements; i++)
    {
        Console.WriteLine($"Enter data for element {i}");
        data[i] = int.Parse(Console.ReadLine());
    }
    return data;
}
```

# 数组参数和 Main 方法

你可能注意到 Main 方法接受一个字符串数组作为参数。你可以从命令行调用 Main 方法，如下：

点击此处查看代码图像

```csharp
static void Main(string[] args)
{
```操作系统将这些参数传递给语言运行时；由 Main 程序来验证这些参数是否有效。下面的示例取自一个处理文件的工具：

点击此处查看代码图像

```csharp
static void Main(string[] args)
{
    foreach (string filename in args)
    {
        ProcessFile(filename);
    }
}
```

用户可以在命令行运行 MyFileUtils，如下：

MyFileUtils C:\Temp\TestData.dat C:\Users\John\Documents\MyDoc.txt

# 复制数组

数组是引用类型。（记住数组是 System.Array 类的实例。）这意味着当你复制数组变量时，你实际上得到了指向同一个数组实例的两个引用，如下例所示：

```csharp
int[] pins = { 9, 3, 7, 2 };
int[] alias = pins; // aliases 和 pins 指向同一个数组实例
```

在这个示例中，如果你修改了 pins[1]，则通过读取 alias[1] 也能看到该更改。

如果你想复制数组变量所引用的数组实例（堆上的数据），你必须做两件事：

1. 创建一个与要复制数组类型相同且长度相同的数组实例。
2. 将数据逐个元素从原始数组复制到新数组，在此示例中：

```csharp
int[] pins = { 9, 3, 7, 2 };
int[] copy = new int[pins.Length];
for (int i = 0; i < pins.Length; i++) {
    copy[i] = pins[i];
}
```

注意此代码使用原始数组的 Length 属性来指定新数组的大小。

