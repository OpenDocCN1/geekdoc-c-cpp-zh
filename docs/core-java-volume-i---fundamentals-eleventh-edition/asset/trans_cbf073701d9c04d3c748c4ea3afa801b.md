

```java
public class TalkingClock
{
    private int interval;
    private boolean beep;

    public TalkingClock(int interval, boolean beep) { . . . }
    public void start() { . . . }

    public class TimePrinter implements ActionListener
        // an inner class
    {
        . . .
    }
}
```

请注意，TimePrinter 类现在位于 TalkingClock 类内部。这*并不*意味着每个 TalkingClock 都有一个 TimePrinter 实例字段。正如你将看到的，TimePrinter 对象是由 TalkingClock 类的方法构造的。

下面是更详细的 TimePrinter 类。请注意，actionPerformed 方法在发出蜂鸣声之前会检查 beep 标志。

```java
public class TimePrinter implements ActionListener
{
    public void actionPerformed(ActionEvent event)
    {
        System.out.println("At the tone, the time is "
            + Instant.ofEpochMilli(event.getWhen()));
        if (beep) Toolkit.getDefaultToolkit().beep();
    }
}
```

有些令人惊讶的事情正在发生。TimePrinter 类没有名为 beep 的实例字段或变量。相反，beep 引用的是创建这个 TimePrinter 的 TalkingClock 对象的字段。正如你所看到的，内部类方法既可以访问自己的数据字段，也可以访问创建它的外部对象的数据字段。

为了实现这一点，内部类对象总是会获得一个指向创建它的对象的隐式引用（见图6.3）。

这个引用在内部类的定义中是不可见的。然而，为了阐明这个概念，让我们把这个对外部对象的引用称为 *outer*。那么 actionPerformed 方法等价于以下代码：

```java
public void actionPerformed(ActionEvent event)
{
    System.out.println("At the tone, the time is "
        + Instant.ofEpochMilli(event.getWhen()));
    if (outer.beep) Toolkit.getDefaultToolkit().beep();
}
```

> **注意：** 我们可以将 `TimePrinter` 类声明为 private。这样，只有 `TalkingClock` 的方法才能构造 `TimePrinter` 对象。只有内部类可以是 private。普通类始终具有包访问权限或公共访问权限。

## **清单 6.7** `innerClass/InnerClassTest.java`

```java
package innerClass;

import java.awt.*;
import java.awt.event.*;
import java.time.*;

import javax.swing.*;

/**
 * This program demonstrates the use of inner classes.
 * @version 1.11 2017-12-14
 * @author Cay Horstmann
 */
public class InnerClassTest
{
   public static void main(String[] args)
   {
      var clock = new TalkingClock(1000, true);
      clock.start();

      // keep program running until the user selects "OK"
      JOptionPane.showMessageDialog(null, "Quit program?");
      System.exit(0);
   }
}

/**
 * A clock that prints the time in regular intervals.
 */
class TalkingClock
{
   private int interval;
   private boolean beep;

   /**
    * Constructs a talking clock
    * @param interval the interval between messages (in milliseconds)
    * @param beep true if the clock should beep
    */
   public TalkingClock(int interval, boolean beep)
   {
       this.interval = interval;
       this.beep = beep;
   }

   /**
    * Starts the clock.
    */
   public void start()
   {
       var listener = new TimePrinter();
       var timer = new Timer(interval, listener);
       timer.start();
   }

   public class TimePrinter implements ActionListener
   {
       public void actionPerformed(ActionEvent event)
       {
           System.out.println("At the tone, the time is "
               + Instant.ofEpochMilli(event.getWhen()));
           if (beep) Toolkit.getDefaultToolkit().beep();
       }
   }
}
```

### 6.3.2 内部类的特殊语法规则

在上一节中，我们通过将内部类的外部类引用称为 *outer* 来解释它。实际上，外部引用的正确语法要稍微复杂一些。表达式

`OuterClass.this`

表示外部类引用。例如，你可以将 `TimePrinter` 内部类的 `actionPerformed` 方法写成

```java
public void actionPerformed(ActionEvent event)
{
    if (TalkingClock.this.beep) Toolkit.getDefaultToolkit().beep();
}
```

相反，你可以使用以下语法更显式地编写内部对象构造函数：

`outerObject.new InnerClass(construction parameters)`

例如：

例如，TalkingClock 类内部的 TimePrinter 类会被转换成一个类文件 `TalkingClock$TimePrinter.class`。要了解其工作原理，请尝试以下实验：运行第5章的 ReflectionTest 程序，并将类 `TalkingClock$TimePrinter` 交给它进行反射。或者，直接使用 `javap` 工具：

```bash
javap -private ClassName
```

> **注意：** 如果你使用 UNIX，请记住在命令行中提供类名时转义 `$` 字符。也就是说，像下面这样运行 ReflectionTest 或 javap 程序：
>
> ```bash
> javap reflection.ReflectionTest innerClass.TalkingClock\$TimePrinter
> ```
>
> 或
>
> ```bash
> javap -private innerClass.TalkingClock\$TimePrinter
> ```

你将得到以下输出：

```java
public class innerClass.TalkingClock$TimePrinter
    implements java.awt.event.ActionListener
{
    final innerClass.TalkingClock this$0;
    public innerClass.TalkingClock$TimePrinter(innerClass.TalkingClock);
    public void actionPerformed(java.awt.event.ActionEvent);
}
```

你可以清楚地看到，编译器为外部类引用生成了一个额外的实例字段 `this$0`。（名称 `this$0` 是由编译器合成的——你无法在代码中引用它。）你还可以看到构造函数的 TalkingClock 参数。

如果编译器可以自动完成这种转换，难道你不能手动实现相同的机制吗？让我们试一试。我们将 TimePrinter 变成一个位于 TalkingClock 类之外的普通类。在构造 TimePrinter 对象时，我们将其创建者的 `this` 引用传递给它。

```java
class TalkingClock
{
    . . .
    public void start()
    {
        var listener = new TimePrinter(this);
        var timer = new Timer(interval, listener);
        timer.start();
    }
}
```

```java
class TimePrinter implements ActionListener
{
   private TalkingClock outer;
   . . .
   public TimePrinter(TalkingClock clock)
   {
      outer = clock;
   }
}
```

现在让我们看看 actionPerformed 方法。它需要访问 outer.beep。

```java
if (outer.beep) . . . // ERROR
```

这里我们遇到了一个问题。内部类可以访问外部类的私有数据，但我们的外部 TimePrinter 类却不能。

因此，内部类确实比普通类更强大，因为它们拥有更多的访问权限。

你可能很想知道，如果内部类被转换为带有奇怪名称的普通类——而虚拟机对它们一无所知——它们是如何获得这些额外的访问权限的。为了解开这个谜团，让我们再次使用 ReflectionTest 程序来窥探 TalkingClock 类：

```java
class TalkingClock
{
   private int interval;
   private boolean beep;

   public TalkingClock(int, boolean);

   static boolean access$0(TalkingClock);
   public void start();
}
```

注意编译器添加到外部类的静态 access$0 方法。它返回作为参数传入的对象的 beep 字段。（方法名可能略有不同，例如 access$000，具体取决于你的编译器。）

内部类的方法会调用该方法。TimePrinter 类的 actionPerformed 方法中的语句

```java
if (beep)
```

实际上会进行以下调用：

```java
if (TalkingClock.access$0(outer))
```

这是安全风险吗？当然是。别人调用 `access$0` 方法读取私有 `beep` 字段是很容易的。当然，`access$0` 不是 Java 方法的合法名称。然而，熟悉类文件结构的黑客很容易生成一个带有虚拟机指令的类文件来调用该方法，例如使用十六进制编辑器。由于这些秘密方法具有包访问权限，攻击代码需要放置在与被攻击类相同的包中。

总而言之，如果内部类访问了某个私有数据字段，那么有可能通过添加到外部类所在包中的其他类来访问该数据字段，但这需要技巧和决心。程序员不会偶然获得访问权限，必须故意为此构建或修改类文件。

> **注意：** 合成的构造函数和方法可能会变得相当复杂。（如果你对此感到不适，可以跳过此注释。）假设我们将 `TimePrinter` 变成一个私有内部类。虚拟机中没有私有类，因此编译器会生成一个次佳的选择：一个具有包访问权限和私有构造函数的类：
>
> ```java
> private TalkingClock$TimePrinter(TalkingClock);
> ```
>
> 当然，没有人能调用这个构造函数，所以还有第二个具有包访问权限的构造函数：
>
> ```java
> TalkingClock$TimePrinter(TalkingClock, TalkingClock$1);
> ```
>
> 它调用第一个构造函数。`TalkingClock$1` 类被合成出来仅仅是为了将这个构造函数与其他构造函数区分开。
>
> 编译器将 `TalkingClock` 类 start 方法中的构造函数调用转换为
>
> ```java
> new TalkingClock$TimePrinter(this, null)
> ```

### 6.3.4 局部内部类

如果仔细查看 TalkingClock 示例的代码，你会发现你只需要一次类型名 TimePrinter：也就是在 start 方法中创建该类型的对象时。

在这种情况下，你可以在单个方法中局部地定义这个类。

```java
public void start()
{
}
```

