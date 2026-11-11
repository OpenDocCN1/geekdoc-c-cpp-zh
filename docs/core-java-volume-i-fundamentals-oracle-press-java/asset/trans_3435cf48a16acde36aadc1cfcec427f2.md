
像 `Comparable` 这样的接口，其通常用途是确保某个类实现特定的一个方法或一组方法。标记接口没有任何方法；其唯一用途是允许在类型查询中使用 `instanceof`：

```java
if (obj instanceof Cloneable) . . .
```

我建议你不要在自己的程序中使用标记接口。

即使 `clone` 的默认（浅拷贝）实现已经足够，你仍然需要实现 `Cloneable` 接口，将 `clone` 重新定义为 public，并调用 `super.clone()`。下面是一个示例：

```java
class Employee implements Cloneable
{
    // public access, change return type
    public Employee clone() throws CloneNotSupportedException
    {
        return (Employee) super.clone();
    }
    . . .
}
```

> **注意：**
>
> 直到 Java 1.4，`clone` 方法的返回类型一直是 `Object`。如今，你可以为自己的 `clone` 方法指定正确的返回类型。这是协变返回类型的一个例子（参见第 5 章）。

你刚才看到的 `clone` 方法并未给 `Object.clone` 提供的浅拷贝增加任何功能。它只是将该方法变为 public。要制作深拷贝，你必须付出更多努力，并克隆可变的实例字段。

下面是一个创建深拷贝的 `clone` 方法示例：

```java
class Employee implements Cloneable
{
    . . .
    public Employee clone() throws CloneNotSupportedException
    {
        // call Object.clone()
        Employee cloned = (Employee) super.clone();
        // clone mutable fields
        cloned.hireDay = (Date) hireDay.clone();
        return cloned;
    }
}
```

`Object` 类的 `clone` 方法会抛出 `CloneNotSupportedException`——只要对一个其类未实现 `Cloneable` 接口的对象调用 `clone`，它就会这样做。当然，`Employee` 和 `Date` 类都实现了 `Cloneable` 接口，因此不会抛出该异常。然而，编译器并不知道这一点。因此，我们声明了该异常：

```java
public Employee clone() throws CloneNotSupportedException
```

> **注意：**
>
> 改为捕获该异常会不会更好？（有关捕获异常的详细信息，请参见[第 7 章](#)。）

```java
public Employee clone()
{
    try
    {
        Employee cloned = (Employee) super.clone();
        . . .
    }
    catch (CloneNotSupportedException e) { return null; }
    // this won't happen, since we are Cloneable
}
```

这对 final 类来说是合适的。否则，最好保留 `throws` 说明符。这样，如果子类无法支持克隆，它们就可以选择抛出 `CloneNotSupportedException`。

你必须小心子类的克隆。例如，一旦你为 `Employee` 类定义了 `clone` 方法，任何人都可以用它来克隆 `Manager` 对象。`Employee` 的 clone 方法能完成这项工作吗？这取决于 `Manager` 类的字段。在我们的例子中，没有问题，因为 `bonus` 字段是基本类型。但 `Manager` 可能已经获得了需要深拷贝或不可克隆的字段。无法保证子类的实现者已经修正 `clone` 以做出正确行为。因此，`clone` 方法在 `Object` 类中声明为 `protected`。但是，如果你希望自己类的用户调用 `clone`，就不能再享受这种便利。

你应该在自己的类中实现 `clone` 吗？如果你的客户端需要制作深拷贝，那么你大概应该实现。有些作者认为，你应当完全避免 `clone`，而是为实现同一目的实现另一个方法。我同意 `clone` 相当别扭，但如果你把责任转移到另一个方法上，也会遇到同样的问题。无论如何，克隆并没有你想象的那么常见。标准库中不到 5% 的类实现了 `clone`。

清单 6.4 中的程序克隆了一个 `Employee` 类的实例（清单 6.5），然后调用了两个修改器。`raiseSalary` 方法改变 `salary` 字段的值，而 `setHireDay` 方法改变 `hireDay` 字段的状态。两次修改都不会影响原始对象，因为 `clone` 已被定义为制作深拷贝。

> **注意：**
>
> 所有数组类型都有一个 `clone` 方法，它是 public 的，而不是 protected 的。你可以用它创建一个包含所有元素副本的新数组。例如：

```java
int[] luckyNumbers = { 2, 3, 5, 7, 11, 13 };
int[] cloned = luckyNumbers.clone();
cloned[5] = 12; // doesn't change luckyNumbers[5]
```

> **注意：**
>
> 第 II 卷第 2 章展示了另一种克隆对象的机制，使用 Java 的对象序列化特性。该机制易于实现且安全，但效率不是很高。

**清单 6.4 `clone/CloneTest.java`**

```java
package clone;

/**
 * This program demonstrates cloning.
 * @version 1.11 2018-03-16
 * @author Cay Horstmann
 */
public class CloneTest
{
    public static void main(String[] args) throws CloneNotSupportedException
    {
        var original = new Employee("John Q. Public", 50000);
        original.setHireDay(2000, 1, 1);
        Employee copy = original.clone();
        copy.raiseSalary(10);
        copy.setHireDay(2002, 12, 31);
        System.out.println("original=" + original);
        System.out.println("copy=" + copy);
    }
}
```

**清单 6.5 `clone/Employee.java`**

```java
package clone;

import java.util.Date;
import java.util.GregorianCalendar;

public class Employee implements Cloneable
{
    private String name;
    private double salary;
    private Date hireDay;

    public Employee(String name, double salary)
    {
        this.name = name;
        this.salary = salary;
        hireDay = new Date();
    }

    public Employee clone() throws CloneNotSupportedException
    {
        // call Object.clone()
        Employee cloned = (Employee) super.clone();

        // clone mutable fields
        cloned.hireDay = (Date) hireDay.clone();

        return cloned;
    }

    /**
     * Set the hire day to a given date.
     * @param year the year of the hire day
     * @param month the month of the hire day
     * @param day the day of the hire day
     */
    public void setHireDay(int year, int month, int day)
    {
        Date newHireDay = new GregorianCalendar(year, month - 1, day).getTime();

        // example of instance field mutation
        hireDay.setTime(newHireDay.getTime());
    }

    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }

    public String toString()
    {
        return "Employee{name=" + name + ",salary=" + salary +
                ",hireDay=" + hireDay + "}";
    }
}
```

## 6.2 Lambda 表达式

在接下来的几节中，你将学习如何使用 lambda 表达式以简洁的语法定义代码块，以及如何编写使用 lambda 表达式的代码。

### 6.2.1 为什么使用 Lambda？

Lambda 表达式是一段可以传递的代码块，以便稍后执行一次或多次。在深入语法（或

比较元素，而该代码被集成到排序逻辑的其余部分，你可能并不想重新实现这部分逻辑。

这两个例子有共同之处。一个代码块被传递给某个对象——一个定时器或一个排序方法。该代码块在稍后的某个时间被调用。

到目前为止，在 Java 中把代码块交给别人并不容易。你不能直接传递代码块。Java 是面向对象的语言，因此你必须构造一个对象，它属于某个类，而这个类有一个包含所需代码的方法。

在其他语言中，可以直接处理代码块。Java 设计者长期以来一直抵制添加此特性。毕竟，Java 的一大优势就是其简单性和一致性。如果一门语言包含每一个只能略微提高代码简洁性的特性，它就可能变得难以维护。然而，在其他那些语言中，不仅启动线程或注册按钮单击处理程序更容易；它们的大量 API 也更简单、更一致、更强大。在 Java 中，本可以编写类似的 API，接收实现了特定接口的类的对象，但这样的 API 用起来会很不愉快。

有一段时间，问题不是是否要为函数式编程增强 Java，而是如何增强。经过数年的实验，才出现了一种适合 Java 的设计。在下一节中，你将看到如何在 Java 中处理代码块。

### 6.2.2 Lambda 表达式的语法

再次考虑上一节中的排序示例。我们传入一段代码，用于检查一个字符串是否比另一个短。我们计算

```java
first.length() - second.length()
```

`first` 和 `second` 是什么？它们都是字符串。Java 是强类型语言，我们也必须指明这一点：
