
## 11.5 动态多态

C# 有两种实现动态多态的方法。它们是：

- **抽象类：** 它们是包含抽象类成员的一种特殊基类。从抽象类派生的类成员必须实现抽象函数和属性。
- **虚函数：** 它们并不真正存在。它们似乎在某些部分存在。

### 抽象类

抽象类提供类的部分实现。当派生类继承它时，实现才完成。其中有些抽象方法通过派生类来实现。

### 创建抽象类的规则

- 用户不能在抽象类外部声明抽象方法
- 不能创建抽象类的实例
- 从抽象类派生的类必须重写该类的所有方法
- 抽象类不能声明为 sealed

### 示例：

```
Example 44:
using System;
namespace poly
{
    abstract class Result
    {
        public abstract int average();
    }

    class Data: Result
    {
        private int sub1;
        private int sub2;
        public Data(int x, int y)
        {
            sub1 = x;
            sub2 = y;
        }
        public override int average()
        {
            Console.WriteLine("The average is:");
            return (x + y / 2);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Data d = new Data(30, 70);
            int a = d.average();
            Console.WriteLine("Average:{0}",a);
            Console.Read();
        }
    }
}
```

编译并执行代码后，输出为：

平均值为：
平均值：50

### 虚函数

如果你需要一个在类中定义、并且需要由继承类实现的函数，就使用虚函数。继承类会根据需求修改所继承类的功能。方法调用发生在运行时。

**virtual** 关键字用在函数的返回类型之前。

### 示例：

```
Example 45:
using System;
namespace virtual1
{
    class Calculate
    {
        protected int x, y;
        public Calculate(int l = 0, int m = 0)
        {
            x = l;
            y = m;
        }
        public virtual int operation()
        {
            return 0;
        }
    }
    class Multiplication : Calculate
    {
        public Multiplication(int l = 0, int m = 0) : base(l, m)
        {
        }
        public override int operation()
        {
            Console.WriteLine("Multiplication is:");
            return x * y;
        }
    }
    class Addition : Calculate
    {
        public Addition(int l = 0, int m = 0) : base(l, m)
        {
        }
        public override int operation()
        {
            Console.WriteLine("Addition is:");
            return x + y;
        }
    }
    class call
    {
        public void callvalue(Calculate c)
        {
            int z;
            z = c.operation();
            Console.WriteLine("Result:{0}", z);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            call p = new call();
            Multiplication m = new Multiplication(10, 2);
            Addition t = new Addition(15, 16);
            p.callvalue(m);
            p.callvalue(t);
            Console.Read();
        }
    }
}
```

编译并执行代码后，输出为：

乘法结果为：
结果：20
加法结果为：
结果：31

## 第12章 继承与接口

### 12.1 继承简介

继承的概念不仅是 C# 的基础，也是大多数其他编程语言的基础。它允许用户创建从其他类*继承*数据成员和方法的类。继承可以节省用户时间，因为它允许用户在一个核心类中创建若干常用且使用广泛的方法，并让其他类继承该核心类及其所有方法。这样用户就不必在每个类中重复相同的方法。

### 12.2 基类和派生类

继承的结构可以通过几种方式来概括。在本例中，我们有三个类 **A、B** 和 **C**。类 **B** 派生自类 **A**。类 **C** 派生自类 **B**。那么这意味着什么呢？

如果我们用符号表示这些类之间的关系，可以这样表示：

类 A → 类 B → 类 C

- 由于类 **B** 派生自类 **A**，我们说类 **A** 是类 **B** 的父类。我们也可以说类 **B** 是类 **A** 的子类。
- 由于类 **C** 派生自类 **B**，我们说类 **B** 是类 **C** 的父类。我们也可以说类 **C** 是类 **B** 的子类。
- 由于类 **C** 派生自类 **B**，而类 **B** 又派生自类 **A**，我们说类 **A** 是类 **C** 的祖父类。我们也可以说类 **C** 是类 **A** 的孙类。
- 在此例中，由于类 A 不继承其他类，因此该类被称为**基类**。类 **B** 和类 **C** 将声明为派生类。

在此例中，我们使用了父与子的比喻来表示不同类之间的关系，但你还会遇到其他比喻，例如超类（基类）和子类（派生类），它们描述的是相同的关系。

下面是我们如何在代码中声明这些关系：

```
<access – specifier> class <base_class>
{
    ….. 
}
class <derived_class> : <base_class>
{
    ….. 
}
```

### 示例：

### 示例 46：

```
using System;
namespace inheritance1
{
    class Demo
    {
        public void side(int s)
        {
            side = s;
        }
        protected int side;
    }
    //Derived class
    class Area : Demo
    {
        public int getAreaOfSquare()
        {
            return side * side;
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Area a = new Area();
            a.side(4);
            
            //Display the area of square
            Console.WriteLine("Area is: {0}", a.getAreaOfSquare());
            Console.Read();
        }
    }
}
```

编译并执行代码后，输出为：

面积为：16

### 12.3 基类初始化

创建继承结构时，用户必须先从基类（超类）开始。下面是一个示例，说明如何设置基类以及派生类如何从它继承。

**示例：**

```
Example 47:
using System;
namespace Base1
{
    class Square
    {
        //member variables
        protected int side;
        public Square(int s)
        {
            side = s;
        }

        public int CalculateArea()
        {
            return side * side;
        }

        public void Show()
        {
            Console.WriteLine("The value of side is:{0}", side);
            Console.WriteLine("Area is:{0}", CalculateArea());
        }
    }

    class Paint : Square
    {
        private int amount;
        public Paint(int side) : base(side)
        {
        }
        public int Totalamount()
        {
            int amount;
            amount = CalculateArea() * 50;
            return amount;
        }
        public void Show()
        {
            base.Show();
            Console.WriteLine("Total amount is:{0}", Totalamount());
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Paint p = new Paint(3);
            p.Show();
            Console.Read();
        }
    }
}
```

编译并执行代码后，输出为：

边长为：3
面积为：9
总金额为：450

## 12.4 C# 中的接口

接口是一个抽象基类，它声明方法，但不声明方法内部的任何逻辑。本质上，接口可以描述为契约，所有继承该接口的类都必须遵守。接口明确规定了每个派生类必须具有哪些方法和属性。如果派生类中不存在这些方法，就会发生错误。

### 声明接口

**interface** 关键字用于声明接口。它们的默认数据类型为 public。

### 接口声明示例

```
public interface Interface1
{
    void MethodToImplement();
}
```

### 示例：

### 示例 48：

```
using System;
namespace interface1
{
    public interface IStudentInfo
    {
        //interface members

        void ShowData();
    }

    public class StudentInfo : IStudentInfo
    {
        private int srno;
        private string name;
        private string subject;

        public StudentInfo()
        {
            srno = "";

