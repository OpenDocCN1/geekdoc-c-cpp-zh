
```
Year = year; // could validate year
Day = day; // validates day
Console.WriteLine($"Date object constructor for date {this}");
}

// property that gets and sets the month
public int Month
{
    get
    {
        return month;
    }
    private set // make writing inaccessible outside the class
    {
        if (value <= 0 || value > 12) // validate month
        {
            throw new ArgumentOutOfRangeException(
                nameof(value), value, $"{nameof(Month)} must be 1-12");
        }

        month = value;
    }
}

// property that gets and sets the day
public int Day
{
    get
    {
        return day;
    }
    private set // make writing inaccessible outside the class
    {
        int[] daysPerMonth =
            {0, 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

        // check if day in range for month
        if (value <= 0 || value > daysPerMonth[Month])
        {
            throw new ArgumentOutOfRangeException(nameof(value), value,
                $"{nameof(Day)} out of range for current month/year");
        }
        // check for leap year
        if ((Month == 2 && value == 29 &&
            !(Year % 400 == 0 || (Year % 4 == 0 && Year % 100 != 0))))
        {
            throw new ArgumentOutOfRangeException(nameof(value), value,
                $"{nameof(Day)} out of range for current month/year");
        }

        day = value;
    }
}
```

**图 10.7** | Date 类声明。（第 2 部分，共 3 部分。）

```
// return a string of the form month/day/year
public override string ToString() => $"{Month}/{Day}/{Year}";
}
```

图 10.7 | Date 类声明。（第 3 部分，共 3 部分。）

### 构造函数

构造函数（第 13—19 行）接收三个 int。第 15 行调用属性 Month 的 set 访问器（第 28—37 行）来验证月份——如果值超出范围，该访问器将引发异常。第 16 行使用属性 Year 设置年份。由于 Year 是自动实现的属性，它不提供验证——在本示例中，我们假定 Year 的值是正确的。第 17 行使用属性 Day 的 set 访问器（第 47—67 行），根据当前 Month 和 Year（依次使用属性 Month 和 Year）获取 month 和 Year 的值，以验证并赋值 day。

初始化顺序很重要，因为属性 Day 的 set 访问器在执行验证时假定 Month 和 Year 是正确的。第 53 行根据 Month 中的天数确定 day 是否超出范围，如果是，则引发异常。第 59—60 行确定 Month 是否为二月、day 是否为 29 以及 Year 是否为非闰年（在这种情况下，29 超出范围），如果是，则引发异常。如果未引发异常，则 day 的值正确，并在第 66 行赋给实例变量。构造函数中的第 18 行将 this 引用格式化为字符串。由于 this 是对当前 Date 对象的引用，因此会隐式调用该对象的 ToString 方法（第 71 行）以获得 Date 的字符串表示形式。

### private set 访问器

Date 类使用访问修饰符确保类的客户端必须使用适当的方法和属性来访问私有数据。具体来说，属性 Year、Month 和 Day 声明了 private set 访问器（分别在第 9、28 和 47 行）——这些 set 访问器只能在类内部使用。我们将这些访问器声明为 private，理由与将实例变量声明为 private 相同——为了简化代码维护并控制对类数据的访问。尽管 Date 类中的构造函数、方法和属性仍然具有使用 set 访问器执行验证的所有优点，但类的客户端必须使用类的构造函数来初始化 Date 对象中的数据。Year、Month 和 Day 的 get 访问器隐式为 public——当 get 或 set 访问器前没有访问修饰符时，将使用属性的访问修饰符。

## 10.7.2 Employee 类

Employee 类（图 10.8）具有公共的自动实现、仅 getter 的属性 FirstName、LastName、BirthDate 和 HireDate。BirthDate 和 HireDate（第 7—8 行）引用 Date 对象，表明类可以将其他类的对象引用作为成员。当然，FirstName 和 LastName 也是如此，它们引用 String 对象。Employee 构造函数（第 11—18 行）使用其四个参数初始化类的属性。当调用 Employee 类的 ToString 方法时，它返回一个字符串，其中包含两个 Date 对象的字符串表示形式。这些字符串中的每一个都是通过对 Date 类的 ToString 方法进行隐式调用来获得的。

```csharp
// Fig. 10.8: Employee.cs
// Employee class with references to other objects.
public class Employee
{
    public string FirstName { get; }
    public string LastName { get; }
    public Date BirthDate { get; }
    public Date HireDate { get; }

    // constructor to initialize name, birth date and hire date
    public Employee(string firstName, string lastName,
        Date birthDate, Date hireDate)
    {
        FirstName = firstName;
        LastName = lastName;
        BirthDate = birthDate;
        HireDate = hireDate;
    }

    // convert Employee to string format
    public override string ToString() => $"{LastName}, {FirstName} " +
        $"Hired: {HireDate} Birthday: {BirthDate}";
}
```

图 10.8 | 引用其他对象的 Employee 类。

## 10.7.3 EmployeeTest 类

EmployeeTest 类（图 10.9）创建两个 Date 对象（第 9—10 行），分别表示 Employee 的生日和雇佣日期。第 11 行创建一个 Employee，并通过向构造函数传递两个字符串（表示 Employee 的名字和姓氏）和两个 Date 对象（表示生日和雇佣日期）来初始化其实例变量。第 13 行隐式调用 Employee 的 ToString 方法，以显示 Employee 的字符串表示形式，并证明该对象已正确初始化。

```csharp
// Fig. 10.9: EmployeeTest.cs
// Composition demonstration.
using System;

class EmployeeTest
{
    static void Main()
    {
        var birthday = new Date(7, 24, 1949);
        var hireDate = new Date(3, 12, 1988);
        var employee = new Employee("Bob", "Blue", birthday, hireDate);

        Console.WriteLine(employee);
    }
}
```

图 10.9 | 组合演示。（第 1 部分，共 2 部分。）

```
Date object constructor for date 7/24/1949
Date object constructor for date 3/12/1988
Blue, Bob Hired: 3/12/1988 Birthday: 7/24/1949
```

图 10.9 | 组合演示。（第 2 部分，共 2 部分。）

## 10.8 垃圾回收与析构函数

你创建的每个对象都会使用各种系统资源，例如内存。在许多编程语言中，这些系统资源会保留给对象使用，直到程序员显式释放它们。如果在资源被显式释放之前，对管理该资源的对象的所有引用都已丢失，则应用将无法再访问该资源来释放它。这称为资源泄漏。

为了避免资源泄漏，我们需要一种规范的方式，在不再需要资源时将其归还给系统。公共语言运行时（CLR）通过使用垃圾回收器来执行自动内存管理，垃圾回收器回收不再使用的对象所占用的内存，以便该内存可用于其他对象。当不再有对对象的引用时，该对象就有资格被销毁。每个对象都有一个称为析构函数的特殊成员，垃圾回收器会调用它，在垃圾回收器回收对象的内存之前对对象执行终止清理。析构函数的声明方式类似于无参数构造函数，不同之处在于其名称是类名，前面带有波浪号（~），并且其头部没有访问修饰符。垃圾回收器调用对象的析构函数后，该对象就有资格进行垃圾回收。此类对象的内存可由垃圾回收器回收。

内存泄漏在 C 和 C++ 等其他语言中很常见（因为这些语言不会自动回收内存），在 C# 中则不太可能发生，但仍可能以微妙的方式发生。还可能发生其他类型的资源泄漏。例如，应用可以打开磁盘上的文件以修改其内容。如果应用不关闭该文件，则在打开它的应用终止之前，其他应用都无法修改（甚至可能无法使用）该文件。

垃圾回收器的一个问题是，它不保证在指定时间执行其任务。因此，垃圾回收器可以在对象有资格被销毁后的任何时间调用析构函数，并且可以在析构函数执行后的任何时间回收内存。事实上，在应用终止之前，这两件事都可能不会发生。因此，无法确定析构函数是否会被调用或何时被调用。因此，析构函数很少使用。

> 软件工程观察 10.9
> 
> 使用资源（如磁盘上的文件）的类应提供一个最终释放资源的方法。许多框架类库（Framework Class Library）类为此提供了 Close 或 Dispose 方法。第 13.6 节介绍 IDisposable 方法，随后许多后续示例都会使用它。Close 方法通常与文件（第 17 章）和其他所谓的数据流类型的对象一起使用。

## 10.9 static 类成员

每个对象都有自己的类实例变量副本。在某些情况下，一个特定变量只应有一份副本，由类的所有对象共享。静态变量（或属性——
