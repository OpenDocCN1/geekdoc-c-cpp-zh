
```java
class TimePrinter implements ActionListener
{
    public void actionPerformed(ActionEvent event)
    {
        System.out.println("At the tone, the time is "
            + Instant.ofEpochMilli(event.getWhen()));
        if (beep) Toolkit.getDefaultToolkit().beep();
    }
}

var listener = new TimePrinter();
var timer = new Timer(interval, listener);
timer.start();
}
```

局部类从不用访问修饰符（即 public 或 private）声明。它们的作用域始终限制在声明它们的块中。

局部类有一个很大的优势：它们对外部世界完全隐藏——甚至 TalkingClock 类中的其他代码也无法访问它们。除了 start 之外，没有任何方法知道 TimePrinter 类。

### 6.3.5 访问外部方法中的变量

局部类相比其他内部类还有另一个优势。它们不仅能访问外部类的字段，甚至还能访问局部变量！不过，这些局部变量必须是*事实上的 final*。这意味着，一旦赋值，它们就不能再改变。

这是一个典型示例。我们把 interval 和 beep 参数从 TalkingClock 构造器移到 start 方法中。

```java
public void start(int interval, boolean beep)
{
    class TimePrinter implements ActionListener
    {
        public void actionPerformed(ActionEvent event)
        {
            System.out.println("At the tone, the time is "
                + Instant.ofEpochMilli(event.getWhen()));
            if (beep) Toolkit.getDefaultToolkit().beep();
        }
    }

    var listener = new TimePrinter();
    var timer = new Timer(interval, listener);
    timer.start();
}
```

注意，`TalkingClock` 类不再需要存储 beep 实例字段。它只是引用 `start` 方法的 beep 参数变量。

也许这并不那么令人惊讶。下面这行

```java
if (beep) . . .
```

毕竟最终位于 `start` 方法内部，那么它为什么不能访问 beep 变量的值呢？

为了弄清这里为什么存在一个微妙的问题，让我们更仔细地考察控制流。

- 1. 调用 `start` 方法。
- 2. 通过调用内部类 `TimePrinter` 的构造器来初始化对象变量 `listener`。
- 3. 将 listener 引用传递给 `Timer` 构造器，启动计时器，然后 `start` 方法退出。此时，`start` 方法的 beep 参数变量已不再存在。
- 4. 一秒后，如果 `(beep) . . .`，则执行 `actionPerformed` 方法。

为了让 `actionPerformed` 方法中的代码能够工作，`TimePrinter` 类必须在 beep 参数值消失之前，将 beep 字段复制为 `start` 方法的局部变量。实际情况正是如此。在我们的示例中，编译器为这个局部内部类合成名称 `TalkingClock$1TimePrinter`。如果你再次使用 `ReflectionTest` 程序来窥探 `TalkingClock$1TimePrinter` 类，将得到以下输出：

```java
class TalkingClock$1TimePrinter
{
    TalkingClock$1TimePrinter(TalkingClock, boolean);

    public void actionPerformed(java.awt.event.ActionEvent);

    final boolean val$beep;
    final TalkingClock this$0;
}
```

注意构造器的 boolean 参数和 `val$beep` 实例变量。创建对象时，beep 值被传入构造器并存储在 `val$beep` 字段中。编译器会检测对局部变量的访问，为每个局部变量生成匹配的实例字段，并将局部变量复制到构造器中，以便初始化这些实例字段。

### 6.3.6 匿名内部类

使用局部内部类时，通常还可以更进一步。如果你只想创建这个类的一个对象，甚至不需要给这个类命名。这样的类称为*匿名内部类*。

```java
public void start(int interval, boolean beep)
{
   var listener = new ActionListener()
      {
         public void actionPerformed(ActionEvent event)
         {
            System.out.println("At the tone, the time is "
               + Instant.ofEpochMilli(event.getWhen()));
            if (beep) Toolkit.getDefaultToolkit().beep();
         }
      };
   var timer = new Timer(interval, listener);
   timer.start();
}
```

这种语法确实非常晦涩。它的含义是：创建一个实现了 ActionListener 接口的类的新对象，其中所需的方法 `actionPerformed` 就是在花括号 `{ }` 内定义的那个方法。

一般来说，语法如下：

```java
new SuperType(construction parameters)
   {
      inner class methods and data
   }
```

这里，*SuperType* 可以是接口，例如 `ActionListener`；此时，内部类实现该接口。*SuperType* 也可以是类；此时，内部类扩展该类。

匿名内部类不能有构造器，因为构造器的名称必须与类名相同，而这个类没有名称。相反，构造参数会传递给*超类*构造器。特别地，每当内部类实现一个接口时，它不能有任何构造参数。不过，你必须提供一对圆括号，如下所示：

```java
new InterfaceType()
   {
      methods and data
   }
```

> **注意：** 下面这个技巧称为*双花括号初始化*，它利用了内部类语法。假设你想构造一个数组列表并将其传递给一个方法：
>
> ```java
> var friends = new ArrayList<String>();
> friends.add("Harry");
> friends.add("Tony");
> invite(friends);
> ```
>
> 如果你不再需要这个数组列表，将它设为匿名对象会很好。但这样如何添加元素呢？方法如下：
>
> ```java
> invite(new ArrayList<String>() {{ add("Harry"); add("Tony"); }});
> ```
>
> 注意双花括号。外层花括号创建了 `ArrayList` 的一个匿名子类。内层花括号是一个对象初始化块（见第 4 章）。
>
> 在实践中，这个技巧很少有用。更常见的情况是，`invite` 方法愿意接受任何 `List<String>`，你可以直接传入 `List.of("Harry", "Tony")`。

> **警告：** 创建一个与超类几乎相同、但并不完全相同的匿名子类通常很方便。但你需要小心 `equals` 方法。在第 5 章中，我们建议你的 equals 方法使用如下测试：
>
> ```java
> if (getClass() != other.getClass()) return false;
> ```
>
> 匿名子类将无法通过这个测试。

> **提示：** 在生成日志或调试消息时，你常常希望包含当前类的名称，例如
>
> ```java
> System.err.println("Something awful happened in " + getClass());
> ```
>
> 但这在静态方法中会失败。毕竟，对 `getClass` 的调用会调用 `this.getClass()`，而静态方法没有 `this`。请改用以下表达式：
>
> ```java
> new Object(){}.getClass().getEnclosingClass() // gets class of static method
> ```
>
> 这里，`new Object(){}` 创建了 `Object` 的一个匿名子类的匿名对象，而 `getEnclosingClass` 获取其外围类——也就是包含该静态方法的类。

### 清单 6.8 `anonymousInnerClass/AnonymousInnerClassTest.java`

```java
package anonymousInnerClass;
```

### 6.3.7 静态内部类

有时，你可能只是想用一个内部类将一个类隐藏在另一个类中——但你不需要这个内部类持有对外部类对象的引用。你可以通过将内部类声明为 static 来抑制生成该引用。

下面是一个你可能需要这样做的典型示例。考虑计算数组中最小值和最大值的任务。当然，你会编写一个方法计算最小值，另一个方法计算最大值。调用这两个方法时，数组会被遍历两次。只遍历数组一次、同时计算最小值和最大值会更高效。

```java
double min = Double.POSITIVE_INFINITY;
double max = Double.NEGATIVE_INFINITY;
for (double v : values)
{
    if (min > v) min = v;
    if (max < v) max = v;
}
```

然而，该方法必须返回两个数。我们可以通过定义一个包含两个值的 Pair 类来实现：

```java
class Pair
{
    private double first;
    private double second;

    public Pair(double f, double s)
    {
        first = f;
        second = s;
    }
    public double getFirst() { return first; }
    public double getSecond() { return second; }
}
```

然后，minmax 方法可以返回一个 Pair 类型的对象。

```java
class ArrayAlg
{
    public static Pair minmax(double[] values)
    {
        ...
        return new Pair(min, max);
    }
}
```
