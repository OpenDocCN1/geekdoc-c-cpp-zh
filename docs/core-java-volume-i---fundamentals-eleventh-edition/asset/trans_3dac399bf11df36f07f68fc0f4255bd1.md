
![](img/127bccebb2cfadea3f02579edaad63c3_192_0.png)

**图 4.7** 修改对象参数具有持久效果。

让我们尝试编写一个交换两个 Employee 对象的方法：

```java
public static void swap(Employee x, Employee y) // doesn't work
{
    Employee temp = x;
    x = y;
    y = temp;
}
```

如果 Java 对对象使用按引用调用，这个方法就会奏效：

```java
var a = new Employee("Alice", . . .);
var b = new Employee("Bob", . . .);
swap(a, b);
// does a now refer to Bob, b to Alice?
```

然而，该方法实际上并不会改变存储在变量 a 和 b 中的对象引用。swap 方法的 x 和 y 参数是用这些引用的副本初始化的。然后该方法继续交换这些副本。

```java
// x refers to Alice, y to Bob
Employee temp = x;
x = y;
y = temp;
// now x refers to Bob, y to Alice
```

但最终，这只是徒劳。方法结束时，参数变量 x 和 y 被丢弃。原始变量 a 和 b 仍然引用与方法调用之前相同的对象（见图 4.8）。

![](img/127bccebb2cfadea3f02579edaad63c3_193_0.png)

**图 4.8** 交换对象参数没有持久效果。

这表明 Java 编程语言并不对对象使用按引用调用。相反，*对象引用是按值传递的*。

下面总结在 Java 中可以用方法参数做什么、不能做什么：

- 方法不能修改基本类型（即数字或布尔值）的参数。
- 方法可以改变对象参数的*状态*。
- 方法不能使对象参数引用一个新对象。

清单 4.4 中的程序演示了这些事实。该程序首先尝试将一个数字参数的值变为三倍，但没有成功：

```text
Testing tripleValue:
Before: percent=10.0
End of method: x=30.0
After: percent=10.0
```

然后它成功地将一名员工的薪水变为三倍：

```text
Testing tripleSalary:
Before: salary=50000.0
End of method: salary=150000.0
After: salary=150000.0
```

方法执行后，harry 所引用对象的状态已经改变。这是可能的，因为该方法通过对象引用的副本修改了状态。

最后，程序演示了 swap 方法的失败：

```text
Testing swap:
Before: a=Alice
Before: b=Bob
End of method: x=Bob
End of method: y=Alice
After: a=Alice
After: b=Bob
```

如你所见，参数变量 x 和 y 被交换了，但变量 a 和 b 未受影响。

> **C++ 注：** C++ 既有按值调用，也有按引用调用。你用 `&` 标记引用参数。例如，你可以轻松实现方法 `void tripleValue(double& x)` 或 `void swap(Employee& x, Employee& y)`，这些方法会修改其引用参数。

### 清单 4.4 ParamTest/ParamTest.java

```java
/**
 * This program demonstrates parameter passing in Java.
 * @version 1.01 2018-04-10
 * @author Cay Horstmann
 */
public class ParamTest
{
    public static void main(String[] args)
    {
        /*
         * Test 1: Methods can't modify numeric parameters
         */
        System.out.println("Testing tripleValue:");
        double percent = 10;
        System.out.println("Before: percent=" + percent);
        tripleValue(percent);
        System.out.println("After: percent=" + percent);

        /*
         * Test 2: Methods can change the state of object parameters
         */
        System.out.println("\nTesting tripleSalary:");
        var harry = new Employee("Harry", 50000);
        System.out.println("Before: salary=" + harry.getSalary());
        tripleSalary(harry);
        System.out.println("After: salary=" + harry.getSalary());

        /*
         * Test 3: Methods can't attach new objects to object parameters
         */
        System.out.println("\nTesting swap:");
        var a = new Employee("Alice", 70000);
        var b = new Employee("Bob", 60000);
        System.out.println("Before: a=" + a.getName());
        System.out.println("Before: b=" + b.getName());
        swap(a, b);
        System.out.println("After: a=" + a.getName());
        System.out.println("After: b=" + b.getName());
    }

    public static void tripleValue(double x) // doesn't work
    {
        x = 3 * x;
        System.out.println("End of method: x=" + x);
    }

    public static void tripleSalary(Employee x) // works
    {
        x.raiseSalary(200);
        System.out.println("End of method: salary=" + x.getSalary());
    }

    public static void swap(Employee x, Employee y)
    {
        Employee temp = x;
        x = y;
        y = temp;
        System.out.println("End of method: x=" + x.getName());
        System.out.println("End of method: y=" + y.getName());
    }
}

class Employee // simplified Employee class
{
    private String name;
    private double salary;

    public Employee(String n, double s)
    {
        name = n;
        salary = s;
    }

    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
        return salary;
    }

    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }
}
```

## 4.6 对象构造

你已经看到如何编写简单的构造器来定义对象的初始状态。然而，由于对象构造如此重要，Java 提供了相当多样的机制来编写构造器。我们将在接下来的各节中逐一介绍这些机制。

### 4.6.1 重载

有些类有不止一个构造器。例如，你可以像这样构造一个空的 `StringBuilder` 对象：

```java
var messages = new StringBuilder();
```

或者，你可以指定一个初始字符串：

```java
var todoList = new StringBuilder("To do:\n");
```

这种能力称为*重载*。如果若干方法具有相同的名称（在这里是 `StringBuilder` 的构造器方法）但参数不同，就会发生重载。编译器必须分辨出要调用哪个方法。它

### 4.6.3 无参数构造器

许多类包含一个无参数构造器，用于创建一个状态被设置为适当默认值的对象。例如，下面是 Employee 类的无参数构造器：

```java
public Employee()
{
    name = "";
    salary = 0;
    hireDay = LocalDate.now();
}
```

如果你编写一个完全没有构造器的类，那么系统会为你提供一个无参数构造器。这个构造器会将*所有*实例字段设置为默认值。因此，实例字段中包含的所有数值数据都会是 0，所有 `boolean` 值都会是 false，所有对象变量都会是 null。

如果一个类至少提供了一个构造器，但没有提供无参数构造器，那么在不提供参数的情况下构造对象是非法的。例如，清单 4.2 中最初的 Employee 类只提供了一个构造器：

```java
public Employee(String n, double s, int year, int month, int day)
```

对于那个类，构造默认员工对象是不合法的。也就是说，调用

```java
e = new Employee();
```

会是一个错误。

> **注意：** 请记住，*只有*当你的类没有其他构造器时，你才会免费获得一个无参数构造器。如果你为自己的类编写了哪怕一个构造器，并且你希望类的用户能够通过调用
>
>     new ClassName()
>
> 来创建实例，那么你必须提供一个无参数构造器。当然，如果你对所有字段的默认值感到满意，你可以简单地提供
>
>     public ClassName()
>     {
>     }

**C++ 注：** C++ 使用“初始化列表”语法来构造字段：

```cpp
Employee::Employee(String n, double s, int y, int m, int d) // C++
: name(n),
  salary(s),
  hireDay(y, m, d)
{
}
```

C++ 使用这种特殊语法来避免不必要地调用无参数构造器。在 Java 中，没有必要这样做，因为对象没有子对象，只有指向其他对象的指针。

### 4.6.4 显式字段初始化

通过重载类中的构造器方法，你可以构建许多方式来设置类实例字段的初始状态。确保无论调用哪个构造器，每个实例字段都被设置为有意义的值，这始终是个好主意。

你可以直接在类定义中为任何字段赋值。例如：

```java
class Employee
{
   private String name = "";
   . . .
}
```

这个赋值在构造器执行之前完成。如果一个类的所有构造器都需要将某个特定实例字段设置为相同的值，这种语法特别有用。

初始化值不必是常量值。下面是一个用方法调用初始化字段的例子。考虑一个 Employee 类，其中每个员工都有一个 id 字段。你可以按如下方式初始化它：

```java
class Employee
{
   private static int nextId;
   private int id = assignId();

   private static int assignId()
   {
      int r = nextId;
      nextId++;
      return r;
   }
   . . .
}
```
