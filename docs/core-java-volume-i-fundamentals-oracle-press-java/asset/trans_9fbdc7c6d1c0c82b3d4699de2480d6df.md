
如 `List`。由于“类优先”规则，这样的方法永远无法胜过 `Object.toString` 或 `Object.equals`。

### 6.1.7 接口与回调

编程中一种常见模式是*回调*模式。在这种模式中，你指定每当特定事件发生时应该执行的操作。例如，你可能希望当按钮被点击或菜单项被选中时执行某个特定操作。不过，由于你尚未了解如何实现用户界面，我们将考虑一个类似但更简单的情形。

`javax.swing` 包包含一个 `Timer` 类，如果你希望在某个时间间隔过去时收到通知，这个类会很有用。例如，如果程序的一部分包含一个时钟，你可以请求每秒收到一次通知，以便更新钟面。

构造计时器时，你设置时间间隔，并告诉它每当该时间间隔过去时应该做什么。

你如何告诉计时器它应该做什么？在许多编程语言中，你提供一个函数名，让计时器定期调用该函数。然而，Java 标准库中的类采用面向对象的方式。你传入某个类的对象。然后计时器调用该对象上的某个方法。传递对象比传递函数更灵活，因为对象可以携带附加信息。

当然，计时器需要知道调用哪个方法。计时器要求你指定一个类的对象，该类实现 `java.awt.event` 包的 `ActionListener` 接口。该接口如下：

```java
public interface ActionListener
{
    void actionPerformed(ActionEvent event);
}
```

每隔一秒，会显示类似

```
At the tone, the time is 2017-12-16T05:01:49.550Z
```

的消息，随后发出一声蜂鸣。

**注意：**

务必导入 `javax.swing.Timer`。还有一个 `java.util.Timer` 类，它略有不同。

程序清单 6.3 让计时器及其动作监听器开始工作。计时器启动后，程序弹出一个消息对话框，并等待用户单击“确定”按钮来停止。在程序等待用户期间，当前时间会每秒显示一次。（如果省略该对话框，程序会在 `main` 方法退出后立即终止。）

**程序清单 6.3** timer/TimerTest.java

```java
1  package timer;
2
3  /**
4     @version 1.02 2017-12-14
5     @author Cay Horstmann
6  */
7
8  import java.awt.*;
9  import java.awt.event.*;
10 import java.time.*;
11 import javax.swing.*;
12
13 public class TimerTest
14 {
15    public static void main(String[] args)
16    {
var listener = new TimePrinter();

// construct a timer that calls the listener once every second
var timer = new Timer(1000, listener);
timer.start();

// keep program running until the user selects "OK"
JOptionPane.showMessageDialog(null, "Quit program?");
System.exit(0);
}
}

class TimePrinter implements ActionListener
{
   public void actionPerformed(ActionEvent event)
   {
      System.out.println("At the tone, the time is " +
      Instant.ofEpochMilli(event.getWhen()));
      Toolkit.getDefaultToolkit().beep();
   }
}
```

**javax.swing.JOptionPane** 1.2

- `static void showMessageDialog(Component parent, Object message)`

  显示一个带有消息提示和“确定”按钮的对话框。该对话框在父组件上方居中。如果 parent 为 null，则对话框在屏幕上居中。

**javax.swing.Timer** 1.2

- `Timer(int interval, ActionListener listener)`

```java
public interface Comparator<T>
{
    int compare(T first, T second);
}
```

要按长度比较字符串，定义一个实现 `Comparator<String>` 的类：

```java
class LengthComparator implements Comparator<String>
{
    public int compare(String first, String second)
    {
        return first.length() - second.length();
    }
}
```

要实际进行比较，需要创建一个实例：

```java
var comp = new LengthComparator();
if (comp.compare(words[i], words[j]) > 0) . . .
```

将此调用与 `words[i].compareTo(words[j])` 对比。compare 方法是在比较器对象上调用的，而不是在字符串本身上调用的。

![](img/0e7b74ef51a065c077b42cd87b362288_480_0.png)

> **注意：**
>
> 即使 `LengthComparator` 对象没有状态，你仍然需要创建它的一个实例。你需要该实例来调用 compare 方法——它不是静态方法。

要对数组排序，将一个 `LengthComparator` 对象传递给 `Arrays.sort` 方法：

```java
String[] friends = { "Peter", "Paul", "Mary" };
Arrays.sort(friends, new LengthComparator());
```

现在该数组要么是 `["Paul", "Mary", "Peter"]`，要么是 `["Mary", "Paul", "Peter"]`。

你将在第 338 页的[6.2 节“Lambda 表达式”](#)中看到如何使用 lambda 表达式更轻松地使用 Comparator。

### 6.1.9 对象克隆

本节讨论 `Cloneable` 接口，它表示某个类提供了安全的 clone 方法。由于克隆并不十分常见，而且细节相当技术化，你可能只想在需要之前大致浏览一下这些内容。

要理解克隆的含义，回想一下当你复制一个持有对象引用的变量时会发生什么。原始变量和副本都是对同一对象的引用（见[图 6.1](#)）。这意味着对任一变量的修改也会影响另一个。

```java
var original = new Employee("John Public", 50000);
Employee copy = original;
copy.raiseSalary(10); // oops--also changed original
```

![](img/0e7b74ef51a065c077b42cd87b362288_482_0.png)

**图 6.1** 复制与克隆

如果你希望 copy 成为一个新对象，它在创建时与 original 相同，但其状态可以随时间而不同，请使用 clone 方法。

![](img/0e7b74ef51a065c077b42cd87b362288_484_0.png)

图 6.2 浅拷贝

副本是浅拷贝会有影响吗？这取决于情况。如果原始对象与浅克隆之间共享的子对象是*不可变的*，那么共享是安全的。如果该子对象属于不可变类，例如 `String`，就确实会如此。另一种情况是，该子对象可能在对象的整个生命周期内保持不变，没有修改器接触它，也没有方法返回对它的引用。

然而，子对象经常是*可变的*，你必须重新定义 `clone` 方法来进行*深拷贝*，同时克隆子对象。在我们的示例中，`hireDay` 字段是 `Date`，它是可变的，因此它也必须被克隆。（出于这个原因，本示例使用 `Date` 类型的字段，而不是 `LocalDate`，来演示克隆过程。如果 `hireDay` 是不可变 `LocalDate` 类的实例，则不需要进一步操作。）

对于每个类，你需要决定是否：

- 1. 默认的 `clone` 方法已经足够好；
- 2. 默认的 `clone` 方法可以通过对可变子对象调用 `clone` 来修补；或者
- 3. 不应尝试 `clone`。

第三个选项实际上是默认选项。要选择第一个或第二个选项，类必须：

- 1. 实现 `Cloneable` 接口；并且
- 2. 用 `public` 访问修饰符重新定义 `clone` 方法。

**注意：**

`clone` 方法在 `Object` 类中声明为 `protected`，因此你的代码不能简单地调用 `anObject.clone()`。但是，protected 方法不是可以从任何子类访问吗？而且每个类不都是 `Object` 的子类吗？幸运的是，protected 访问的规则更加微妙（见第 5 章）。子类只能调用 protected 的 `clone` 方法来克隆*它自己的*对象。你必须将 `clone` 重新定义为 public，才能允许任何方法克隆对象。

在这种情况下，`Cloneable` 接口的出现与接口的常规用法无关。特别地，它*并不*指定 `clone` 方法——该方法继承自 `Object` 类。该接口仅充当一个标记，表明类设计者理解克隆过程。对象对克隆如此偏执，以至于如果某个对象请求克隆但没有实现该接口，就会生成一个受检异常。

**注意：**

`Cloneable` 接口是 Java 提供的少数*标签接口*之一。（有些程序员称它们为*标记接口*。）回想一下，
