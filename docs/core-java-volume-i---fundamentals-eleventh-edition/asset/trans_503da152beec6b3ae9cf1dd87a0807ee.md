
`Employee` 类是超类，但这并不是因为它比其子类更高级或包含更多功能。事实上，*情况恰恰相反*：子类比其超类具有*更多*功能。例如，当我们查看 `Manager` 类的其余代码时你会看到，`Manager` 类比其超类 `Employee` 封装了更多数据，也具有更多功能。

> **注意：** *超*（super）和*子*（sub）这两个前缀来自理论计算机科学和数学中使用的集合语言。所有员工的集合包含所有经理的集合，因此前者被称为经理集合的*超集*。或者换句话说，所有经理的集合是所有员工集合的*子集*。

我们的 `Manager` 类有一个用于存储奖金的新字段，以及一个用于设置该字段的新方法：

```java
public class Manager extends Employee
{
   private double bonus;
   . . .
   public void setBonus(double bonus)
   {
      this.bonus = bonus;
   }
}
```

这些方法和字段并没有什么特别之处。如果你有一个 `Manager` 对象，只需调用 `setBonus` 方法即可。

```java
Manager boss = . . .;
boss.setBonus(5000);
```

当然，如果你有一个 `Employee` 对象，就不能调用 `setBonus` 方法——它不在 `Employee` 类定义的方法之中。

不过，你*可以*对 `Manager` 对象使用 `getName` 和 `getHireDay` 等方法。尽管这些方法没有在 `Manager` 类中显式定义，但它们会自动从 `Employee` 超类继承。

同样，字段 `name`、`salary` 和 `hireDay` 来自超类。每个 `Manager` 对象都有四个字段：`name`、`salary`、`hireDay` 和 `bonus`。

通过扩展超类来定义子类时，你只需指出子类与超类之间的*差异*。设计类时，应将最通用的方法放在超类中，将更专门化的方法放在其子类中。将公共功能提取出来并移到超类，是面向对象编程中的常规做法。

### 5.1.2 重写方法

超类的某些方法并不适合 Manager 子类。特别是，getSalary 方法应返回基本工资与奖金之和。你需要提供一个新方法来*重写*超类方法：

```java
public class Manager extends Employee
{
    . . .
    public double getSalary()
    {
        . . .
    }
    . . .
}
```

如何实现这个方法？乍看之下似乎很简单——只需返回 salary 和 bonus 字段之和：

```java
public double getSalary()
{
    return salary + bonus; // won't work
}
```

然而，这样做行不通。回想一下，只有 Employee 的方法才能直接访问 Employee 类的私有字段。这意味着 Manager 类的 getSalary 方法不能直接访问 salary 字段。如果 Manager 的方法想要访问这些私有字段，就必须像其他所有方法一样——使用公共接口，在这里就是 Employee 类的公共 getSalary 方法。

那么，我们再试一次。你需要调用 getSalary，而不是直接访问 salary 字段：

```java
public double getSalary()
{
    double baseSalary = getSalary(); // still won't work
    return baseSalary + bonus;
}
```

现在的问题在于，对 getSalary 的调用只是调用了*它自身*，因为 Manager 类有一个 getSalary 方法（也就是我们正试图实现的方法）。其后果是对同一方法的无限调用链，最终导致程序崩溃。

我们需要表明，我们要调用的是 Employee 超类的 getSalary 方法，而不是当前类的方法。为此，你要使用特殊关键字 *super*。调用 `super.getSalary()` 会调用 Employee 类的 getSalary 方法。下面是 Manager 类中 getSalary 方法的正确版本：

```java
public double getSalary()
{
   double baseSalary = super.getSalary();
   return baseSalary + bonus;
}
```

> **注意：** 有些人认为 *super* 类似于 *this* 引用。然而，这种类比并不十分准确：*super* 并不是对对象的引用。例如，你不能将值 *super* 赋给另一个对象变量。相反，*super* 是一个特殊关键字，指示编译器调用超类方法。

如你所见，子类可以*添加*字段，也可以*添加*方法或*重写*超类的方法。然而，继承永远不能移除任何字段或方法。

> **C++ 注意：** Java 使用关键字 *super* 来调用超类方法。在 C++ 中，则应改用超类名称配合 `::` 运算符。例如，`Manager` 类的 `getSalary` 方法会调用 `Employee::getSalary`，而不是 `super.getSalary()`。

### 5.1.3 子类构造器

为完成我们的示例，下面提供一个构造器。

```java
public Manager(String name, double salary, int year, int month, int day)
{
   super(name, salary, year, month, day);
   bonus = 0;
}
```

在这里，关键字 *super* 的含义有所不同。指令

```java
super(name, salary, year, month, day);
```

是“以 name、salary、year、month 和 day 为参数调用 Employee 超类的构造器”的简写。

由于 Manager 构造器不能访问 Employee 类的私有字段，所以必须通过构造器来初始化它们。该构造器使用特殊的 super 语法调用。使用 `super` 的调用必须是子类构造器中的第一条语句。

如果子类构造器没有显式调用超类构造器，就会调用超类的无参构造器。如果超类没有无参构造器，而子类构造器又没有显式调用另一个超类构造器，Java 编译器就会报错。

> **注意：** 回想一下，`this` 关键字有两种含义：表示对隐式参数的引用，以及调用同一个类的另一个构造器。同样，`super` 关键字也有两种含义：调用超类方法和调用超类构造器。当用于调用构造器时，`this` 和 `super` 关键字密切相关。构造器调用只能作为另一个构造器中的第一条语句出现。构造器参数要么传给同一个类的另一个构造器（`this`），要么传给超类的构造器（`super`）。

> **C++ 注意：** 在 C++ 构造器中，不调用 `super`，而是使用初始化列表语法来构造超类。Manager 构造器在 C++ 中看起来会像这样：

```cpp
// C++
Manager::Manager(String name, double salary, int year, int month, int day)
  : Employee(name, salary, year, month, day)
{
    bonus = 0;
}
```

在为 Manager 对象重新定义 `getSalary` 方法后，经理的工资将*自动*加上奖金。

下面是一个实际运行的例子。我们创建一个新经理并设置该经理的奖金：

```java
Manager boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
boss.setBonus(5000);
```

我们创建一个包含三名员工的数组：

```java
var staff = new Employee[3];
```

我们用经理和员工的混合来填充该数组：

```java
staff[0] = boss;
staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);
```

我们打印每个人的工资：

```java
for (Employee e : staff)
    System.out.println(e.getName() + " " + e.getSalary());
```

这个循环会打印以下数据：

```
Carl Cracker 85000.0
Harry Hacker 50000.0
Tony Tester 40000.0
```

现在，staff[1] 和 staff[2] 各自打印其基本工资，因为它们是 Employee 对象。然而，staff[0] 是一个 Manager 对象，其 getSalary 方法会将奖金加到基本工资上。

值得注意的是，调用 `e.getSalary()` 会选出正确的 *getSalary* 方法。注意，e 的*声明*类型是 Employee，但 e 所引用对象的*实际*类型可以是 Employee 或 Manager。

当 e 引用一个 Employee 对象时，调用 e.getSalary() 会调用 Employee 类的 getSalary 方法。然而，当 e 引用一个 Manager 对象时，则会调用 Manager 类的 getSalary 方法。虚拟机知道 e 所引用对象的实际类型，因此能够调用正确的方法。

对象变量（例如变量 e）可以引用多种实际类型，这一事实称为*多态*。在运行时自动选择合适的方法称为*动态绑定*。本章将更详细地讨论这两个主题。

![](img/127bccebb2cfadea3f02579edaad63c3_239_0.png)

> **C++ 注意：** 在 C++ 中，如果要实现动态绑定，需要将成员函数声明为 virtual。在 Java 中，动态绑定是默认行为；如果你*不*希望某个方法是虚方法，就将其标记为 final。（本章后面会讨论 final 关键字。）

清单 5.1 包含一个程序，展示 Employee（清单 5.2）和 Manager（清单 5.3）对象的工资计算有何不同。
