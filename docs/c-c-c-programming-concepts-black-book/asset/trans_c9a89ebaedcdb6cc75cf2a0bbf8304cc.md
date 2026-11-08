

## 第18章

在前面的代码中，我们定义了一个索引器，它接受两个字符串参数 data 和 replacementData，如果字符串与 data 匹配，则将其替换为 replacementData。在 Main() 方法中，我们将索引器声明为 emp["USA", "United State Of America"] = "Empty"。这会调用 set 访问器，该访问器尝试查找包含值 USA 的数组元素。如果找到，USA 将被替换为 United State of America。上述代码的输出如下：

```text
Employee[0]: John
Employee[1]: United State of America
Employee[2]: Software Engineer
Employee[3]: 12345
Employee[4]: Developer
```

现在，让我们学习如何引用方法。

### 定义委托

委托是 C# 中的一种元素，我们可以通过它引用方法。这类似于我们在 C++ 中已经学过的函数指针。然而，委托提供了类型安全性，因此它不同于 C++ 中的函数指针。

现在，问题出现了：为什么我们在 C# 程序中需要委托？考虑一个程序，我们希望引用不同的方法，这些方法具有相似的参数类型和相同的返回模式。在这种情况下，我们可以使用委托来实现该功能。此外，如果我们想开发一个适用于所有数据类型的通用算法，而不需要为每种数据类型编写单独的方法，那么我们可以使用委托来实现这一目的。因此，委托为程序实现任何功能提供了更大的灵活性。使用委托时，我们需要考虑以下几点：

-   方法只需要与委托的参数类型和返回类型匹配
-   委托允许将方法作为参数传递

委托使用 delegate 关键字在类定义的开头定义。此外，它们必须在程序中定义其委托处理方法。委托处理方法就是与委托的参数类型和返回类型匹配的方法。让我们在清单18.15中演示委托的功能：

**清单18.15：**展示委托示例

```csharp
using System;
//Defining Delegate
public delegate long Calculator(long item1, long item2);
class Program
{
    public static void Main()
    {
        Items items = new Items(6, 3);
        //Initializing the delegates
        Calculator addition = new Calculator(items.Addition);
        Calculator subtraction = new Calculator(items.Subtraction);
        Calculator multiplication = new Calculator(items.Multiplication);
        Calculator division = new Calculator(items.Division);
        //calling the delegate handler methods using the instance of
        //the delegate
        Console.WriteLine("The result of addition is: "
                          + addition(items.item1, items.item2));
        Console.WriteLine("The result of subtraction is:"
                          + subtraction(items.item1, items.item2));
        Console.WriteLine("The result of multiplication is:"
                          + multiplication(items.item1, items.item2));
        Console.WriteLine("The result of division is: "
                          + division(items.item1, items.item2));
    }
}
class Items
{
    public long item1;
    public long item2;
    public Items(long item1, long item2)
    {
        this.item1 = item1;
        this.item2 = item2;
    }
    //Defining the delegate handler
    public long Addition(long item1, long item2)
    {
        return item1 + item2;
    }
    public long Subtraction(long item1, long item2)
    {
        return item1 - item2;
    }
    public long Multiplication(long item1, long item2)
    {
        return item1 * item2;
    }
    public long Division(long item1, long item2)
    {
        return item1 / item2;
    }
}
```

在清单18.15中，我们定义了一个名为 Calculator 的委托。此外，我们定义了一个名为 Items 的类，它包含委托处理方法或委托将分配的方法。这些方法是 Addition、Subtraction、Multiplication 和 Division。在 Main() 方法中，我们首先实例化了 Items 类的一个对象，然后为四种不同的委托处理方法实例化了 Calculator 委托的四个对象。最后，我们通过使用这些对象传递值来引用各自的方法。上述代码的输出如下：

```text
The result of addition is: 9
The result of subtraction is: 3
The result of multiplication is: 18
The result of division is: 2
```

让我们考虑另一个委托示例，其中我们比较员工的姓名和员工ID，并将结果打印到控制台，如清单18.16所示：

**清单18.16：**展示另一个委托示例

```csharp
using System;
//Defining delegate
public delegate void DelComparisonMethod(object obj1, object obj2);
public class DelExample
{
    Employee[] employee = new Employee[2];
    public DelExample()
    {
        employee[0] = new Employee(1001, "John Mathew", "USA");
        employee[1] = new Employee(1005, "George Mallory", "UK");
    }

    public static void Main()
    {
        DelExample delExam = new DelExample();
        //Instantiating two delegates
        DelComparisonMethod delCompName =
            new DelComparisonMethod(Employee.CompareEmpName);
        DelComparisonMethod delCompID =
            new DelComparisonMethod(Employee.CompareEmpID);
        //calling the delegate handler methods using the delegate
        //instance
        delCompName(delExam.employee[0], delExam.employee[1]);
        delCompID(delExam.employee[0], delExam.employee[1]);
    }
}
public class Employee
{
    public int emp_ID;
    public string name;
    public string address;
    public Employee(int empID, string empName, string empAddress)
    {
        this.emp_ID = empID;
        this.name = empName;
        this.address = empAddress;
    }
    //defining the delegate handler method or the method which will
    //be assigned to delegate
    public static void CompareEmpName(object name1, object name2)
    {
        string name_1 = ((Employee)name1).name;
        string name_2 = ((Employee)name2).name;
        if(String.Compare(name_1, name_2) > 0)
        {
            Console.WriteLine(name_2 + " comes before " + name_1);
        }
        else
        {
            Console.WriteLine(name_2 + " comes after " + name_1);
        }
    }
    public static void CompareEmpID(object ID1, object ID2)
    {
        int ID_1 = ((Employee)ID1).emp_ID;
        int ID_2 = ((Employee)ID2).emp_ID;
        if(ID_1 > ID_2)
        {
            Console.WriteLine(ID_1 + " is greater than " + ID_2);
        }
        else
        {
            Console.WriteLine(ID_1 + " is either equal to or smaller than " + ID_2);
        }
    }
}
```

在上述代码中，我们定义了一个名为 DelComparisonMethod 的委托，它接受两个对象作为参数并返回 bool 类型。然后，我们编写了一个类 Employee，其成员变量包括员工ID、姓名和地址。此外，它有两个委托处理方法，其返回类型和参数类型与委托相同。这两个委托处理方法操作于两种不同的数据类型，因此体现了灵活性。两个处理方法比较 emp_ID 和 name，根据比较结果返回 true 或 false。上述代码还有一个名为 DelExample 的类，其中包含 Main() 方法。这个类首先实例化了 Employee 类的两个实例，然后将它们保存在一个 Employee 数组中。在 Main() 方法中，我们首先创建了 DelExample 类的对象，然后为每个委托处理方法创建了两个委托方法对象。上述代码的输出如下：

```text
George Mallory comes before John Mathew
1001 is either equal to or smaller than 1005
```

### 定义事件

在传统的控制台应用程序中，开发人员无法编写可以在点击某些键时触发的代码。要在点击键时执行事件，我们需要手动遵循某些执行步骤。然而，如今大多数应用程序都是事件驱动的。因此，C# 允许开发人员在程序中编写事件。C# 中的事件是一种委托，只能从声明该委托的类内部调用。

假设一个类包含事件的定义。应用程序可能包含多个类，其中一个类想使用在另一个类中声明的事件。该操作可以通过委托来实现。清单18.17展示了如何在C#程序中使用事件：

**清单18.17：**展示事件示例

```csharp
using System;
//Defining delegate
delegate void PromotedDelegate();
class Program
{
    public static void Main()
    {
        Friend f = new Friend();
        Employee e = new Employee();
        //Adding event handler to PromotedEvent event
        e.PromotedEvent += new PromotedDelegate(f.CallWhenPromoted);
        //Invoking the event
        e.Promote();
    }
}
class Employee
{
    //Defining an event
    public event PromotedDelegate PromotedEvent;
    public void Promote()
    {
        PromotedEvent();
    }
}
class Friend
{
    //This method is called when the event is fired
    public void CallWhenPromoted()
    {
        Console.WriteLine("Thanks for calling.....");
    }
}
```

