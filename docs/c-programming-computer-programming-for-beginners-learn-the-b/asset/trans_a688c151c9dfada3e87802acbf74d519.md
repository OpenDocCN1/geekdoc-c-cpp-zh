

}
}

执行上述示例后，您将得到以下结果。

Enter the first value:

7

Enter the second value:

8

After method call, value of a : 7

After method call, value of b : 8

相反，我们创建一个数组 a，并使用 a[0]、a[1] 和 a[2] 等。

请记住，数组中的特定元素可以通过索引访问。在 C# 中，所有数组都拥有连续的内存位置。最低地址对应于数组的第一个元素，而最高地址属于最后一个元素。

## 声明数组

在 C# 中，如果要声明数组，必须使用以下语法。

```
datatype[] arrayName;
```

该语法的各个组成部分讨论如下。

- datatype 用于指定数组中元素的类型。
- [] 指定数组的秩。数组的秩定义数组的大小。
- arrayName 是该数组的名称。

## 初始化数组

请记住，声明数组不会在内存中初始化它。只有初始化数组变量后，才能为其赋值。由于数组是引用类型，您必须使用 new 关键字来创建给定数组的实例。

下面的示例说明了具体做法。

```
double[] balance = new double[10];
```

## 给数组赋值

可以给数组的各个元素赋值。为此，需要使用元素的索引号。下面的示例说明了这一点。

```
double[] balance = new double[10];
```

```
balance[0] = 4500.0;
```

也可以在声明数组时为其赋值。

```
double[] balance = { 2340.0, 4523.69, 3421.0 };
```

还可以同时创建和初始化数组。

```
int [] marks = new int[5] { 99, 98, 92, 97, 95 };
```

如果需要，可以省略数组的大小。

```
int [] marks = new int[] { 99, 98, 92, 97, 95 };
```

数组变量可以被复制到另一个数组变量。在这种情况下，目标数组变量以及源数组变量都将

```csharp
{
static void Main(string[] args)
{
	int [] n = new int[10]; /* n is an array of 10 integers */
	int i,j;
	/* initialize elements of array n */
	for (i = 0; i < 10; i++)
	{
		n[i] = i + 100;
	}
	 /* output each array element's value */
	for (j = 0; j < 10; j++)
	{
		Console.WriteLine("Element[{0}] = {1}",j, n[j]);
	}
	Console.ReadKey();
}
}
```

执行上述代码后，将产生以下结果。

Element[0] = 100

Element[1] = 101

Element[2] = 102

Element[3] = 103

Element[4] = 104

Element[5] = 105

Element[6] = 106

Element[7] = 107

Element[8] = 108

Element[9] = 109

## C# 中与数组相关的概念

在 C# 中处理数组时，有几个重要概念需要了解。它们在高级课程中可能会很有用。

## 多维数组

C# 支持多维数组。这些数组最常见和最简单的形式是二维数组。

## 交错数组

简单来说，这些数组就是数组的数组。

## Array 类

该类定义在 System 命名空间中。它是所有数组的基类。因此，它提供了许多方法和属性，以便在操作数组时为您提供帮助。

## 将数组传递给函数

可以将数组传递给函数。这可以通过指定数组的名称（不带索引）来实现。

## 参数数组

它们用于向给定函数传递数量不定的参数。

关于数组的部分到此结束。接下来，我们将研究字符串。

## 字符串简介

在 C# 中，字符串可以用作字符数组。尽管如此，常见做法是使用 string 关键字来声明存储变量。您必须记住，string 关键字只是 System.String 类的别名。

## 创建字符串对象

可以通过以下任一过程创建字符串对象。

- 通过将字符串字面量赋值给 String 变量
- 使用 String 类构造函数
- 通过检索属性或调用可返回字符串的方法
- 通过使用字符串连接运算符 +
- 通过调用格式化方法，将对象或值转换为相应的字符串表示形式

下面的示例说明了字符串对象的创建。

```
using System;

namespace StringApplication
{
    class Program
    {
        static void Main(string[] args)
        {
```

```csharp
//from string literal and string concatenation
string fname, lname;
fname = "John";
lname = "Smith";
string fullname = fname + lname;
Console.WriteLine("Full Name: {0}", fullname);
```

```csharp
//by using string constructor
char[] letters = { 'H', 'e', 'l', 'l', 'o' };
string greetings = new string(letters);
Console.WriteLine("Greetings: {0}", greetings);
```

```csharp
//methods returning string
string[] sarray = { "Hello", "From", "The", "Earth" };
string message = String.Join(" ", sarray);
Console.WriteLine("Message: {0}", message);
```

```csharp
//formatting method to convert a value
DateTime waiting = new DateTime(2016, 10, 17, 58, 1);
string chat = String.Format("Message sent at {0:t} on {0:D}", waiting);
```

```csharp
Console.WriteLine("Message: {0}", chat);
}
}
}
```

编译并执行上述代码后，将产生以下结果。

```
Full Name: Rowan Atkinson
Greetings: Hello
Message: Hello From The Earth
Message: Message sent at 5:58 PM on Wednesday, October 10, 2016
```

## String 类属性

String 类拥有两个属性。如下所列。

- Chars：获取给定 String 对象中指定位置的 Char 对象。
- Length：获取给定 String 对象中的字符总数。

## String 类中的方法

String 类中有多个可用方法。在处理字符串对象时，这些方法会很有帮助。以下是一些常用的方法。

## public static int Compare(string strA, string strB)

比较两个给定的字符串对象。返回一个整数，指示这两个对象在排序顺序中的相对位置。

## public static int Compare(string strA, string strB, bool ignoreCase )

比较两个给定的字符串对象，并返回一个整数，指示这两个对象在排序顺序中的相对位置。但是，当布尔参数为 true 时，它将忽略大小写。

## public static string Concat(string stro, string str1)

连接两个字符串对象。可以增加要连接的字符串对象的数量。

## public bool Contains(string value)

返回一个值，指示给定的 String 对象是否存在于给定字符串中。

## public static string Copy(string str)

创建一个与给定字符串具有相同值的新 String 对象。

## public bool EndsWith(string value)

确定给定字符串对象的结尾是否与给定字符串匹配。

## public static bool Equals(string a, string b)

确定两个给定的 String 对象是否具有完全相同的值。

## public int IndexOf(char value)

返回给定 Unicode 字符在字符串中的索引。将提供该字符首次出现的从零开始的索引。

## public static string Format(string format, Object argo)

替换给定字符串中的一个或多个格式项。它们将被替换为给定对象的字符串表示形式。

## public string Insert(int startIndex, string value)

返回一个新字符串，该字符串在给定字符串对象中的特定索引位置插入了给定字符串。

