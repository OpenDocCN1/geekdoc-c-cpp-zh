
图 6.11：MyDelegate 程序的输出

现在让我们来看这个程序最重要的部分。以下代码段显示了如何在使用的类中定义委托：

```csharp
public delegate Boolean Incrementaccount(Account a, double d);
public delegate Boolean Decrementaccount(Account a, double d);
if (d < 0)
    dec(accounts[n], -d);
else
    inc(accounts[n], d);
```

创建适当类型的新委托并将其连接到执行处理的真实方法见以下代码段：

```csharp
new AccountDB.Incrementaccountdelegate(id =
new AccountDB.Incrementaccountdelegate(ah.AccountInc);
new AccountDB.Decrementaccountdelegate(ah.AccountDec);
```

让我们学习如何实例化和调用委托

# 声明和实例化委托

让我们创建一个名为 `SampleDelegate` 的控制台应用程序，用于声明和实例化委托。列表 6.10 显示了 `SampleDelegate` 应用程序 `Program.cs` 文件的代码：

列表 6.10：SampleDelegate 程序的代码

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SampleDelegate
{
    public struct Employee
    {
        public string strname;
        public string Lname;
        public decimal Sal;
        public bool Stat;
        public Employee(string name, string lname, decimal salary, bool status)
        {
            strname = name;
            Lname = lname;
            Sal = salary;
            Stat = status;
        }
    }
    // 声明委托类型
    delegate void EmployeeDelegateOper(Employee employee);

# 立即解决方案

public class EmpDOB {
    // 员工数据库中所有员工列表：
    ArrayList List = new ArrayList();
    // 向数据库中添加员工：
    public void addEmp(string name, string Iname, decimal salary, bool status) {
        List.add(new Employee(name, Iname, salary, status));
    }
    public void EmpStatus(EmployeeDelegateOper ProcEmp) {
        foreach (Employee b in List) {
            if (b.Stat)
                ProcEmp(); //调用委托
        }
    }
}

// 使用 EmployeeData 类类
namespace EmpClient {
    class Salary {
        int TotalEmp = 0;
        decimal EmpSalary = 0.0;
        internal void AddSalary(Employee employee) {
            TotalEmp += 1;
            EmpSalary += employee.Sal;
        }
        internal decimal AvgSalary() {
            return EmpSalary / TotalEmp;
        }
    }
    // 测试员工数据库的类：
    class TestEmployees {
        static void Print(Employee b) {
            System.Console.WriteLine("{0}", b.strname);
        }
        static void Main() {
            EmpDOB empDatabase = new EmpDOB();
            // 向数据库中添加员工
            AddEmployee(empDatabase);
            System.Console.WriteLine("Status of the Employees:");
            Salary salder = new Salary();
            // 与非静态方法关联的新对象
            // 注意：以下代码在原始 OCR 中关于委托类型似乎有逻辑错误
            // 但保留了文本结构。
            empDatabase.EmpStatus(salder.AddSalary()); 
            Console.WriteLine("Average Salary of the Employee: {0:#.#}");
            salder.AvgSalary();
            Console.Write("Press ENTER to exit...");
            Console.ReadKey();
        }
        // 使用一些员工初始化员工数据库：
        static void AddEmployee(EmpDOB empDatabase) {
            empDatabase.AddEmp("Peter", "wilkins", .100m, true);
            empDatabase.AddEmp("Tom", "Johnson", 25.35m, true);
            empDatabase.AddEmp("Pat", "David", 50.90m, false);
            empDatabase.AddEmp("Henry", "Williams", 15.20m, true);
        }
    }
}
}
```

图 6.12 显示了上述代码的输出：

![](img/17af790174c480761404624aeed9b30b_281_0.png)

图 6.12：SampleDelegate 程序的输出

列表 6.10 显示了声明、实例化和使用委托的代码。`EmpDB` 类封装了数据库，维护着员工数据库。它包含一个方法 `EmpStatus()`，该方法可以识别数据库中的所有正式员工，并为每个员工调用委托。如果某个员工的状态值为 `true`，则会打印该员工。`TestEmployees` 类使用 `DelegateDelegate` 来打印员工的名字和正式员工的平均薪资。在列表 6.10 中，以下语句声明了一个委托：

```csharp
public delegate void DelegateOper(Employee employee);
```

在声明委托类型后，我们需要创建一个带有方法的委托对象。在列表 6.10 中，使用以下语句将 `Print()` 方法传递给 `EmpStatus()` 方法：

```csharp
empDatabase.EmpStatus(Print);
```

最后，在创建委托后，使用以下语句调用委托：

```csharp
Proceed();
```

让我们学习创建多播委托。

# 创建多播委托

多播委托允许你将针对给定事件的多个委托处理程序组合到一个链表中。此列表可以在程序控制下直接调用，也可以通过触发事件机制间接调用。

多播委托的优势在于你可以修改这些委托的输入。例如，如果你想跟踪分配给委托的事件链，可以增加计数器并作为输入参数传递给委托处理程序。或者，如果你更了解它们的处理过程，也可以简单地跳过处理程序。

委托系统的核心是 `Combine()` 方法。该方法允许你创建处理程序的链表。`GetInvocationList` 方法用于各个处理程序检索到一个简单的数组中以便逐个调用。列表 6.11 显示了创建多播委托的代码：

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace MulticastDelegates
{
    public class EventHandler1
    {
        public static void HandleEvent(string s)
        {
            Console.WriteLine("EventHandler1 called {0}", s);
        }
    }

    public class EventHandler2
    {
        public static void HandleEvent(string s)
        {
            Console.WriteLine("EventHandler2: {0}", s);
        }
    }
}

public class EventClass
{
    public delegate void OnEventFired(string s);
    private string fs;
    public OnEventFired evf = null;
    public EventClass(string s)
    {
        fs = s;
        OnFireEvent();
    }
    public void setString(string s)
    {
        fs = s;
        OnFireEvent();
    }
    private void OnFireEvent()
    {
        // 触发事件
        if (evf != null)
            evf(fs);
    }
    public void CallAllEventHandler(string s)
    {
        if (evf == null)
            return;
        Delegate[] list = evf.GetInvocationList();
        for (int i = 0; i < list.Length; ++i)
        {
            OnEventFired oef = (OnEventFired)list[i];
            ofe(s);
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        // 创建处理程序
        EventClass.OnEventFired ev1 = new EventClass.OnEventFired(MulticastDelegates.EventHandler1.HandleEvent);
        EventClass.OnEventFired ev2 = new EventClass.OnEventFired(MulticastDelegates.EventHandler2.HandleEvent);
        // 创建类实例
        EventClass e = new EventClass("Hello world");
        // 设置处理程序
        e.evf = ev1;
        e.evf += ev2;
        // 更改某些内容以便进行调用
        e.setString("Hello");
        // 调用所有处理程序
        e.CallAllEventHandler("Goodbye");
        Console.write("\nPress ENTER to quit...");
        Console.ReadLine();
    }
}
```

图 6.13 显示了上述代码的输出：

# 第 6 章：指针、委托和事件

![](img/17af790174c480761404624aeed9b30b_283_0.png)

图 6.13：MulticastDelegates 程序的输出

程序的输出显示，字符串是相同的，无论这种变化是由内部数据的间接修改引起的（通过调用 `setString()` 方法），还是通过对事件处理程序链表中的处理程序进行物理调用引起的。

现在让我们学习如何实现协变（covariance）。

## 实现协变

我们在本章的*深度*（*Depth*）节中讨论过，协变允许你使用一个带有派生类型作为委托的方法。让我们创建一个名为 *Covariance* 的控制台应用程序，演示委托如何使用派生返回类型。列表 6.12 显示了应用程序 `Program.cs` 文件的代码：

列表 6.12：Covariance 应用程序的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Covariance
{
    class X
    {
        public X CreateX()
        {
            Console.WriteLine("This is class X");
            return new X();
        }
    }
    class Y : X
    {
        public Y CreateY()
        {
            Console.WriteLine("This is class Y");
            return new Y();
        }
    }
    class Program
    {
        public delegate void Foo(object obj);
        public static void Main(string[] args)
        {
            Foo obj1 = new X().CreateX();
            Foo obj2 = new Y().CreateY();
            Foo(obj1);
            Foo(obj2);
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

图 6.14 显示了上述代码的输出：

![](img/17af790174c480761404624aeed9b30b_284_0.png)

图 6.14：Covariance 应用程序的输出

在这个应用程序中，我们定义了两个类 `X` 和 `Y`。`Y` 继承自类 `X`。现在，可以定义一个返回类型为 `X` 的委托，但此委托可以用于返回类型 `X` 或 `Y`。定义的委托返回基类 `X`，尽管你可以使用同一个委托来返回已定义类 `Y` 的对象。

现在让我们学习如何实现逆协变（contravariance）。

## 实现逆协变

正如早些时候在输入（In）节中讨论的那样，逆协变允许你使用带有派生参数方法的委托。让我们创建一个名为 `Contravariance` 的控制台应用程序，演示如何通过委托使用逆协变。列表 6.13 显示了 `Contravariance` 应用程序 `Program.cs` 文件的代码：

列表 6.13：Contravariance 应用程序的代码
