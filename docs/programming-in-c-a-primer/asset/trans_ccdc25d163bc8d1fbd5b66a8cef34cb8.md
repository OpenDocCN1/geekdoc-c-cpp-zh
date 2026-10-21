

```
static int Main(string[] args)
{
	double principal, rate, time, amount;
	double duration = 0;
	string durationname = null;
	Interest interest = new Interest();
	ShowInterest si = new ShowInterest(AddupAmount);
	Console.WriteLine("This is a program to Calculate Loan Amount in Simple Interest.");
	Console.WriteLine("");
	principal = interest.Principal();
	rate = interest.InterestRate();
	time = interest.Time(duration);
	amount = interest.CalculateInterest(principal, rate, time);
	double Amount = si(principal, amount);
	durationname = "years";
	Console.WriteLine("");
	Console.WriteLine("-----------------------------------------------");
	Console.WriteLine("Calculated Loan");
	Console.WriteLine("-----------------------------------------------");
	Console.WriteLine("Principal: {0}", principal);
	Console.WriteLine("Interest: {0}", rate / 100);
	Console.WriteLine("Period: {0} {1}", time, durationname);
	Console.WriteLine("Interest to be paid on Loan (Rs.): {0}", amount);
	Console.WriteLine("Total Amount to pay after \"{0}\" years (Rs.): {1}", time, Amount);
	Console.WriteLine("-----------------------------------------------\n");
	return 0;
}

static double AddupAmount(double val1, double val2)
{
	return val1 + val2;
}
```

委托允许你在 C# 应用程序中实现回调技术，其中一个对象向发送消息的对象发送回调消息。C# 中的委托充当另一个方法的 方法。委托的主要功能是在创建时调用其中封装的方法。

+   16.1 判断以下陈述是真还是假。
+   (a) 委托代表类的一个数据成员。
+   (b) 委托可以持有任意类的一个方法的引用。

## 332 Programming in C#
+   - (c) 委托只能在类内部定义。
+   - (d) 委托类型可以从另一个委托类型派生。
+   - (e) 为委托类型使用可访问性修饰符是可选的。
+   - (f) new 修饰符可用于声明任何委托。
+   - (g) 委托方法的签名必须与委托的签名匹配。
+   - (h) 委托方法的返回类型必须与委托的返回类型匹配。
+   - (i) 委托只能持有对实例方法的引用。
+   - (j) 委托方法必须始终返回值。
+   - (k) 总是可以对委托的实例执行加法操作。
+   - (l) 事件是一个委托类型成员。

+   - 16.2 什么是委托？它用于什么？
+   - 16.3 委托是值类型还是引用类型？
+   - 16.4 创建和使用委托涉及的步骤有哪些？
+   - 16.5 讨论委托声明的语法。
+   - 16.6 可以应用于委托的修饰符有哪些？
+   - 16.7 我们何时需要使用 new 修饰符？
+   - 16.8 给出至少两个委托声明的示例。
+   - 16.9 委托可以在程序的哪些地方定义？
+   - 16.10 什么是委托方法？
+   - 16.11 委托方法的条件是什么？
+   - 16.12 委托的特殊特性是什么？
+   - 16.13 我们如何创建委托的实例？
+   - 16.14 我们如何调用委托？调用委托时会发生什么？
+   - 16.15 什么是多播委托？
+   - 16.16 多播委托的特性是什么？
+   - 16.17 什么是事件？
+   - 16.18 描述事件声明的语法。
+   - 16.19 给出事件使用的两个典型示例。
+   - 16.20 什么是事件处理程序？它是如何设计的？
+   - 16.21 event 关键字做什么？

+   - 16.22 找出以下委托声明中的错误，如有：
+   
+   (a) delegate D1( );
+   
+   (b) int delegate D2 ( );
+   
+   (c) delegate void D3 (x,y);
+   
+   (d) delegate void D4 (int a, int b) { }
+   
+   (e) private double D5 (double x);
+   
+   (f) public delegate int D6 (int x, int y)

```
delegate D1( );
int delegate D2 ( );
delegate void D3 (x,y);
delegate void D4 (int a, int b) { }
private double D5 (double x);
public delegate int D6 (int x, int y)
```

+   - 16.23 给定委托
+   
+   delegate double D1 (int x, int y);
+   以下哪些方法可以被它封装？
+   
+   (a) int M1 (int x, int y) { }
+   
+   (b) double M2 (double a, double b) { }

```
delegate double D1 (int x, int y);
int M1 (int x, int y) { }
double M2 (double a, double b) { }
```

+   (c) static double M3 (int x, int y) {}
+   (d) public double M4 (int x, y ) {}
+   (e) private double M5 (int a, int b) {}

# 16.24 给定以下代码段

```
delegate void D1 ( );
class A
{
    public void M ( ) {}
}
```

以下哪些委托实例化语句是正确的？

+   (a) D1 d1 = new D1 (M);
+   (b) D1 d1 = new (A.M);
+   (c) D1 d1 = new D1 (A,M);
+   (d) D1 D1 = new ((new A () ).M);

# Debugging Exercises

16.1 调试以下用于演示 C# 中方法返回类型的程序。

```
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp1_chap16
{
    int ResultDisplay(int i, int j);
    class Show
    {
        public static MathsFunc(int x, int y)
        {
            return ((x * x + 2*x*y + y * y) / (x+y));
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            ResultDisplay rd = new ResultDisplay(Show.Mathsfync());
            int getResult = rd(1, 2);
            Console.WriteLine("The value of the function is " + getResult);
        }
    }
}
```

16.2 找出以下 C# 委托示例中的错误。

```
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp2_chap16
```

## 334 Programming in C#

```
public delegate void MsgHandler();
class Class1
{
public MsgHandler msg;
public void Show()
{
msg();
}
}
class Class2 : Class1
{
public Class2()
{
msg += MsgHandler(Display);
Show();
}
public void Display()
{
Console.WriteLine ("This is an example of working of a delegate.");
}
}
class Program
{
static void Main(string[] args)
{
Class2 cl = new Class2();
cl.Display();
}
}
```

```
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp3_chap16
{
delegate void Delegate1(int i);
class DelegateExample
{
string name;
static void Main(string[] args)
{
Delegate1 dl1 = new Delegate1(DelegateExample.Show);
DelegateExample de = new DelegateExample();
de.name = "Display method returns ";
Delegate1 dl2 = new Delegate1(de.Display);
Console.WriteLine (dl1(455));
}
}
}
```

```
```csharp
Console.WriteLine(d12(77));
string Show(int i)
{
	return string.Format("Show method returns : {0}", i);
}
void Display(int i)
{
	return string.Format("{0} {1}", name, i);
}
}
```
```

# 16.4 修正以下使用 static 关键字的程序。

```
```csharp
using System;
using System.Collections.Generic;
using System.Text;

namespace debugApp4.chap16
{
	class Program
	{
		delegate void MulticastDelegate(int a);
		public class DelegateClass
		{
			public void Method1(int a)
			{
				Console.WriteLine(a + " is passed in the Method1.");
			}
			static public void staticMethod1(int b)
			{
				Console.WriteLine(b + " is passed in the staticMethod1.");
			}
		}
		static void Main(string[] args)
		{
			DelegateClass dc = new DelegateClass();
			MulticastDelegate md = new MulticastDelegate(dc.Method1());
			md(447);
			Console.WriteLine("");
			md += new MulticastDelegate(DelegateClass.staticMethod1());
			md(689);
		}
	}
}
```
```

## Managing Console I/O Operations

# 17.1 Introduction

程序被编写来操作给定的数据集并生成作为输出的处理后的数据，遵循熟悉的输入-处理-输出循环。因此，了解如何提供输入数据以及如何以期望的格式呈现结果至关重要。

我们已经看到了使用 Console.WriteLine() 方法产生简单输出以及 Console.ReadLine() 方法从键盘读取输入。我们将在本章更详细地考虑 C# 支持的控制台 I/O 操作。

# 17.2 THE CONSOLE CLASS

用于从控制台读取和写入的方法由 System.Console 类提供。此类为我们提供了对标准输入、标准输出和标准错误流的访问，如表 17.1 所示。

# Table 17.1 Input/Output streams

| 流对象 | 代表 |
|---|---|
| Console.In | 标准输入 |
| Console.Out | 标准输出 |
| Console.Error | 标准错误 |

标准输入系统 Console.In 默认从键盘获取输入。我们也可以重定向它以从文件接收输入。标准输出流 Console.Out 默认将输出发送到屏幕。我们也可以将输出重定向到文件。

标准错误流 Console.Error 通常将错误消息发送到屏幕。即使标准输出被发送到文件，任何错误消息仍会显示在屏幕上。

# 17.3 CONSOLE INPUT

控制台输入流对象支持两种从键盘获取输入的方法：

+   - Read() 返回一个字符作为 int。无更多字符可用时返回 -1。
+   - ReadLine() 返回包含一行文本的字符串。无更多行可用时返回 null。

