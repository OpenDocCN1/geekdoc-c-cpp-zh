

## 第 9 章 使用类和对象

为了使 `BinarySearch()` 和 `Sort()` 等方法正常工作，为你为类创建 `CompareTo()` 方法必须返回一个整数值。表 9-2 显示了每个版本的 `CompareTo()` 应该提供的返回值。

| 返回值 | 含义 |
|---|---|
| 负数 | 此实例小于被比较的对象。 |
| 零 | 此实例与被比较的对象相等。 |
| 正数 | 此实例大于被比较的对象。 |

**表 9-2** `IComparable.CompareTo()` 方法的返回值

当你 de创建一个包含 `IComparable.CompareTo()` 方法的类时，该方法是一个实例方法，并接收用于调用它的对象的引用。第二个对象会被传递给该方法；你必须先将传递的对象转换、强制转换（cast）为与调用对象的类相同的类型，然后比较你想从该对象和传递的对象中获取的相应字段。例如，图 9-40 显示了一个 `Employee` 类，它包含一个阴色的 `CompareTo()` 方法，并根据 `idNumber` 字段的内容来比较 `Employee` 对象。

```csharp
class Employee : IComparable {
    public int idNumber {get;set;}
    public double Salary {get;set;}
    int IComparable.CompareTo(Object o) {
        int returnVal;
        Employee temp = (Employee)o;
        if(this.idNumber > temp.idNumber)
            returnVal = 1;
        else
            if(this.idNumber < temp.idNumber)
                returnVal = -1;
            else
                returnVal = 0;
        return returnVal;
    }
}
```

**图 9-40** 使用 `IComparable` 接口的 `Employee` 类

图 9-40 中的 `Employee` 类在类类头部中使用冒号和 `IComparable` 来表示这是一个接口。阴色的方法是一个实例方法；也就是说，它“属于”一个 `Employee` 对象。当另一个 `Employee` 作为 `Object` 传递进来时，它被强制转换为 `Employee` 并存储在 `temp` 变量中。比较此 `Employee` 和传递的 `Employee` 的 `idNumber` 值，并返回三个整数之一。例如，如果你声明了两个名为 `worker1` 和 `worker2` 的 `Employee`，你可以使用语句：
`int answer = worker1.CompareTo(worker2);`

在 `Employee` 类的 `CompareTo()` 方法中，`worker1` 将是“this” Employee——即方法中的控制 Employee（调用者 `Employee` 对象）。`temp` Employee 将是 `worker2`。如果 `worker1` 的 ID 编号比 `worker2` 高，则 `answer` 的值将为 1。

图 9-41 显示了一个使用 `Employee` 类的程序。该程序声明了一个具有不同 ID 编号和薪水的五个 `Employee` 对象数组；ID 编号是无序的，以证明 `Sort()` 方法运行正常。程序还声明了一个 ID 编号为 222 的 `seekEmp` 对象。程序对数组排序，显示排序后的元素，然后找到与 `seekEmp` 对象匹配的数组元素。图 9-42 显示了程序的执行结果。

```csharp
using System;
using static System.Console;
class ComparableEmployeeArray
{
    static void Main()
    {
        Employee[] empArray = new Employee[5];
        int x;
        for(x = 0; x < empArray.Length; ++x) {
            empArray[0].IdNumber = new Employee(333);
            empArray[1].IdNumber = 444;
            empArray[2].IdNumber = 555;
            empArray[3].IdNumber = 111;
            empArray[4].IdNumber = 222;
        }
        Employee seekEmp = new Employee();
        seekEmp.IdNumber = 222;
        Array.Sort(empArray);
        WriteLine("Sorted employees:");
        for(x = 0; x < empArray.Length; ++x)
            WriteLine("Employee#{0}: {1} {2}",
                empArray[x].IdNumber,empArray[x].Salary.ToString("C"));
        x = Array.BinarySearch(empArray,seekEmp);
        WriteLine("Employee#{0} was found at position {1}",
            seekEmp.IdNumber, x);
    }
}
```

**图 9-41** `ComparableEmployeeArray` 程序

```
Sorted employees:
Employee #0: 111 $0.00
Employee #1: 222 $0.00
Employee #2: 333 $0.00
Employee #3: 444 $0.00
Employee #4: 555 $0.00
Employee #222 was found at position 1
```

**图 9-42** `ComparableEmployeeArray` 程序的输出

注意，`seekEmp` 对象根据 `idNumber`——而不是薪水——匹配数组中第二个位置的 `Employee`，因为 `Employee` 类中的 `CompareTo()` 方法仅使用 `idNumber` 进行比较。你可以编写代码，要求在返回正数之前，`idNumber` 和 `salary` 值都必须匹配。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_426_0.png)

## 你来做做

## 创建对象数组

在接下来的步骤中，你将创建一个 `Student` 对象数组。你将提示用户输入数据以填充数组，并在显示所有数据之前按 `Student ID` 对数组进行排序。

- 打开 `CreateStudents2` 程序并立即另存为 `CreateStudents3`。将类名更改为 `CreateStudents3`。删除 `Main()` 方法中的所有现有语句，保留大括号。在大括号之间，声明一个包含八个 `Student` 对象的数组。还要声明一个变量作为数组，并声明三个变量用于在构造 `Student` 对象之前临时存储用户的输入数据。

```csharp
Student[] students = new Student[8];
int x;
int id;
string name;
double gpa;
```

- 在循环中，调用 `GetData()` 方法（你稍后会编写）。向方法传递输出参数（out arguments），以便检索存储 ID 编号、名称和平均分数的变量的值。然后，依次将这三个值传递给八个 `Student` 对象中的每个构造函数。

- 调用 `Array.Sort()` 方法并将 `students` 数组传递进去。然后，在循环中，逐个对象调用你编写的 `Display()` 方法。

