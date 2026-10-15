

在清单 5.7 中，我们创建了一个类 BinaryOperator，它包含一个构造函数 BinaryOperator，用于初始化其两个变量。BinaryOperator 类还包含 ShowData() 方法来显示类变量的值并重载 +（加法）运算符的功能。+ 运算符是通过使用 operator 关键字来重载的。接下来，在 MainClass 类的 Main() 方法中，使用 + 运算符来显示 BinaryOperator 类对象的数值相加。

图 5.8 显示了清单 5.7 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_242_0.png)

图 5.8：显示 BinaryOperatorOverload 应用程序的输出

让我们现在学习如何重载一个方法。

## 重载一个方法

C# 允许你创建多个同名但签名不同的方法。让我们创建一个名为 MethodOverload 的应用程序（也可在 CD 上获得）来学习如何重载一个方法。

### 清单 5.8：显示 MethodOverload 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MethodOverload
{
public class Shape
{
    public void Area(int Side)
    {
        int SquareArea = Side * Side;
        Console.WriteLine("The Area of Square is: "+SquareArea);
    }
    public void Area(int Length, int Breadth)
    {
        int RectangleArea = Length * Breadth ;
        Console.WriteLine("The Area of Rectangle is: " + RectangleArea);
    }
    public void Area(double Radius)
    {
        double CircleArea = 3.14 * Radius * Radius;
        Console.WriteLine("The Area of Circle is: "+CircleArea);
    }
    public double Area(double Base, double Height)
    {
        double TriangleArea = (Base * Height)/2;
        Console.WriteLine("The Area of Triangle is: "+TriangleArea);
        return TriangleArea;
    }
}
class MainClass
{
    static void Main(string[] args)
    {
        Shape shape = new Shape();
        shape.Area(15);
        shape.Area(10, 20);
        shape.Area(10.5);
        shape.Area(15.5, 20.4);
    }
}
```

```
Console.Write("\nPress ENTER to quit...");
Console.ReadLine();
}
```

在清单 5.8 中，Shape 类的 Area() 方法被重载用于计算正方形、矩形、圆形和三角形形状的面积。在 Main() 方法中，通过传递不同的参数多次调用 Area() 方法。

图 5.9 显示了清单 5.8 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_243_0.png)

图 5.9：显示 MethodOverload 应用程序的输出

让我们现在学习如何重载一个索引器。

## 重载一个索引器

如讨论所述，与运算符和方法类似，索引器也可以被重载。让我们创建一个名为 IndexerOverload 的应用程序（也可在 CD 上获得），它展示了如何重载索引器。清单 5.9 显示了 IndexerOverload 应用程序的代码：

### 清单 5.9：显示 IndexerOverload 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace IndexerOverload
{
    class MyClass
    {
        private string[] MyData;
        private int ArraySize;
        public MyClass(int size)
        {
            ArraySize = size;
            MyData = new string[size];
            for (int i = 0; i < size; i++)
            {
                MyData[i] = "Datavalue";
            }
        }
        public string this[int Position]
        {
            get
            {
                return MyData[Position];
            }
            set
            {
                MyData[Position] = value;
            }
        }
        public string this[string data]
        {
            get
            {
                int Count = 0;
                for (int i = 0; i < ArraySize; i++)
```

```
{
    if (MyData[i] == data)
    {
        Count=Count+1;
    }
}
return Count.ToString();
}
set
{
    for (int i = 0; i < ArraySize; i++)
    {
        if (MyData[i] == data)
        {
            MyData[i] = value;
        }
    }
}
}
class MainClass
{
    static void Main(string[] args)
    {
        int size = 10;
        MyClass MyIndexer = new MyClass(size);
        MyIndexer [9] = "Hello";
        MyIndexer [3] = "Welcome";
        MyIndexer [5] = "Good Morning";
        MyIndexer [7] = "Good Night";
        MyIndexer ["DataValue"] = "Have a Nice Day";
        Console.WriteLine("\nIndexer Output");
        Console.WriteLine("----------------");
        for (int i = 0; i < size; i++)
        {
            Console.WriteLine("MyIndexer[{0}]: {1}", i, MyIndexer [i]);
        }
        Console.WriteLine("\nNumber of \"Have a Nice Day\" Entries: {0}", MyIndexer ["Have a Nice Day"]);
        Console.Write("\nPress ENTER to quit...");
        Console.ReadLine();
    }
}
}
```

在清单 5.9 中，我们定义了两个索引器，一个使用 int 类型参数 Position，另一个使用 string 类型参数 data。这些索引器用于在 MainClass 类的 Main() 方法中显示传递的不同字符串数据的值。

图 5.10 显示了清单 5.9 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_244_0.png)

图 5.10：显示 IndexerOverload 应用程序的输出

让我们现在学习如何使用 new 运算符隐藏一个方法。

## 重载 new 运算符

new 运算符用于在派生类中覆盖基类方法，而不使用 virtual 关键字。让我们创建一个名为 MethodHiding 的应用程序（也可在 CD 上获得），它展示了派生类方法如何覆盖基类方法。清单 5.10 显示了 MethodHiding 应用程序的代码：

### 清单 5.10：显示 MethodHiding 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MethodHiding
{
    class BaseClass
    {
        public void MyMethod()
        {
            Console.WriteLine("I am in Base Class");
        }
    }

    class DerivedClass : BaseClass
    {
        public new void MyMethod()
        {
            Console.WriteLine("I am in Derived Class");
        }
    }

    class MainClass
    {
        static void Main(string[] args)
        {
            BaseClass bc = new BaseClass();
            DerivedClass dc = new DerivedClass();
            bc.MyMethod();
            dc.MyMethod();
            bc = new DerivedClass();
            bc.MyMethod(); //BaseClass Method
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
```

在清单 5.10 中，我们在 DerivedClass 类的 MyMethod() 方法中重载了 new 运算符，以覆盖 BaseClass 类的 MyMethod() 方法。

图 5.11 显示了清单 5.10 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_245_0.png)

## 图 5.11：显示 MethodHiding 应用程序的输出

让我们现在学习如何使用 virtual 关键字重写一个方法。

## 重写基类方法

在 C# 中，你可以在基类中创建虚拟方法，这些方法可以在派生类中被重写以改变基类方法的行为。你可以使用 virtual 关键字在基类中声明一个函数为虚拟；然而，要在派生类中重写此函数，你需要使用 override 关键字。让我们创建一个名为 MethodOverriding 的应用程序（也可在 CD 上获得），它展示了使用 virtual 和 override 关键字重写方法的示例。清单 5.11 显示了 MethodOverriding 应用程序的代码：

### 清单 5.11：显示 MethodOverriding 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MethodOverriding
{
    class Program
    {
        static void Main(string[] args) {
            Person p = new Person();
            p.setAge(18);
            AdultPerson ap = new AdultPerson();
            ap.setAge(18);
            Console.WriteLine("Person Age: {0}", p.getAge());
            Console.WriteLine("AdultPerson Age: {0}", ap.getAge());
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }

    public class Person
    {
        private int fAge;
        public Person() {
            fAge = 21;
        }

        public virtual void setAge(int age) {
            fAge = age;
        }

        public virtual int getAge() {
            return fAge;
        }
    }

    public class AdultPerson : Person
    {
        public AdultPerson() { }
        override public void setAge(int age)
        {
            if (age > 21)
                base.setAge(age);
        }
    }
```

在清单 5.11 中，我们创建了 Person 和 AdultPerson 类，其中 AdultPerson 类是 Person 类的派生类。Person 类包含两个虚拟函数 setAge 和 getAge。AdultPerson 类通过使用 override 关键字重写了基类的 setAge() 方法。

图 5.12 显示了清单 5.11 的输出：

