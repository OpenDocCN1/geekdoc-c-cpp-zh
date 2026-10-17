
```csharp
public void DerivedClassMethod()
{
    Console.WriteLine("I am a Derived Class Method()");
}
}
public class Program
{
    public static void Main(string[] args)
    {
        // 创建基类对象
        Console.WriteLine("I am accessing Base Class Object:");
        BaseClass bc = new BaseClass();
        bc.DataMember = 1;
        bc.BaseClassMethod();
        // 创建派生类对象
        Console.WriteLine("I am accessing Derived Class Object:");
        DerivedClass dc = new DerivedClass();
        dc.DataMember = 2;
        bc.BaseClassMethod();
        dc.DerivedClassMethod();
        Console.Write("\nPRESS ENTER to quit.");
        Console.ReadLine();
    }
}
```

在列表 5.1 中，我们创建了三个类：`BaseClass`、`DerivedClass` 和 `Program`。`DerivedClass` 类继承了 `BaseClass` 类。这意味着 `DerivedClass` 继承了 `BaseClass` 类的所有成员。在 `Program` 类中，我们初始化了这些类并调用了它们的方法。

图 5.2 显示了列表 5.1 的输出：

![](img/17af790174c480761404624aeed9b30b_245_0.png)

图 5.2：MyInheritance 应用程序的输出

### 创建密封类

你可以使用 `sealed` 关键字来创建一个密封类。密封类不能用基类。换句话说，密封类不能被继承。现在，让我们创建一个名为 `MySealedClass` 的应用程序，展示如何将类声明为密封类。列表 5.2 显示了 `MySealedClass` 应用程序的代码：

列表 5.2：MySealedClass 应用程序的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MySealedClass
{
    sealed class MyClass
    {
        string Fname;
        string Lname;
        int Age;
        public void GetDetail()
        {
            Console.Write("Enter Your First Name:");
            Fname = Console.ReadLine();
            Console.Write("Enter Your Last Name:");
            Lname = Console.ReadLine();
            Console.Write("Enter Your Age:");
            Age = int.Parse(Console.ReadLine());
        }
        public void ShowDetail()
        {
            Console.WriteLine(Fname + " " + Lname + " you are " + Age + " years old");
        }
    }
    /* // 以下行将显示编译错误，因为密封类不能被继承
    // class Derived : MyClass
    */
    class MainClass
    {
        static void Main(string[] args)
        {
            MyClass obj = new MyClass();
            obj.GetDetail();
            obj.ShowDetail();
            Console.Write("\nPRESS ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

在列表 5.2 中，我们使用 `sealed` 关键字创建了一个名为 `MyClass` 的密封类。该类包含两个方法 `GetDetail()` 和 `ShowDetail()`，分别用于获取用户输入并显示详情。在 `MainClass` 中，我们创建了 `MyClass` 的对象。最后，我们调用了 `GetDetail()` 和 `ShowDetail()` 方法。

图 5.3 显示了列表 5.2 的输出：

![](img/17af790174c480761404624aeed9b30b_246_0.png)

### 使用扩展方法

正如在该节中学，扩展方法可以在不创建新类的情况下扩展类。让我们创建一个名为 `MyExtension` 的应用程序来学习使用扩展方法。

列表 5.3：MyExtension 应用程序的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyExtension
{
    public static int StaticMethod(this string Number)
    {
        return int.Parse(Number);
    }
    public static string GetDetail(this string Number)
    {
        return Number.Length();
    }
    class MainClass
    {
        static void Main(string[] args)
        {
            string number = "100";
            int ext = StaticMethod(number); // 行 A
            Console.WriteLine("The Output from StaticMethod()");
            int stat = GetDetail(number); // 行 B
            Console.WriteLine("The Output from GetDetail()");
            Console.Write("\nPRESS ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

图 5.5 显示了列表 5.4 的输出：

![](img/17af790174c480761404624aeed9b30b_248_0.png)

图 5.5：Employee应用程序的输出

让我们学习使用属性来实现封装。

## 使用属性实现封装

在 C# 中，你也可以通过使用自定义属性来实现封装。这些属性包含一对 `get` 和 `set` 方法。让我们创建一个名为 Student 的应用程序，展示如何实现封装属性。列表 5.5 显示了 Student 应用程序的代码：

列表 5.5：Student应用程序的代码

![](img/17af790174c480761404624aeed9b30b_248_1.png)

在列表 5.5 中，我们声明了一个名为 StudentName 的命名属性。该属性包含 `set` 和 `get` 方法，分别用于赋值和显示 `Name` 变量的值。

图 5.6 显示了列表 5.5 的输出：

![](img/17af790174c480761404624aeed9b30b_248_2.png)

图 5.6：Student应用程序的输出

现在让我们学习如何重载运算符

## 第 5 章：C# 5.0 中的面向对象编程

如前所述，运算符重载意味着通过在对象上使用运算符来修改该运算符的功能。当你重载运算符时，你需要创建一个方法，且该方法必须以 `operator` 关键字开头。在本节中，我们正在创建两个应用程序：`UnaryOperatorOverload` 和 `BinaryOperatorOverload`，分别用于重载一元运算符和二元运算符。

列表 5.6：UnaryOperatorOverload应用程序的代码

```c
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace UnaryOperatorOverload
{
    class UnaryOperator
    {
        private int number1;
        private int number2;
        public UnaryOperator()
        {
        }
        public UnaryOperator(int number1, int number2)
        {
            number1 = number1;
            number2 = number2;
        }
        public void showData()
        {
            Console.WriteLine("The numbers are: " + number1 + " and " + number2);
        }
        public static UnaryOperator operator -(UnaryOperator opr)
        {
            UnaryOperator obj = new UnaryOperator();
            obj.number1 = -opr.number1;
            obj.number2 = -opr.number2;
            return obj;
        }
    }
    class MainClass
    {
        public static void Main()
        {
            UnaryOperator opr1 = new UnaryOperator(20, 30);
            Console.WriteLine("Before Operator Overloading");
            opr1.showData();
            UnaryOperator opr2 = new UnaryOperator();
            opr2 = -opr1;
            Console.WriteLine("---------------------------");
            Console.WriteLine("After operator overloading");
            opr2.showData();
            Console.WriteLine("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

在列表 5.6 中，我们创建了一个类 `UnaryOperator`，它包含一个构造函数 `UnaryOperator` 来初始化它的两个变量。`UnaryOperator` 类还包含 `ShowData()` 方法，用于显示类变量的值并重载 `-` 运算符的功能。运算符是通过使用 `operator` 关键字来实现的。接下来，在 `MainClass` 类的 `Main()` 方法中，使用该运算符来显示 `UnaryOperator` 类对象的负值。

图 5.7 显示了列表 5.6 的输出：

![](img/17af790174c480761404624aeed9b30b_250_0.png)

图 5.7：BinaryOperatorOverload应用程序的输出

列表 5.7 显示了 BinaryOperatorOverload 应用程序的代码：

```csharp
Listing 5.7 Code of the BinaryOperatorOverload Application
using System;
using System.Collections.Generic;
using System.Linq;
namespace System.Text;
class BinaryOperator
{
    private int Number1;
    private int Number2;
    public BinaryOperator()
    {
    }
    public BinaryOperator(int number1, int number2)
    {
        Number1 = number1;
        Number2 = number2;
    }
    public void ShowData()
    {
        Console.WriteLine("The numbers are: " + Number1 + " and " + Number2);
    }
    public static BinaryOperator operator +(BinaryOperator opr1,BinaryOperator opr2)
    {
        BinaryOperator opr = new BinaryOperator();
        opr.Number1 = opr1.Number1 + opr2.Number1;
        opr.Number2 = opr1.Number2 + opr2.Number2;
        return opr;
    }
}
class MainClass
{
    public static void Main()
    {
        BinaryOperator opr1 = new BinaryOperator(20, 30);
        opr1.ShowData(); // displays 20 & 30
        BinaryOperator opr2 = new BinaryOperator(30, 40);
        BinaryOperator opr3 = opr1 + opr2;
        opr3.ShowData(); // displays 50 & 70
        Console.WriteLine("\nPress ENTER to quit...");
        Console.ReadLine();
    }
}
```

在列表 5.7 中，我们创建了一个类 `BinaryOperator`，它包含一个构造函数 `BinaryOperator` 来初始化它的变量。`BinaryOperator` 类还包含 `ShowData()` 方法，用于显示类变量的值并重载 `+` 运算符的功能。运算符是通过使用 `operator` 关键字来实现的。在 `MainClass` 类的 `Main()` 方法中，使用该运算符来显示对象的和。

图 5.8 显示了列表 5.7 的输出：

![](img/17af790174c480761404624aeed9b30b_251_0.png)

图 5.8：BinaryOperatorOverload应用程序的输出

## 第 5 章：C# 5.0 中的面向对象编程

让我们学习如何重载方法

C# 允许你创建多个同名但签名不同的方法。让我们创建一个名为 `MethodOverload` 的应用程序，展示如何重载方法。列表 5.8 显示了 `MethodOverload` 的代码：

```csharp
using System;
using System.Collections.Generic;
using System.Text;
namespace MethodOverload
{
    class Shape
    {
        public void Area(int side)
        {
            Console.WriteLine("Area of square: " + (side * side));
```
