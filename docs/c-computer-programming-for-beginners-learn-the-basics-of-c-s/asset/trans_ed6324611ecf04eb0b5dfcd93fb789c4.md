
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

# C# 中结构体的特征

在上面的示例中，你使用了一个简单的结构体。如果你已经在 C 或 C++ 中使用过结构体，那么你应该知道 C# 中的结构体与你在任一语言中找到的是不同的。C# 结构体的特征如下：

- 结构体可以拥有字段、方法、属性、索引器、事件和运算符方法。
- 它们可以定义构造函数。但它们不能有析构函数。同时，无法为结构体定义默认构造函数。默认构造将被将被定义。因此，它们无法被修改。
- 与类不同，结构体不能继承其他结构体或类。
- 同样，无法将其作为其他类或结构体的基类。
- 你不能将结构成员指定为虚、抽象或保护。
- 结构体可以实现一个或多个接口。
- 使用 New 运算符创建结构体对象时，它会被创建并调用相应的构造函数。与类不同，结构体对象可以在不使用 New 运算符的情况下实例化。
- 如果你不使用 New 运算符，字段将保持未分配状态。因此，在初始化所有字段之前，该对象将是不可用的。

# 类与结构体的区别

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

```}
}

在编译并执行上述代码后，将产生以下结果。

Book 1 title : C# Programming

Book 1 author : John Smith

Book 1 subject : C# Programming Tutorial

Book 1 book_id : 123456

Book 2 title : Java Programming

Book 2 author : Jane Smith

Book 2 subject : Java Programming Tutorial

Book 2 book_id : 456789
```

# 什么是枚举（Enum）？

Enum 是 enumerations 的缩写。在 C# 中，枚举是一个由底层整数类型的命名常量集合。枚举用于提高代码的可读性和可维护性。

# 声明枚举

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
