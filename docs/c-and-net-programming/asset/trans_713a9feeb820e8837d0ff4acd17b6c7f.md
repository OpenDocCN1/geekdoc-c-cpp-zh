
{
  get { return _empID; }
}

### 2.5.3 受保护
可访问性的范围仅限于类内部以及从此类（称为基类）派生的类。

### 2.5.4 内部
internal 访问修饰符可以在包含其声明的程序内访问，也可以在同一程序集级别内访问，但不能从另一个程序集访问。

### 2.5.5 受保护内部
protected internal 具有 protected 和 internal 两者的相同访问级别。它可以在同一程序集中的任何位置访问，也可以在同一类中以及从同一类继承的类中访问。

## 1.5 创建类方法
类方法定义了类的行为，即方法封装了可以在类属性上执行的操作。

```
public void LoginCheck(string _loginName, string _password)
{
    if ( _loginName == "Ravi" && _password == "technical")
    {
        _employeeID = 10;
        _Department = "IT";
        _Name = "RaviW";
    }
    else if ( _loginName == "Avi" && _password == "publish")
    {
        _employeeID = 20;
        _Department = "ERP";
        _Name = "AviW";
    }
    else
    {
        Console.WriteLine("Invalid Login");
    }
}
```

## 1.6 创建类的实例
使用 new 运算符创建实例，即类的对象。new 运算符为对象的存储分配内存。

```
Book b;
```

上述语句仅创建了 Book 类型的引用，但未分配内存。

```
Book b = new Book();
```

上述语句实际上为 Book 类型的引用 b 分配了内存。

## 2. 构造函数

### 概念
- 1. 在面向对象编程中，构造函数是专门用于在类的对象实例被实例化时执行所需处理的特殊方法。
- 2. 类的构造函数方法与类同名，并在对象创建时自动调用。

### 解释
3. 构造函数的属性
- 3.1 一个类可以有任意数量的构造函数（即构造函数可以重载）。
- 3.2 构造函数没有任何返回类型，甚至不是 void。
- 3.3 静态构造函数不能是参数化构造函数。
- 3.4 在一个类中只能创建一个静态构造函数。
- 3.5 构造函数的主要用途是在为类创建实例时初始化类的私有字段。
- 3.6 当类中未定义构造函数时，编译器会自动在类中创建默认构造函数。
- 默认构造函数将类中的所有数值字段初始化为零，所有字符串和对象字段初始化为 null。

4. 共有 5 种类型的构造函数，分别是，
- 1. 默认构造函数
- 2. 参数化构造函数
- 3. 拷贝构造函数
- 4. 静态构造函数
- 5. 私有构造函数

## 4.1 默认构造函数
无参数的构造函数称为默认构造函数，即默认构造函数不接受任何参数。

默认构造函数的局限性在于类的每个实例都将被初始化为相同的值。

### 示例
```csharp
using System;
namespace Constructors
{
class DefaultConstructor
{
int n1,n2;
public DefaultConstructor() //default constructor
{
n1 = 300;
n2 = 450;
}

public static void Main()
{
DefaultConstructor obj = new DefaultConstructor (); //an object is created , default
constructor is called
Console.WriteLine("Addition is : " + (obj.n1 + obj.n2));
}
}
}
```

### 输入

### 输出
Addition is : 750

## 4.2 参数化构造函数
至少有一个参数的构造函数称为参数化构造函数。参数化构造函数的优点是每个类的实例可以根据需要初始化为不同的值。

```csharp
using System;
namespace Constructors
{
class ParamConstructor
{
public int n1,n2;
public ParamConstructor (int no1, int no2) //Parameterized Constructor with no1,no2 parameters
{
    n1 = no1;
    n2 = no2;
}
}
class MainClass
{
    static void Main()
    {
        ParamConstructor obj = new ParamConstructor (300, 450);  // Creating object through //Parameterized Constructor
        Console.WriteLine("Addition is : " + (obj.n1 + obj.n2));
    }
}
```

输入 无

### 输出
750

## 4.3 拷贝构造函数
通过从另一个已创建的对象复制变量来创建对象的构造函数称为拷贝构造函数。拷贝构造函数的目的是将新实例初始化为现有实例的值。

### 示例
```
using System;
namespace Constructors
{
    class Book
    {
        private string title;
        private string author;
        public Book(Book bk) //defining copy constructor
        {
            title=bk.name;
            author=bk.age;
        }
        public Book(string title, string author) // parameterized constructor.
        {
            this.title = title;
            this.author = author;
        }
public string GetDetails  // Get details of Book
{
    get
    {
        return "The book " + title + " is authored by "+ author;
    }
}
}

class BookDetails
{
    static void Main()
    {
        Book bk1 = new Book("C#", "RaviW");  // Create a new Book object.
        Book bk2 = new Book(bk1);            // here is bk1 details are copied to bk2.
        Console.WriteLine(bk2.GetDetails);
    }
}
```

## 4.4 静态构造函数
构造函数可以创建为静态构造函数。

静态构造函数对类的所有实例仅调用一次，并且在类的第一个实例创建时或对类中静态成员的首次引用时调用。

静态构造函数用于初始化类的静态字段，并编写在类生命周期中仅需执行一次的代码。

### 静态构造函数的属性
- 1. 静态构造函数没有任何访问修饰符，也没有任何参数。
- 2. 静态构造函数会在类的第一个实例创建之前或任何静态成员被引用之前自动调用以初始化类。
- 3. 静态构造函数不能直接调用，程序员无法控制静态构造函数在程序中执行的时机。
- 4. 静态构造函数的典型用途是当类使用记录文件时，构造函数用于向该记录文件写入条目。即当需要共享相同的数据项时使用静态构造函数。

### 示例
```
using System;
namespace Constructors
{
public class StaticBook
{
static StaticBook() // Static constructor defined
Console.WriteLine("The static constructor ");
}
public static void GetDetails()
{
Console.WriteLine("Book Details");
}
}
class BookDetails
{
static void Main()
{
Console.WriteLine();
StaticBook.GetDetails();
}
}
```

## 4.5 私有构造函数
当构造函数使用 private 指定符创建时，其他类无法从此类派生，也无法创建此类实例。包含私有构造函数的此类通常用于仅包含静态成员的类。

### 私有构造函数的属性
- 1. 当类仅包含静态成员时使用私有构造函数。
- 2. 它提供了单例类模式的实现
- 3. 一旦类中存在私有或公共或任何构造函数，编译器将不会向类添加无参数的公共构造函数。

//illustration of private constructor
using System;
namespace Constructors
{
public class CountValue
{
private CountValue() //private constructor declaration
}
public static int currentvalue;
public static int CountTillNow()
{
    return ++ currentvalue;
}
}
class Countdetails
{
    static void Main()
    {
        CountValue.currentvalue = 500;
        CountValue.CountTillNow();
        Console.WriteLine("Now the count is: {0}", CountValue.currentvalue);
    }
}
```

## 5. 构造函数可以调用另一个构造函数
构造函数可以调用另一个构造函数，这在多种情况下会很有用。

### 示例
```
public Book()
{
    Console.WriteLine("Constructor with no parameters called!");
}

public Book(string cover) : this()
{
    this.cover = cover;
    Console.WriteLine("Constructor with color parameter called!");
}
```

## 3. 析构函数

### 概念
- 1. 析构函数是类成员方法，在类变得不可达后运行。

### 解释
- 2. 它的名称前有特殊的 "~" 字符。
- 3. 其执行的确切时间未指定。但只要类在内存中不再被任何引用可达，它就会始终运行。
- 4. '析构函数' 用于销毁类的实例。
- 5. 一个类只能有一个析构函数。
- 6. 析构函数不能被继承或重载。
- 7. 析构函数不能被调用。它们是自动调用的。
