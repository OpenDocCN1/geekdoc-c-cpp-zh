
# 使用类和对象

## 非默认构造函数

如果你想使用非默认构造函数，必须提供相应的参数。例如，如果 `Employee` 类包含一个带有 `int` 参数的构造函数，你可以编写以下代码来填充七个数组元素中的三个：

```cs
Employee[] empArray = {new Employee(123),
new Employee(234), new Employee(345)};
```

通过使用属于数组中对象的方法，你可以在数组名之后、点操作符和方法之前插入适当下标符号。例如，要将所有七个 `Employee` 的 `IdNumber` 属性设置为 999，你可以编写以下代码：

```c
for(int x = 0; x < empArray.Length; ++x)
    empArray[x].IdNumber = 999;
```

## 在对象数组中使用 Sort() 和 BinarySearch() 方法

在“使用数组”章节中，你学习了如何使用 `System.Array` 类以及对 `int`、`double` 和 `string` 等简单数据类型使用 `Sort()` 方法。`Sort()` 方法接受一个数组参数，并按升序/降序排列其元素。`BinarySearch()` 方法接受一个已排序的数组和一个它尝试在数组中匹配的值。

当你搜索或排序你创建的对象数组时，会产生比较问题。当你创建并排序简单数据项数组时，只需要考虑一种类型的值，且顺序基于每个项目的 Unicode 值。支持简单数据项的类都包含一个名为 `CompareTo()` 的方法，该方法提供了基本数据类型之间如何比较的细节。换句话说，它们定义了如“2 大于 1”和“B 大于 A”之类的比较。`Sort()` 和 `BinarySearch()` 使用当前排序数据类型的 `CompareTo` 方法。换言，`Sort()` 在排序整数时使用 `Int32` 版本的 `CompareTo()`，在排序字符时使用 `Char` 版本的 `CompareTo()`。

你在第 2 章学习了内置数据类的名称；它们总结在表 2-1 中。

你整本书都一直在使用 `String` 类（及其字符串别名）。该类也包含一个 `CompareTo()` 方法，你在第 2 章中首次使用了它。

当你创建一个要在对象之间进行比较的类时，必须告诉编译器在进行这些比较时使用哪个字段。例如，在逻辑上，你可能根据 ID 号、工资、部门编号、姓氏、入职日期或类中包含的任何字段对组织的员工排序。为了告诉 C# 使用哪个字段来排列 `Employee` 对象，你必须创建一个接口。

抽象方法没有方法体；接口包含抽象方法。在下一章中，你将学习更多关于抽象方法的知识。现在，请理解接口不是数据类型，而是一组空的、抽象的方法（以及可能的其他成员）的集合，只要类提供了覆盖接口的“无操作”方法定义，就可以被任何类使用。与类不同，接口不能包含实例字段，你无法从它创建对象。

实现接口的类必须重写接口的方法。当方法被重写时，它的优先级高于原方法，并被用来替代原始版本。换句话说，接口中的方法是空的，任何使用这些方法的类必须包含一个提供细节并被替代的新版本。接口定义了类必须实现的命名行为，以便所有类使用相同的方法名，但根据类的情况恰当地使用它们。通过这种方式，接口实现了多态——不同对象使用相同方法名但根据上下文采取相应的能力。

> 当方法被重写时，它的签名与被重写的方法签名相同。当方法被重载时，它们具有不同的签名。你将在下一章学习更多关于重写方法以及抽象方法和类。

C# 支持许多接口。你可以通过首字母 `I` 来识别接口。例如，C# 包含一个 `IComparable` 接口，它包含了 `CompareTo()` 方法的定义，该方法比较一个对象与另一个对象并返回一个整数。图 9-39 显示了 `IComparable` 的定义。`CompareTo()` 方法接受一个参数 `Object` 但不包含任何语句；如果你想让对象是可比较的，必须在你创建的类中为此方法提供实现。也就是说，`CompareTo()` 方法是抽象的，你必须为该类确定大于、小于和等于的含义。

```c
interface IComparable {
    int CompareTo(Object o);
}
```

**图 9-39 IComparable 接口**

当你创建一个实例将被你使用的的类时：

- 你必须在类名后包含单个冒号和接口名称 `IComparable`。
- 你必须编写一个包含以下头部的方法：

```c
int IComparable.CompareTo(Object o)
```

> 当方法被重写时，它的签名与被重写的方法签名相同。当方法被重载时，它们具有不同的签名。你将在下一章学习更多关于重写方法以及抽象方法和类。

（注：提供的 OCR 文本在后几页关于 `IComparable` 接口的内容存在大量重复/交错片段。我已根据提供的技术内容清理了逻辑流。）

为了使 `BinarySearch` 和 `Sort()` 等方法正常工作，你为每个类创建的 `CompareTo` 方法必须返回一个整数。表 9-2 显示了返回值。

| 返回值 | 含义 |
|---|---|
| 负数 | 此实例小于所比较的对象。 |
| 零 | 此实例与所比较的对象相等。 |
| 正数 | 此实例大于所比较的对象。 |

**表 9-2 CompareTo() 的返回值**

图 9-40 中的 `Employee` 类在其头部使用了冒号和 `IComparable` 来指示接口。阴影方法是一个实例方法；也就是说，它“属于” `Employee`。

```csharp
class Employee : IComparable {
    public int idNumber {get; set;}
    public double Salary {get; set;}
    int CompareTo(Object o) {
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

**图 9-40 使用接口 Employee 类**

## 第 9 章 使用类和对象

```text
C:\CF\Chapter.07>ComparableEmployeeArray
Sorted employees:
Employee #0: 111 $0.00
Employee #1: 222 $0.00
Employee #2: 333 $0.00
Employee #3: 444 $0.00
Employee #4: 555 $0.00
Employee #222 found at position 1
C:\CF\Chapter.07>
```

**图 9-42 ComparableEmployeeArray 程序的输出**

请注意，`seekEmp` 对象仅根据 `idNumber` 匹配数组第二个位置的 `Employee`——而不是根据 `salary`——这是因为 `Employee` 类中的 `CompareTo()` 方法仅使用 `idNumber` 值而未使用薪水进行比较。你可以编写代码，要求 `idNumber` 和 `salary` 值都必须匹配后才返回正数。

## 两个真理一个谎言

### 声明对象数组

假设一个运行程序包含以下数组声明：

`BankAccount[] acctArray = new BankAccount[500];`

- 1. 该语句为 `BankAccount` 对象留出了足够的计算机内存。
- 2. 该语句构造了 500 个 `BankAccount` 对象。
- 3. `acctArray` 的有效下标是 0 到 499。

> 虚假的陈述是 #2。该语句为 500 个 `BankAccount` 对象留出了空间，但并没有实际构造这些对象；要这样做，你必须调用构造函数。

## 你来做

### 创建对象数组

在接下来的步骤中，你创建一个 `Student` 对象数组。你提示用户输入数据以填充数组，并在显示所有数据之前根据学生 ID 对数组进行排序。

1. 打开 `CreateStudents2` 程序并立即另存为 `CreateStudents3`。将类名改为 `CreateStudents`。
2. 删除 `Main()` 方法中的所有现有语句，保留起始和结束括号。在大括号之间，声明一个包含八个 `Student` 对象的数组。还要声明一个变量作为数组下标，并声明三个在构造 `Student` 对象之前用于临时存储用户输入数据的变量。

```csharp
Student[] students = new Student[8];
int x;
int id;
string name;
double gpa;
```

3. 在循环中，调用 `GetData()` 方法（你稍后会编写）。向该方法发送输出参数，以便你可以获取用于存储 ID 号、名称和平均学点的变量的值。然后，将这三个值依次发送给八个 `Student` 对象的构造函数。

```csharp
for(x = 0; x < students.Length; ++x)
{
    GetData(out id, out name, out gpa);
    students[x] = new Student(id, name, gpa);
}
```

4. 调用 `Array.Sort()` 方法并传递学生数组。然后在循环中逐个对对象调用你在上一步步骤中编写的 `Display()` 方法。

```csharp
Array.Sort(students);
WriteLine("Sorted List:");
for(x = 0; x < students.Length; ++x)
    Display(students[x]);
```

5. 编写 `GetData()` 方法。它的参数是 `out` 参数，以便其值对调用方法可见。该方法简单地提示用户输入每个数据项，读取它，并在必要时转换为相应的类型。

```csharp
static void GetData(out int id, out string name, out double gpa)
{
    string inString;
    Write("Please enter student ID number >> ");
    inString = ReadLine();
    int.TryParse(inString, out id);
    Write("Please enter last name for student {0} >> ");
    name = ReadLine();
    Write("Please enter grade point average >> ");
    inString = ReadLine();
    double.TryParse(inString, out gpa);
}
```

6. 在 `Student` 类的头部之后，添加 `IComparable`，以便类的对象可以排序：

```csharp
class Student : IComparable
```

7. 在 `Student` 类的结束括号之前，添加 `IComparable.CompareTo()` 方法，该方法的用于类的对象排序。该方法将根据 ID 号对 `Student` 对象进行排序，因此根据 `IdNumber` 属性的比较返回 1、-1 或 0。该方法接受一个转换为 `Student` 对象的对象。如果控制 `Student` 对象的 `IdNumber` 大于参数的 `IdNumber`，则返回值为 1。如果控制 `Student` 对象的 `IdNumber` 小于参数的 `IdNumber`，则返回值为 -1。否则，返回值为 0。

```csharp
int CompareTo(Object o)
{
    int returnValue;
    Student temp = (Student)o;
    if(this.IdNumber > temp.IdNumber)
        returnValue = 1;
    else
        if(this.IdNumber < temp.IdNumber)
            returnValue = -1;
        else
            returnValue = 0;
    return returnValue;
}
```

8. 保存文件，然后编译并执行。在提示时，输入你选择的学生 ID、名称和平均学点。对象将按照 `IdNumber` 顺序排序并显示。图 9-43 显示了一个典型的执行过程。

```text
C:\C\Chapter.09>CreateStudents
Please enter student ID number >> 912
Please enter last name for student ID >> Harris
Please enter grade point average >> 3.4
Please enter student ID number >> 634
Please enter last name for student ID >> Lewis
Please enter grade point average >> 3.2
Please enter student ID number >> 610
Please enter last name for student ID >> Johnson
Please enter grade point average >> 2.6
Please enter student ID number >> 377
Please enter last name for student ID >> Lee
Please enter grade point average >> 4.0
Please enter student ID number >> 391
Please enter last name for student ID >> Young
Please enter grade point average >> 3.9
Please enter student ID number >> 215
Please enter last name for student ID >> Jenks
Please enter grade point average >> 3.8
Please enter student ID number >> 185
Please enter last name for student ID >> Bower
Please enter grade point average >> 2.3
Please enter student ID number >> 478
Please enter last name for student ID >> Cooper
Please enter grade point average >> 2.6
Sorted List:
Employee #0: 185 $2.3
Employee #1: 215 $3.8
Employee #2: 377 $4.0
Employee #3: 391 $3.9
Employee #4: 478 $2.6
Employee #5: 610 $2.6
Employee #6: 634 $3.2
Employee #7: 912 $3.4
```

**图 9-43 典型执行输出**

## 理解 GUI 应用程序对象

图 9-47 显示了一个新的 GUI 应用程序，程序员仅通过将一个按钮（Button）拖到表单（Form）上就开始创建它。

![](img/b0a31988f44670d0728c4f372d8dab77_433_0.png)

**图 9-47 表单上的按钮**

如果你在解决方案管理器中点击 `Form1.Designer.cs` 并向下滚动，就可以显示声明按钮的代码。请见图 9-48。

![](img/b0a31988f44670d0728c4f372d8dab77_434_0.png)

**图 9-48 自动生成的声明 button1 的语句**

如果你在代码中右键点击 `button1` 并在弹出的菜单中选择“查找所有引用”，IDE 底部的“查找符号结果”区域将显示项目里对 `button1` 的每个引用。（你可能需要调整窗口大小以清晰地查看引用。）你可以双击列表中的每个项目，以定位到为 `button1` 生成代码的所有位置。例如，图 9-49 所示，`button1` 的多个实例位于名为 `InitializeComponent()` 的方法中。第一个引用还可以查看按钮的名称（Name）、位置（Location）、大小（Size）和其他属性是如何设置的。你可以自己编写这些语句，特别是现在你已经对对象及其构造方式有了更多了解，但通过将按钮拖到表单并让 IDE 为你创建这些语句来视觉化开发应用程序要简单得多。

![](img/b0a31988f44670d0728c4f372d8dab77_435_0.png)

**图 9-49 IDE 中一些自动生成的 button1 引用**

在图 9-49 中，每个 `button1` 出现位置之前的此引用指向包含这些语句的类（`Form1`）。

现在你已经理解了如何在自己的类中创建属性，你就可以理解 GUI 对象的属性以及它们是如何为你创建的了。

## 本章总结

- 应用程序类包含一个 `Main()` 方法。你也可以从类中实例化对象；这些类不需要有 `Main()` 方法。类的数据组件是它的实例变量（或字段）和方法。实例化另一个预写类对象的程序或类称为客户端类或类用户。
