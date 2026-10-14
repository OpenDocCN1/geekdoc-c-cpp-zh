

*struct*，或此数组中任何不是 *int* 的内容。如果你在声明数组时指定了一组初始值设定项，可以让 C# 编译器为你推断出数组元素的实际类型，如下所示：

Click here to view code image

```
var names = new[] {"John", "Diana", "James", "Francesca"};
```

在此示例中，C# 编译器确定 *names* 变量是一个字符串数组。值得指出的是，此声明中有几个语法上的特殊之处。首先，你省略了类型中的方括号；此示例中的 *names* 变量仅声明为 *var*，而不是 *var[]*。其次，你必须在初始值设定项列表之前指定 *new* 运算符和方括号。

如果你使用此语法，必须确保所有初始值设定项具有相同的类型。下一个示例会导致编译时错误“未找到隐式类型化数组的最佳类型”：

Click here to view code image

```
var bad = new[] {"John", "Diana", 99, 100};
```

然而，在某些情况下，如果这样做有意义，编译器会将元素转换为不同类型。在以下代码中，*numbers* 数组是 *double* 数组，因为常量 3.5 和 99.999 都是 *double*，并且 C# 编译器可以将整数值 1 和 2 转换为 *double* 值：

Click here to view code image

```
var numbers = new[] {1, 2, 3.5, 99.999};
```

通常，最好避免混合类型，希望编译器为你转换它们。

隐式类型化数组在你使用匿名类型时最有用，如第 7 章“创建和管理类和对象”所述。以下代码创建了一个匿名对象的数组，每个对象包含两个字段，指定我家庭成员的姓名和年龄：

Click here to view code image

```
var names = new[] { new { Name = "John", Age = 50 }, new { Name = "Diana", Age = 50 }, new { Name = "James", Age = 23 }, new { Name = "Francesca", Age = 21 } };
```

匿名类型中的字段必须对数组的每个元素都相同。

## 访问单个数组元素

要访问单个数组元素，你必须提供一个索引来指示需要哪个元素。数组索引从零开始；因此，数组的初始元素位于索引 0 而不是索引 1。索引值为 1 访问第二个元素。例如，你可以使用以下代码将 pins 数组的第 2 个元素（第三个元素）的内容读入 int 变量：

```
int myPin;
myPin = pins[2];
```

同样，你可以通过为索引元素赋值来更改数组的内容：

```
myPin = 1645;
pins[2] = myPin;
```

所有数组元素访问都进行边界检查。如果你指定一个小于 0 或大于或等于数组长度的索引，编译器会抛出 IndexOutOfRangeException 异常，如此示例所示：

Click here to view code image

```
try
{
    int[] pins = { 9, 3, 7, 2 };
    Console.WriteLine(pins[4]); // error, the 4th and last element is at index 3
}
catch (IndexOutOfRangeException ex)
{
    ...
}
```

## 遍历数组

所有数组实际上都是 Microsoft .NET Framework 中 System.Array 类的实例，而该类定义了许多有用的属性和方法。例如，你可以查询 Length 属性来发现数组包含多少个元素，并使用 for 语句遍历数组中的所有元素。以下示例代码将 pins 数组的数组元素值写入控制台：

Click here to view code image

```
int[] pins = { 9, 3, 7, 2 };
for (int index = 0; index < pins.Length; index++)
{
    int pin = pins[index];
    Console.WriteLine(pin);
}
```

### Note

*Length* 是一个属性而不是方法，这就是为什么你在调用它时不使用括号。你可以在第 15 章“实现属性以访问字段”中了解有关属性的信息。

新程序员经常会忘记数组从元素 0 开始，最后一个元素编号为 *Length – 1*。C# 提供了 *foreach* 语句，你可以使用它遍历数组元素，而无需担心这些问题。例如，这里是前面 *for* 语句重写为等效 *foreach* 语句：

```
int[] pins = { 9, 3, 7, 2 };
foreach (int pin in pins)
{
    Console.WriteLine(pin);
}
```

*foreach* 语句声明一个迭代变量（在此示例中为 *int pin*），该变量会自动获取数组中每个元素的值。此变量的类型必须与数组中元素的类型匹配。*foreach* 语句是遍历数组的首选方式；它直接表达了代码的意图，并且所有 *for* 循环的脚手架都消失了。然而，在少数情况下，你会发现必须恢复使用 *for* 语句：

- *foreach* 语句始终遍历整个数组。如果你只想遍历数组的已知部分（例如，前半部分）或跳过某些元素（例如，每第三个元素），使用 *for* 语句会更容易。
- *foreach* 语句始终从索引 0 遍历到索引 *Length – 1*。如果你想向后迭代或按其他顺序迭代，使用 *for* 语句会更容易。
- 如果循环体需要知道元素的索引而不是仅元素的值，你必须使用 *for* 语句。
- 如果你需要修改数组的元素，你必须使用 *for* 语句。这是因为 *foreach* 语句的迭代变量是数组中每个元素的只读副本。

### Tip

使用 *foreach* 语句遍历零长度数组是完全安全的。

你可以将迭代变量声明为 var 并让 C# 编译器根据数组中元素的类型推断出变量的类型。这在你实际上不知道数组中元素的类型时尤其有用，例如当数组包含匿名对象时。以下示例演示了如何遍历前面显示的家庭成员数组：

Click here to view code image

```
var names = new[] { new { Name = "John", Age = 50 },
                new { Name = "Diana", Age = 50 },
                new { Name = "James", Age = 23 },
                new { Name = "Francesca", Age = 21 } };
foreach (var familyMember in names)
{
    Console.WriteLine($"Name: {familyMember.Name}, Age: {familyMember.Age}");
}
```

## 将数组作为参数传递和作为方法返回值

你可以定义接受数组作为参数或作为返回值返回数组的方法。

将数组作为参数传递的语法与声明数组的语法基本相同。例如，以下代码示例定义了一个名为 ProcessData 的方法，该方法接受整数数组作为参数。方法体遍历数组并对每个元素执行一些未指定的处理：

Click here to view code image

```
public void ProcessData(int[] data)
{
    foreach (int i in data)
    {
        ...
    }
}
```

重要的是要记住数组是引用对象，因此如果你在 ProcessData 等方法内部修改作为参数传递的数组的内容，则该修改将通过对数组的所有引用可见，包括作为参数传递的原始参数。

要从方法返回数组，你将数组的类型指定为返回类型。在方法中，你创建并填充数组。以下示例提示用户输入数组的大小，然后输入每个元素的数据。方法创建的数组作为返回值传递回来：

Click here to view code image

```
public int[] ReadData()
{
    Console.WriteLine("How many elements?");
    string reply = Console.ReadLine();
    int numElements = int.Parse(reply);

    int[] data = new int[numElements];
    for (int i = 0; i < numElements; i++)
    {
        Console.WriteLine($"Enter data for element {i}");
        reply = Console.ReadLine();
        int elementData = int.Parse(reply);
        data[i] = elementData;
    }
    return data;
}
```

你可以像这样调用 *ReadData* 方法：

```
int[] data = ReadData();
```

