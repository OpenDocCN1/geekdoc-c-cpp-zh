
执行执行上述代码后，将产生以下结果。

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

## 关于 C# 数组的概念

当你处理 C# 数组时，肯定会遇到一些需要了解的概念。它们在高级课程中会被证明非常有用。

## 多维数组

C# 支持多维数组。这些数组最常见且简单的形式是二维数组。

## 锯齿数组

这些数组可以简单说是数组的数组。

## Array 类

该类定义在 `System` 命名空间中。它是数组的基类。因此，它提供了许多方法和属性来帮助你处理数组。

## 将数组传递给函数

可以将数组传递给函数。可以通过指定数组名称但不指定索引来实现。

## 参数数组

它们用于向给定函数传递未知数量的参数。数组部分在此结束。现在，我们将查看字符串，但在之前，我们想向你简要介绍 C# 中的索引器（indexers）。

## 索引器

索引器允许像数组一样被索引。当你为类定义索引器时，该类的行为类似于虚拟数组。此时，该类的实例可以使用方括号 `[]` 进行访问。

## 索引器的用途

索引器的声明与属性在某种程度上相似。就像属性一样，你使用 `get` 和 `set` 访问器来定义索引器。索引器从对象实例中返回或设置特定值，而属性返回或设置特定的数据成员。换句话说，索引器将实例数据拆分为较小的部分，并对每个部分进行索引、设置或获取。（Tutorials Point

## 重载索引器

索引器可以重载。它们可以声明多个参数，且每个参数可以是不同的类型。索引器并不要求整数，它们也可以是其他类型，例如 C# 中的字符串（`string`）。

## 字符串介绍

在 C# 中，字符串可以作为字符数组使用。尽管如此，通常的做法是使用 `string` 关键字来声明一个存储变量。你必须记住，`string` 关键字仅仅是 `System.String` 类的别名。

## 字符串对象的创建

字符串对象可以通过以下任何一种过程创建。

- 通过将字符串字面量赋值给 `String` 变量
- 使用 `String` 类的构造函数
- 通过获取属性或调用可以返回字符串的方法。
- 使用字符串拼接运算符 `+`
- 通过调用格式化方法，该方法可以将对象或值转换为相应的字符串表示。

下面的示例说明了字符串对象的创建。

```csharp
using System;

namespace StringApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            // 来自字符串字面量和字符串拼接
            string fname, lname;
            fname = "John";
            lname = "Smith";
            string fullname = fname + lname;
            Console.WriteLine("Full Name: {0}", fullname);

            // 使用字符串构造函数
            char[] letters = { 'H', 'e', 'T', 'o' };
            string greetings = new string(letters);
            Console.WriteLine("Greetings: {0}", greetings);

            // 返回字符串的方法
            string[] array = { "Hello", "From", "The", "Earth" };
            string message = String.Join(" ", array);
            Console.WriteLine("Message: {0}", message);

            // 用于转换值的格式化方法
            DateTime waiting = new DateTime(2016, 10, 10, 17, 58, 1);
            string chat = String.Format("Message sent at {0:t} on {0:D}", waiting);
            Console.WriteLine("Message: {0}", chat);
        }
    }
}
```

在编译并执行上述代码后，将产生以下结果。

Full Name: Rowan Atkinson
Greetings: Hello
Message: Hello From The Earth Message sent at 5:58 PM on Wednesday, October 10, 2016

## String 类属性

`String` 类拥有两个属性。它们描述如下。

- Chars: 获取给定字符串对象中指定位置的 `Char` 对象。
- Length: 获取给定字符串对象中字符的总数。

## String 类中存在的方法

`String` 类中提供了许多可用方法。当你处理字符串对象时，这些方法会非常有帮助。以下是一些常用方法。

```csharp
public static int Compare(string strA, string strB)
```
这将比较两个字符串对象。它将返回一个整数，表示对象在排序顺序中的相对位置。

```csharp
public static int Compare(string strA, string strB, bool ignoreCase )
```
这也会比较两个字符串对象，并返回一个表示对象在排序顺序中的相对位置的整数。尽管如此，当布尔参数为 `true` 时，它将忽略大小写。

```csharp
public static string Concat(string str0, string str1)
```
这将拼接两个字符串对象。可以增加正在拼接的字符串对象的数量。

```csharp
public bool Contains(string value)
```
它将返回一个值，表示给定字符串是否存在于字符串中。

```csharp
public static string Copy(string str)
```
这将创建一个与给定字符串具有相同值的新 `String` 对象。

```csharp
public bool EndsWith(string value)
```
这将确定给定字符串对象的末尾是否与给定字符串匹配。

```csharp
public static bool Equals(string a, string b)
```
这将确定两个 `String` 对象是否具有完全相同的值。

```csharp
public int IndexOf(char value)
```
这将返回字符在字符串中的索引。将提供字符首次出现位置的从 0 开始的索引。

```csharp
public static string Format(string format, Object arg)
```
这将替换给定字符串中的一个或多个项目。它们将被替换为给定对象的字符串表示。

```csharp
public string Insert(int startIndex, string value)
```
这将返回一个新字符串，该字符串在给定字符串的特定位置插入了给字符串。

```csharp
public static bool IsNullOrEmpty(string value)
```
这指示给定字符串是否为 `null` 或空字符串。

```csharp
public static string Join(string separator, string[] value)
```
这将使用每个元素之间的分隔符拼接数组中的所有元素。

```csharp
public static string Join(string separator, string[] value, int startIndex, int count)
```
这将使用每个元素之间的分隔符拼接字符串的元素。

```csharp
public int LastIndexOf(char value)
```
这返回当前对象内部字符的索引位置。将使用从 0 开始的索引位置，且仅提到最后一次出现。
```
public string Remove(int startIndex)
```
这将删除从当前实例的指定位置开始的所有字符。它将持续到最后一个位置。最后，将返回字符串。

`String` 类还有许多其他方法和构造函数。MSDN 库包含了完整列表。现在，让我们来看几个示例，演示如何使用上述某些方法。

下面的示例说明了如何使用上述某些方法。

（此处省略重复的示例代码翻译逻辑）

```csharp
public int book_id;
};
```

下面的示例展示了如何使用该结构体。

```csharp
using System;
struct Books
{
    public string title;
    public string author;
    public string subject;
    public int book_id;
}
public class testStructure
{
    public static void Main(string[] args)
    {
        Books Book1; /* 定义类型为 Book 的 Book1 */
        Books Book2; /* 定义类型为 Book 的 Book2 */
        /* book 1 规格 */
        Book1.title = "C# Programming";
        Book1.author = "John Smith";
        Book1.subject = "C# Programming Tutorial";
    }
}
```

```csharp
Book1.book_id = 123456;
/* book 2 规格 */
Book2.title = "Java Programming";
Book2.author = "Jane Smith";
Book2.subject = "Java Programming Tutorial";
Book2.book_id = 456789;
/* 打印 Book1 信息 */
Console.WriteLine("Book 1 title : {0}", Book1.title);
Console.WriteLine("Book 1 author : {0}", Book1.author);
Console.WriteLine("Book 1 subject : {0}", Book1.subject);
Console.WriteLine("Book 1 book_id : {0}", Book1.book_id);
/* 打印 Book2 信息 */
Console.WriteLine("Book 2 title: {0}", Book2.title);
Console.WriteLine("Book 2 author: {0}", Book2.author);
Console.WriteLine("Book 2 subject : {0}", Book2.subject);
Console.WriteLine("Book 2 book_id : {0}", Book2.book_id);
Console.ReadKey();
}
```

在编译并执行上述代码后，将产生以下结果。

Book 1 title : C# Programming
Book 1 author : John Smith
Book 1 subject : C# Programming Tutorial
Book 1 book_id : 123456
Book 2 title : Java Programming
Book 2 author : Jane Smith
Book 2 subject : Java Programming Tutorial
Book 2 book_id : 456789

## C# 中结构体的特征

在上面的示例中，你使用了一个简单的结构体。如果你已经在 C 或 C++ 中使用过结构体，那么你应该知道 C# 中的结构体与你在任一语言中找到的是不同的。C# 结构体的特征如下：

- 结构体可以拥有字段、方法、属性、索引器、事件和运算符方法。
- 它们可以定义构造函数。但它们不能有析构函数。同时，无法为结构体定义默认构造函数。默认构造将被将被定义。因此，它们无法被修改。
- 与类不同，结构体不能继承其他结构体或类。
- 同样，无法将其作为其他类或结构体的基类。
- 你不能将结构成员指定为虚、抽象或保护。
- 结构体可以实现一个或多个接口。
- 使用 New 运算符创建结构体对象时，它会被创建并调用相应的构造函数。与类不同，结构体对象可以在不使用 New 运算符的情况下实例化。
- 如果你不使用 New 运算符，字段将保持未分配状态。因此，在初始化所有字段之前，该对象将是不可用的。

## 类与结构体的区别

这两者之间几点不同。列如下：

- 结构体是值类型，而类是引用类型。
- 与类不同，结构体不支持继承。
- 结构体没有默认构造函数。

现在我们对结构体有了更多了解，让我们重新创建之前的关于 Books 结构体的示例，以便更好地理解。

```csharp
using System;
struct Books
{
    private string title;
    private string author;
    private string subject;
    private int book_id;
    public void getValues(string t, string a, string s, int id)
    {
        title = t;
        author = a;
        subject = s;
        book_id = id;
    }
    public void display()
    {
      Console.WriteLine("Title : {0}", title);
      Console.WriteLine("Author : {0}", author);
      Console.WriteLine("Subject : {0}", subject);
      Console.WriteLine("Book_id :{0}", book_id);
    }
}
public class testStructure
{
  public static void Main(string[] args)
  {
    Books Book1 = new Books(); /* 定义类型为 Book 的 Book1 */
    Books Book2 = new Books(); /* 定义类型为 Book 的 Book2 */
    /* book 1 规格 */
    Book1.getValues("C# Programming", "John Smith", "C# Programming Tutorial", 123456);
    /* book 2 规格 */
    Book2.getValues("Java Programming", "Jane Smith", "Java Programming Tutorial", 456789);
    /* 打印 Book1 信息 */
    Book1.display();
    /* 打印 Book2 信息 */
    Book2.display();
    Console.ReadKey();
  }
}
```

在编译并执行上述代码后，将产生以下结果。

Book 1 title : C# Programming
Book 1 author : John Smith
Book 1 subject : C# Programming Tutorial
Book 1 book_id : 123456
Book 2 title : Java Programming
Book 2 author : Jane Smith
Book 2 subject : Java Programming Tutorial
Book 2 book_id : 456789

## 什么是枚举（Enum）？

Enum 是 enumerations 的缩写。在 C# 中，枚举是一个由底层整数类型的命名常量集合。枚举用于提高代码的可读性和可维护性。

## 声明枚举

通常，声明枚举的语法所示。

```csharp
using System;
namespace EnumApplication
{
    enum Days
    {
        Sun, Mon, Tue, Wed, Thu, Fri, Sat
    }
    class EnumProgram
    {
        static void Main(string[] args)
        {
            Days WeekdayStart = Days.Mon;
            Days WeekdayEnd = Days.Fri;
            Console.WriteLine("Monday: {0}", WeekdayStart);
            Console.WriteLine("Friday: {0}", WeekdayEnd);
            Console.ReadKey();
        }
    }
}
```

执行上述代码后，将产生以下结果。

Monday: 1
Friday: 5
