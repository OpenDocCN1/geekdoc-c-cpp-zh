
```csharp
namespace StaticApplication
{
    class StaticVar
    {
        public static int num;
        public static void count()
        {
            num++;
        }
        public static int getNum()
        {
            return num;
        }
    }
    class StaticTester
    {
        static void Main(string[] args)
        {
            StaticVar s1 = new StaticVar();
            StaticVar s2 = new StaticVar();
            s1.count();
            s1.count();
            s1.count();
            s2.count();
            s2.count();
            s2.count();
            Console.WriteLine("Value for s1: {0}", StaticVar.getNum());
            Console.WriteLine("Value for s2: {0}", StaticVar.getNum());
            Console.ReadKey();
        }
    }
}
```

执行上述代码后，你会发现以下结果。

Value for s1: 3
Value for s2: 6

由方法返回，则返回类型将为 `void`。

方法名（Method name）：这是方法名的唯一标识符。名称对大小写敏感。此外，标识符不能与类中已定义的任何其他标识符相同。

参数列表（Parameter list）：参数是用于在方法之间传递和接收数据的。它们被包含括号内。参数列表将引用方法参数的顺序、数量和类型。重要的是，方法可能没有任何任何参数。

方法体（Method Body）：方法体将包含完成该活动必需的指令集。

请看下面给出的示例。在这一段代码中，你会注意到一个名为 `FindMax` 的函数。它接收两个整数值并对它们进行比较。返回其中较大的值。该函数有一个公有修饰符（public）。因此，可以使用它的实例从类的外部访问它。

```csharp
class NumberManipulator
{
    public int FindMax(int num1, int num2)
    {
        /* local variable declaration */
        int result;
        if (num1 > num2)
            result = num1;
        else
            result = num2;
        return result;
    }
}
...
}
```

---

## 调用方法 (Calling a Method)

在 C# 中，调用方法非常简单，只需使用其名称即可。看下面给出的示例。它展示了如何调用方法。

```csharp
using System;
namespace CalculatorApplication
{
class NumberManipulator
{
    public int FindMax(int num1, int num2)
    {
        /* local variable declaration */
        int result;
        if (num1 > num2)
            result = num1;
        else
            result = num2;
        return result;
    }
    static void Main(string[] args)
{
  /* local variable definition */
  int a = 100;
  int b = 200;
  int ret;
  NumberManipulator n = new NumberManipulator();
  //calling the FindMax method
  ret = n.FindMax(a, b);
  Console.WriteLine("Max value is : {0}", ret);
  Console.ReadLine();
}
}
}
```

执行上述代码后，将产生以下结果。

Max value is : 200

可以通过使用方法的类的实例从其他类调用公有方法。下面给出的示例向你展示了如何操作。在这种情况下，`FindMax` 方法是 `NumberManipulator` 类的一部分。它可以从另一个名为 `Test` 的类调用。

```csharp
using System;
namespace CalculatorApplication
{
class NumberManipulator
{
    public int FindMax(int num1, int num2)
    {
        /* local variable declaration */
        int result;
        if(num1 > num2)
            result = num1;
        else
            result = num2;
        return result;
    }
}
class Test
{
    static void Main(string[] args)
    {
        /* local variable definition */
        int a = 100;
        int b = 200;
        int ret;
        NumberManipulator n = new NumberManipulator();
        //calling the FindMax method
        ret = n.FindMax(a, b);
        Console.WriteLine("Max value is : {0}", ret);
        Console.ReadLine();
    }
}
}
```

下面给出的结果由上述示例产生。

Max value is : 200

---

## 理解递归方法调用 (Understanding Recursive Method Call)

方法可以调用自己。这种过程被称为递归。下面的示例说明了递归方法调用的用法。在这里，通过递归方法调用计算给定数字的阶乘。

```csharp
using System;
namespace CalculatorApplication
{
    class NumberManipulator
    {
        public int factorial(int num)
        {
            /* local variable declaration */
            int result;
            if (num <= 1)
                result = 1;
            else
                result = num * factorial(num - 1);
            return result;
        }
        static void Main(string[] args)
        {
            /* local variable definition */
            int a = 5;
            int ret;
            NumberManipulator n = new NumberManipulator();
            //calling the factorial method
            ret = n.factorial(a);
            Console.WriteLine("Factorial of {0} is {1}", a, ret);
            Console.ReadLine();
        }
    }
}
```

执行上述代码后，将产生以下结果。

Factorial of 5 is 120

```csharp
using System;
namespace CalculatorApplication
{
    class NumberManipulator
    {
        public void getValue(out int x)
        {
            int temp = 5;
            x = temp;
        }
        static void Main(string[] args)
        {
            NumberManipulator n = new NumberManipulator();
            /* local variable definition */
            int a = 100;
            Console.WriteLine("Before method call, value of a : {0}", a);
            /* calling a function to get the value */
            n.getValue(out a);
            Console.WriteLine("After method call, value of a : {0}", a);
            Console.ReadLine();
        }
    }
}
```

执行完上方示例所示的代码后，将产生以下结果。

Before method call, value of a : 100

After method call, value of a : 5

对于输出参数（output parameter），提供的变量不需要赋值初始值。因此，当你需要通过参数从方法返回值，而又不需要为参数分配初始值时，输出参数非常有用的。

下面的示例演示了这一点。

```csharp
using System;
namespace CalculatorApplication
{
    class NumberManipulator
    {
        public void getValues(out int x, out int y)
        {
            Console.WriteLine("Enter the first value: ");
            x = Convert.ToInt32(Console.ReadLine());
            Console.WriteLine("Enter the second value: ");
            y = Convert.ToInt32(Console.ReadLine());
        }
    }
}
```

```csharp
static void Main(string[] args)
{
    NumberManipulator n = new NumberManipulator();
    /* local variable definition */
    int a, b;
    /* calling a function to get the values */
    n.getValues(out a, out b);
    Console.WriteLine("After method call, value of a : {0}", a);
    Console.WriteLine("After method call, value of b : {0}", b);
    Console.ReadLine();
}
}
```

执行上述示例后，你将得到以下结果。

Enter the first value:
7

Enter the second value:
8

After method call, value of a : 7
After method call, value of b : 8

## 第 11 章：处理数组与字符串

由于你正在使用 C#，你肯定会遇到数组和字符串。事实上，你在学习 `for each` 循环时已经使用过数组。至于字符串，它们已经在书中的各种示例中出现过。现在是时候进一步了解一下这两种类型了。

### 了解数组

数组将存储一组不同元素的集合。该集合具有固定的大小，且所有元素都是相同类型。它们被用于存储一组数据。然而，定义它们的一种更好方式是说：它们是存储在连续内存位置的变量集合。

数组避免了声明多个独立变量的麻烦。相反，我们只需要声明一个数组变量，并将所需的值放入其中。因此，我们不需要创建如 `a0, a1, a2` 等这样的变量列表。相反，我们创建一个数组并使用 `a[0]`、`a[1]` 和 `a[2]` 等。

记住，数组中的特定元素可以通过索引（index）访问。在 C# 中，所有数组都具有连续的内存位置。最低地址对应数组的第一个元素，而最高地址属于最后一个元素。

### 声明数组

在 C# 中，如果你想声明一个数组，必须使用以下语法。

```csharp
datatype[] arrayName;
```

该语法的每个元素说明如下：

- `datatype` 用于指定数组中将存在的元素的数据类型。
- `[]` 指定数组的秩（rank）。数组的秩定义了数组的大小。
- `arrayName` 是该数组的名称。

### 初始化数组

记住，声明数组后并不会在内存中初始化它。只有在数组变量初始化后，你才能对其赋值。由于数组是引用类型，你必须使用 `new` 关键字来创建给定数组的实例。

下面的示例展示了如何操作。

```csharp
double[] balance = new double[10];
```

### 给数组赋值

可以给数组的单个元素赋值。为了这样做，需要使用元素的索引号。下面的示例说明了这一点。

```csharp
double[] balance = new double[10];
```

```csharp
balance[0] = 4500.0;
```

在声明数组时也可以给其赋值。

```csharp
double[] balance = { 2340.0, 4523.69, 3421.0 }; 
```

还可以在同时创建并初始化数组。

```csharp
int [] marks = new int[5] { 99, 98, 92, 97, 95};
```

如果你愿意，可以忽略数组的大小。

```csharp
int [] marks = new int[] { 99, 98, 92, 97, 95};
```

数组变量可以复制到另一个数组变量中。在这种情况下，目标数组变量将指向相同的内存位置。如下例所示。

```csharp
int [] marks = new int[] { 99, 98, 92, 97, 95};
```

当创建数组时，编译器将隐式地将所有元素初始化为默认值。

```csharp
int[] marks = int[] { 99, 98, 92, 97, 95};
```

### 访问数组元素

可以通过索引访问数组中的特定元素。这如下例所示。

```csharp
using System;
namespace ArrayApplication
{
    class MyArray
{
        static void Main(string[] args)
{
    int [] n = new int[10];
    int i,j;
    /* 初始化数组 n */
    for (i = 0; i < 10; i++)
    {
        n[i] = i + 100;
    }
    /* 输出 n 的每个元素 */
    for (j = 0; j < 10; j++
    {
        Console.WriteLine("Element[{0}] = {1}", j, n[j]);
    }
}
}
}
```
