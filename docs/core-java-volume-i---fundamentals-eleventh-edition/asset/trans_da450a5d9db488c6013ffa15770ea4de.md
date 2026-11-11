
> **注意：** 所有数组类型都有一个 clone 方法，它是 public 的，而不是 protected 的。你可以用它创建一个新数组，其中包含所有元素的副本。例如：
>
> ```java
> int[] luckyNumbers = { 2, 3, 5, 7, 11, 13 };
> int[] cloned = luckyNumbers.clone();
> cloned[5] = 12; // doesn't change luckyNumbers[5]
> ```

> **注意：** 第 II 卷第 2 章展示了另一种克隆对象的机制，它使用 Java 的对象序列化特性。该机制易于实现且安全，但效率不高。

## 清单 6.4 `clone/CloneTest.java`

```java
package clone;

/**
 * This program demonstrates cloning.
 * @version 1.1 2018-03-16
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

## 清单 6.5 `clone/Employee.java`

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
        return "Employee[name=" + name + ", salary=" + salary + ", hireDay=" + hireDay + "]";
    }
}
```

## 6.2 Lambda 表达式

在接下来的几节中，你将学习如何使用 lambda 表达式以简洁的语法定义代码块，以及如何编写使用 lambda 表达式的代码。

### 6.2.1 为什么使用 Lambda？

lambda 表达式是一段可以传递的代码块，以便稍后执行一次或多次。在深入语法（甚至这个奇怪的名字）之前，让我们退一步，看看在 Java 中哪些地方用过这样的代码块。

在第 310 页的 6.1.7 节“接口与回调”中，你看到了如何按时间间隔执行工作。把工作放进 ActionListener 的 actionPerformed 方法中：

```java
class Worker implements ActionListener
{
   public void actionPerformed(ActionEvent event)
   {
      // do some work
   }
}
```

然后，当你想要重复执行这段代码时，构造一个 Worker 类的实例。再把这个实例提交给一个 Timer 对象。

关键在于，actionPerformed 方法包含了你希望稍后执行的代码。

或者考虑使用自定义比较器进行排序。如果你想按长度而不是默认的字典顺序对字符串排序，可以把一个 Comparator 对象传给 sort 方法：

```java
class LengthComparator implements Comparator<String>
{
   public int compare(String first, String second)
   {
      return first.length() - second.length();
   }
}

Arrays.sort(strings, new LengthComparator());
```

compare 方法不会立即被调用。相反，sort 方法会不断调用 compare 方法，如果元素顺序不对就重新排列它们，直到数组排好序。你给 sort 方法提供一段比较元素所需的代码片段，这段代码会被整合到排序逻辑的其余部分中，而你大概并不想重新实现那部分逻辑。

这两个例子有一个共同点。一段代码被传给了某个对象——一个计时器或一个 sort 方法。这段代码块在稍后的某个时间被调用。

到目前为止，在 Java 中把一段代码交给别人并不容易。你不能直接传递代码块。Java 是面向对象的语言，因此你必须构造一个对象，它所属的类中有一个包含所需代码的方法。

在其他语言中，可以直接使用代码块。Java 设计者长期以来一直抵制添加这一特性。毕竟，Java 的一大优势就是简洁性和一致性。如果一门语言包含了每一个只能让代码略微更简洁的特性，它可能会变得难以维护、一团乱麻。然而，在其他那些语言中，不仅仅是启动线程或注册按钮单击处理器更容易；它们的大量 API 也更简单、更一致、更强大。在 Java 中，本来可以编写类似的 API，接收实现了特定接口的类的对象，但这样的 API 用起来会很不愉快。

有一段时间，问题不是要不要为函数式编程扩展 Java，而是如何扩展。经过数年的实验，才出现了一种适合 Java 的设计。在下一节中，你将看到如何在 Java 中使用代码块。

### 6.2.2 Lambda 表达式的语法

再次考虑上一节中的排序示例。我们传入的代码检查一个字符串是否比另一个短。我们计算

```java
first.length() - second.length()
```

这里的 *first* 和 *second* 是什么？它们都是字符串。Java 是强类型语言，我们也必须指明这一点：

```java
(String first, String second)
    -> first.length() - second.length()
```

你刚刚看到了第一个 *lambda 表达式*。这样的表达式就是一段代码块，以及必须传给该代码的任何变量的说明。

为什么叫这个名字？很多年前，在计算机出现之前，逻辑学家阿隆佐·邱奇想要形式化“数学函数有效可计算”意味着什么。（奇怪的是，有些函数已知存在，但没人知道如何计算它们的值。）他用希腊字母 lambda（λ）来标记参数。如果他知道 Java API，他会写成

```java
λfirst.λsecond.first.length() - second.length()
```

> **注意：** 为什么用字母 λ？邱奇把字母表里的其他字母都用完了吗？
> 实际上，令人尊敬的 *《数学原理》* 用 ^ 重音符号表示自由变量，这启发邱奇用大写 lambda Λ 表示参数。但最终，他改用了小写版本。从那以后，带有参数变量的表达式就一直被称为 lambda 表达式。

你刚刚看到了 Java 中 lambda 表达式的一种形式：参数、-> 箭头和一个表达式。如果代码执行的计算无法放入单个表达式，就完全像编写方法那样来写：用 {} 括起来，并显式使用 return 语句。例如，

```java
(String first, String second) ->
{
    if (first.length() < second.length()) return -1;
    else if (first.length() > second.length()) return 1;
    else return 0;
}
```

如果 lambda 表达式没有参数，仍然要提供空括号，就像无参方法一样：

```java
() -> { for (int i = 100; i >= 0; i--) System.out.println(i); }
```

如果可以推断 lambda 表达式的参数类型，就可以省略它们。例如，

```java
Comparator<String> comp
    = (first, second) // same as (String first, String second)
        -> first.length() - second.length();
```

这里，编译器可以推断 first 和 second 必定是字符串，因为该 lambda 表达式被赋给了一个字符串比较器。（下一节我们将更仔细地研究这个赋值。）

如果一个方法只有一个类型可推断的参数，甚至可以省略括号：

```java
ActionListener listener = event ->
    System.out.println("The time is "
        + Instant.ofEpochMilli(event.getWhen()));
    // instead of (event) -> . . . or (ActionEvent event) -> . . .
```
