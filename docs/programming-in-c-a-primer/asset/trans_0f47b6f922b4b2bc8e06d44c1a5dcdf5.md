
```csharp
namespace CaseStudy14
{
    interface HPSystem
    {
        void ListComputer();
        void ShowComputerColor(string str);
        void ShowComputerFeature(string feature);
        void ShowComputerPrice(double price);
    }
    class ComputerList : HPSystem
    {
        string comptercolor = "";
        string computernames = "";
        public void ListComputer()
        {
            computernames = "1.      HP Pavilion Media Center m8000\n";
            computernames = computernames + "\n2.      HP Compaq DC5750 PC";
            computernames = computernames + "\n3.      HP Compaq DX2300 pc";
            Console.WriteLine("The HP Computers are :\n\n" + computernames);
        }
        public void ShowComputerColor(string color)
        {
            this.comptercolor = color;
            Console.WriteLine("\nThe color of the systems are : " + comptercolor + "\n");
        }
        public void ShowComputerFeature(string feature)
        {}
        public void ShowComputerPrice(double price) {}
    }
    class ShowHPCompterDetails : ComputerList
    {
        string Computerfeature = "";
        double ComputerPrice = 0;
        public void ShowComputerFeature(string feature)
        {
            this.Computerfeature = feature;
            Console.WriteLine("The features of the systems are " +Computerfeature);
        }
        public void ShowComputerPrice(double price)
        {
            this.ComputerPrice = price;
            Console.WriteLine("\nThe Prices of the systems are:" +ComputerPrice);
        }
    }
    class ShowComputerFeatures
    {
        static void Main(string[] args)
        {
            ShowHPCompterDetails hpm = new ShowHPCompterDetails();
            hpm.ListComputer();
            hpm.ShowComputerColor("Steel Gray");
            hpm.ShowComputerColor("Black");
            hpm.ShowComputerColor("Gray");
            hpm.ShowComputerFeature("Pentium PIV PC Dual Core2");
            hpm.ShowComputerFeature("Pentium PIV 2.5GHz processor");
            hpm.ShowComputerFeature("Pentium PIV PC Dual Core");
            hpm.ShowComputerPrice(63000);
            hpm.ShowComputerPrice(30000);
            hpm.ShowComputerPrice(45000);
        }
    }
}
```

## 备注

接口特性使我们在 C# 应用程序中能够实现多重继承的概念。它还提供了代码复用的好处，可以将一个应用程序中定义的代码复用于另一个应用程序。在接口中，方法被声明为抽象方法，不包含任何实现代码。在 C# 中，接口可以由多个类实现。

## 常见编程错误

- 将数据字段声明为成员。
- 将成员声明为 static。
- 使用可见性修饰符来声明成员。
- 忘记在方法声明末尾放置分号。
- 忘记在实现类中实现某个成员。
- 忘记将类对象强制转换为接口类型。
- 在显式实现方法上使用访问修饰符。
- 试图创建接口的实例。
- 忘记将实现方法声明为 public。

## 复习题

14.1 判断以下陈述是否正确（true/false）。

- (a) 与类一样，接口只能继承一个接口。
- (b) 接口的所有成员都是隐式抽象的。
- (c) 接口的成员可以被声明为 private。
- (d) 接口通常用于声明常量数据字段。
- (e) 接口不能扩展类。
- (f) 在父接口中声明的方法必须在子接口中实现。
- (g) 类可以实现任意数量的接口。
- (h) 任意数量的类都可以实现一个接口。
- (i) 接口可以被视为抽象类的替代方案。
- (j) 抽象类可以实现接口。
- (k) 我们可以使用 new 运算符创建接口的实例。

14.2 什么是接口？

14.3 类和接口之间的主要区别是什么？

14.4 类和接口之间的相似之处是什么？

14.5 接口的所有成员都被隐式设置为 public。为什么？

14.6 接口的所有成员都是隐式抽象的。这意味着什么？

14.7 当接口继承另一个接口时，我们称之为扩展接口；但当类继承接口时，我们称之为实现接口。为什么？

14.8 什么是显式接口实现？何时使用？

14.9 C# 支持多重继承吗？如果支持，如何实现？

14.10 使用接口，我们可以在类中实现多重继承特性。如何实现？

14.11 我们如何表示类 Class1 派生自基类 BaseClass，并实现 FileRead 和 FileWrite 接口？

14.12 我们可以将两个或更多接口组合在一起。请讨论。

14.13 描述实现接口的各种形式，并为每种情况给出 C# 代码示例。

14.14 给出一个接口可用于支持多重继承的示例。

14.15 抽象类可以实现接口吗？如果可以，接口方法是如何实现的？

14.16 区分抽象类和接口。

14.17 找出以下接口定义和实现中的错误：

- (a)

  ```csharp
  new interface A
  {
      void M1();
  };
  ```

- (b)

  ```csharp
  private interface A {}
  public interface B : A {}
  ```

- (c)

  ```csharp
  interface A {}
  interface B {}
  interface C extends A, B
  {}
  ```

- (d)

  ```csharp
  interface A {}
  class B {}
  class C : A, B
  {}
  ```

- (e)

  ```csharp
  interface A {}
  class B implements A
  {}
  ```

- (f)

  ```csharp
  interface A
  {
      void M1();
      int n;
  }
  ```

- (g)

  ```csharp
  interface X
  {
      static void Fun();
  }
  ```

- (h)

  ```csharp
  interface Y
  {
      public void Display ();
      int count {get;}
  }
  ```

- (i)

  ```csharp
  interface P
  {
      abstract void Paint ();
  }
  ```

- (j)

  ```csharp
  interface A
  {
      void Mul ();
  }
  interface B : A
  {
      void Mul ();
  }
  ```

## 调试练习

### 14.1 定位并更正下面程序中的错误。

```csharp
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp1_chap14
{
    public abstract class Car
    {
        abstract void RemoveAllFuses();
        abstract void StartEngine();
    }
    class Seat : Car
    {
        public override void RemoveAllFuses()
        {
        }
        public override void StartEngine()
        {
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Seat c = new Seat();
            c.RemoveAllFuses();
        }
    }
}
```

### 14.2 找出下面程序中的错误。

```csharp
using System;
using System.Collections.Generic;
using System.Text;

namespace debugApp2_chap14
{
    interface Dimensions
    {
        float Length();
        float Width();
    }
    interface MetricDimensions
    {
        int Length();
        int Width();
    }
    class Box : Dimensions, MetricDimensions
    {
        float lengthInches;
        float widthInches;
        public Box(float length, float width)
        {
            lengthInches = length;
            widthInches = width;
        }
        // Explicitly implement the members of IEnglishDimensions:
        float Dimensions.Length()
        {
            return lengthInches;
        }
        float Dimensions.Width()
        {
            return widthInches;
        }

        float MetricDimensions.Length()
        {
            return lengthInches * 2.54f;
        }
        float MetricDimensions.Width()
        {
            return widthInches * 2.54f;
        }
        static void Main()
        {
            Box box1 = new Box(30.0f, 20.0f);
            // Declare an instance of the English units interface:
            Dimensions eDimensions = (Dimensions)box1;
            // Declare an instance of the metric units interface:
            MetricDimensions mDim = (MetricDimensions)box1;
            // Print dimensions in English units:
            System.Console.WriteLine("Length(in): {0}", eDimensions.Length());
            System.Console.WriteLine("Width (in): {0}", eDimensions.Width());
            // Print dimensions in metric units:
            System.Console.WriteLine("Length(cm): {0}", mDim.Length());
            System.Console.WriteLine("Width (cm): {0}", mDim.Width());
        }
    }
}
```

### 14.3 检查下面程序中的语法错误并更正。

```csharp
using System;
using System.Collections.Generic;
using System.Text;

namespace debugApp3_chap14
{
    class Program
    {
        public class ShowValues
        {
            void Show();
        }

        public class CharContainer :: ShowValues
        {
            public void Show()
            {
                // Do character type sorting here.
                Console.WriteLine("From CharContainer.");
            }
        }

        public class NumberContainer :: ShowValues
        {
            public void Show()
            {
                // Do numeric type sorting here.
                Console.WriteLine("From NumberContainer.");
            }
        }

        public void ShowAll(ShowValues[] sortobj)
        {
            foreach (ShowValues sv in sortobj)
            {
                sv.Show();
            }
        }

        static void Main(string[] args)
        {
            Program Obj = new Program();
            obj.ShowAll(new ShowValues[2] { new CharContainer(), new NumberContainer() }
            );
        }
    }
}
```
