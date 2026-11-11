

## **代码清单 4.1** `CalendarTest/CalendarTest.java`

```java
import java.time.*;

/**
 * @version 1.5 2015-05-08
 * @author Cay Horstmann
 */
public class CalendarTest
{
   public static void main(String[] args)
   {
      LocalDate date = LocalDate.now();
      int month = date.getMonthValue();
      int today = date.getDayOfMonth();

      date = date.minusDays(today - 1); // set to start of month
      DayOfWeek weekday = date.getDayOfWeek();
      int value = weekday.getValue(); // 1 = Monday, . . . , 7 = Sunday

      System.out.println("Mon Tue Wed Thu Fri Sat Sun");
      for (int i = 1; i < value; i++)
         System.out.print("   ");
      while (date.getMonthValue() == month)
      {
         System.out.printf("%3d", date.getDayOfMonth());
         if (date.getDayOfMonth() == today)
            System.out.print("*");
         else
            System.out.print(" ");
         date = date.plusDays(1);
         if (date.getDayOfWeek().getValue() == 1)
            System.out.println();
      }
      if (date.getDayOfWeek().getValue() != 1)
         System.out.println();
   }
}
```

### 4.3.1 Employee 类

Java 中类定义的最简单形式是

```java
class ClassName
{
  field1
  field2
  . . .
  constructor1
  constructor2
  . . .
  method1
  method2
  . . .
}
```

考虑下面这个非常简化的 Employee 类版本，企业编写工资系统时可能会用到它：

```java
class Employee
{
  // instance fields
  private String name;
  private double salary;
  private LocalDate hireDay;

  // constructor
  public Employee(String n, double s, int year, int month, int day)
  {
    name = n;
    salary = s;
    hireDay = LocalDate.of(year, month, day);
  }

  // a method
  public String getName()
  {
    return name;
  }

  // more methods
  . . .
}
```

在接下来的各节中，我们将较为详细地剖析这个类的实现。不过首先，代码清单 4.2 是一个展示 `Employee` 类实际运行的程序。

在该程序中，我们构造一个 `Employee` 数组，并用三个 `Employee` 对象填充它：

```java
Employee[] staff = new Employee[3];

staff[0] = new Employee("Carl Cracker", . . .);
staff[1] = new Employee("Harry Hacker", . . .);
staff[2] = new Employee("Tony Tester", . . .);
```

接下来，我们使用 `Employee` 类的 `raiseSalary` 方法将每位员工的薪水提高 5%：

```java
for (Employee e : staff)
    e.raiseSalary(5);
```

最后，我们通过调用 `getName`、`getSalary` 和 `getHireDay` 方法打印每位员工的信息：

```java
for (Employee e : staff)
    System.out.println("name=" + e.getName()
        + ",salary=" + e.getSalary()
        + ",hireDay=" + e.getHireDay());
```

```java
);
staff[1] = new Employee("Harry Hacker", 50000, 1989, 10,
1);
staff[2] = new Employee("Tony Tester", 40000, 1990, 3,
15);

// raise everyone's salary by 5%
for (Employee e : staff)
    e.raiseSalary(5);

// print out information about all Employee objects
for (Employee e : staff)
    System.out.println("name=" + e.getName() + ",salary="
        + e.getSalary() + ",hireDay="
        + e.getHireDay());
}

class Employee
{
    private String name;
    private double salary;
    private LocalDate hireDay;

    public Employee(String n, double s, int year, int month, int day)
    {
        name = n;
        salary = s;
        hireDay = LocalDate.of(year, month, day);
    }

    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
50    return salary;
51  }
52
53  public LocalDate getHireDay()
54  {
55      return hireDay;
56  }
57
58  public void raiseSalary(double byPercent)
59  {
60      double raise = salary * byPercent / 100;
61      salary += raise;
62  }
63 }
```

### 4.3.2 使用多个源文件

*代码清单 4.2* 中的程序在单个源文件里包含两个类。许多程序员更喜欢把每个类放到各自的源文件中。例如，你可以把 `Employee` 类放到文件 `Employee.java` 中，把 `EmployeeTest` 类放到 `EmployeeTest.java` 中。

如果你喜欢这种安排，编译程序时有两种选择。你可以使用通配符调用 Java 编译器：

```bash
javac Employee*.java
```

这样，所有匹配该通配符的源文件都会被编译成类文件。或者，你也可以直接输入

```bash
javac EmployeeTest.java
```

你可能会感到惊讶：即使从未显式编译 `Employee.java` 文件，第二种选择也能工作。然而，当 Java 编译器看到 `EmployeeTest.java` 中使用了 `Employee` 类时，它会查找名为 `Employee.class` 的文件。如果找不到该文件，它会自动搜索 `Employee.java` 并编译它。此外，如果它找到的 `Employee.java` 版本的时戳比现有 `Employee.class` 文件的时戳更新，Java 编译器会*自动*重新编译该文件。

![](img/0e7b74ef51a065c077b42cd87b362288_224_0.png)

> **注意：**
>
> 如果你熟悉 UNIX 的 make 工具（或它的某个 Windows 近亲，例如 nmake），可以把 Java 编译器看作已经内置了 make 功能。

### 4.3.3 剖析 `Employee` 类

在接下来的各节中，我们将剖析 `Employee` 类。先从该类中的方法开始。通过查看源代码可以看到，这个类有一个构造器和四个方法：

```java
public Employee(String n, double s, int year, int month, int day)
public String getName()
public double getSalary()
public LocalDate getHireDay()
public void raiseSalary(double byPercent)
```

这个类的所有方法都被标记为 public。关键字 public 表示任何类中的任何方法都可以调用该方法。（本章和下一章会介绍四种可能的访问级别。）

接下来，请注意三个实例字段，它们将保存 `Employee` 类实例内部操作的数据。

```java
private String name;
private double salary;
private LocalDate hireDay;
```

`private` 关键字确保：能够访问这些实例字段的方法*只有* `Employee` 类自身的方法。任何外部方法都不能读写这些字段。

> **注意：**
>
> 你可以对实例字段使用 `public` 关键字，但这是个非常糟糕的主意。将实例字段设为 `public` 会允许程序任何部分读取和修改这些实例字段，彻底破坏封装。任何类的任何方法都可以修改 public 字段——而且根据我们的经验，有些代码*会*在你最意想不到的时候利用这种访问权限。我强烈建议把所有实例字段都设为 `private`。

最后，请注意其中两个实例字段本身就是对象：`name` 和 `hireDay` 字段分别是对 `String` 和 `LocalDate` 对象的引用。这很常见：类经常会包含类类型的实例字段。

### 4.3.4 构造器入门

我们来看 `Employee` 类中列出的构造器。

```java
public Employee(String n, double s, int year, int month, int day)
{
    name = n;
    salary = s;
    hireDay = LocalDate.of(year, month, day);
}
```

如你所见，构造器的名称与类名相同。当你构造 `Employee` 类的对象时，这个构造器会运行——为实例字段赋予你希望它们具有的初始状态。

例如，当你用如下代码创建 `Employee` 类的实例时：

```java
new Employee("James Bond", 100000, 1950, 1, 1)
```

你就把实例字段设置如下：

```java
name = "James Bond";
salary = 100000;
hireDay = LocalDate.of(1950, 1, 1); // January 1, 1950
```

构造器与其他方法之间有一个重要区别。构造器只能与 new 运算符一起调用。你不能对已有对象应用构造器来重置实例字段。例如，

```java
james.Employee("James Bond", 250000, 1950, 1, 1) // ERROR
```

这是一个编译期错误。

本章后面还会更详细地讨论构造器。现在，请记住以下几点：

- 构造器的名称与类名相同。
- 一个类可以有多个构造器。
- 构造器可以接受零个、一个或多个参数。
- 构造器没有返回值。
- 构造器总是与 new 运算符一起调用。

![](img/0e7b74ef51a065c077b42cd87b362288_226_0.png)

### C++ 注意：

构造器在 Java 中的工作方式与 C++ 中相同。但请记住，所有 Java 对象都构造在堆上，并且一个

