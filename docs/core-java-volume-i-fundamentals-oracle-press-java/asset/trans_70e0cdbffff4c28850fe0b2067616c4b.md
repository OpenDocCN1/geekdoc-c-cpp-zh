
```java
    }

    public Object getFirst() { return first; }
    public Object getSecond() { return second; }

    public void setFirst(Object newValue) { first = newValue; }
    public void setSecond(Object newValue) { second = newValue;
    }
    }
```

由于 T 是无界类型变量，因此它被简单地替换为 Object。

结果是一个普通类，就像在 Java 添加泛型之前你可能实现的那样。

你的程序可能包含不同种类的 Pair，例如 Pair<String> 或 Pair<LocalDate>，但类型擦除会把它们全都变成原始 Pair 类型。

> **C++ 注意：**
>
> 在这方面，Java 泛型与 C++ 模板非常不同。C++ 会为每个模板实例化产生不同的类型——这种现象称为“模板代码膨胀”。Java 不会遇到这个问题。

原始类型会用第一个上界替换类型变量；如果没有给出上界，则用 Object 替换。例如，类 Pair<T> 中的类型变量没有显式上界，因此原始类型会用 Object 替换 T。假设我们声明一个稍有不同的类型：

```java
public class Interval<T extends Comparable & Serializable>
implements Serializable
{
    private T lower;
    private T upper;
    . . .
    public Interval(T first, T second)
    {
        if (first.compareTo(second) <= 0) { lower = first; upper = second; }
        else { lower = second; upper = first; }
    }
}
```

原始类型 `Interval` 看起来像这样：

```java
public class Interval implements Serializable
{
    private Comparable lower;
    private Comparable upper;
    . . .
    public Interval(Comparable first, Comparable second) { . . .
    }
}
```

**注意：**

你可能想知道如果交换上界会发生什么：`class Interval<T extends Serializable & Comparable>`。在这种情况下，原始类型会用 `Serializable` 替换 `T`，并且编译器会在必要时插入到 `Comparable` 的强制类型转换。因此，为了提高效率，你应该把标记接口（即没有方法的接口）放在上界列表的末尾。

### 8.5.2 翻译泛型表达式

当你编写对泛型方法的调用时，如果返回类型已被擦除，编译器会插入强制类型转换。例如，考虑下面这组语句

```java
Pair<Employee> buddies = . . .;
Employee buddy = buddies.getFirst();
```

`getFirst` 的擦除结果返回类型为 `Object`。编译器会自动插入到 `Employee` 的强制类型转换。也就是说，编译器把该方法调用翻译成两条虚拟机指令：

- 调用原始方法 Pair.getFirst
- 将返回的 Object 强制转换为 Employee 类型

当你访问泛型字段时，也会插入强制类型转换。假设 Pair 类的 first 和 second 字段是 public 的。（也许这不是良好的编程风格，但它是合法的 Java。）那么表达式

```java
Employee buddy = buddies.first;
```

在生成的字节码中也会插入强制类型转换。

### 8.5.3 翻译泛型方法

类型擦除也会发生在泛型方法上。程序员通常会把这样一个泛型方法

```java
public static <T extends Comparable> T min(T[] a)
```

看作一整族方法，但擦除之后，只剩下一个方法：

```java
public static Comparable min(Comparable[] a)
```

注意，类型参数 T 已被擦除，只留下它的上界类型 Comparable。

方法的擦除会带来几个复杂问题。考虑这个例子：

```java
class DateInterval extends Pair<LocalDate>
{
    public void setSecond(LocalDate second)
    {
        if (second.compareTo(getFirst()) >= 0)
            super.setSecond(second);
    }
    . . .
}
```

日期区间是一对 LocalDate 对象，我们会想要重写这些方法，以确保第二个值永远不会小于第一个值。这个类被擦除为

```java
class DateInterval extends Pair // after erasure
{
    public void setSecond(LocalDate second) { . . . }
    . . .
}
```

也许令人惊讶的是，还有另一个从 Pair 继承来的 setSecond 方法，即

```java
public void setSecond(Object second)
```

这显然是一个不同的方法，因为它的参数类型不同——是 Object 而不是 LocalDate。但它不应该是不同的。考虑下面这组语句：

```java
var interval = new DateInterval(. . .);
Pair<LocalDate> pair = interval; // OK--assignment to superclass
pair.setSecond(aDate);
```

我们期望对 setSecond 的调用是多态的，并且会调用合适的方法。由于 pair 引用的是一个 DateInterval 对象，因此那个

你不能那样写 Java 代码；有两个参数类型相同的方法——在这里是没有参数——是非法的。然而，在虚拟机中，参数类型*和返回类型*共同指定一个方法。因此，编译器可以为两个仅在返回类型上不同的方法生成字节码，而虚拟机会正确处理这种情况。

**注意：**

桥方法并不限于泛型类型。你在第 5 章已经看到，在重写另一个方法时，方法可以指定一个限制更严格的返回类型，这是合法的。例如：

```java
public class Employee implements Cloneable
{
    public Employee clone() throws CloneNotSupportedException {
    . . . }
}
```

`Object.clone` 和 `Employee.clone` 方法被称为具有*协变返回类型*。

实际上，`Employee` 类有*两个* clone 方法：

```java
Employee clone() // defined above
Object clone()   // synthesized bridge method, overrides Object.clone
```

合成的桥方法会调用新定义的方法。

总之，你需要记住以下关于 Java 泛型翻译的事实：

- 虚拟机中没有泛型，只有普通类和方法。
- 所有类型参数都被它们的上界替换。
- 合成桥方法以保持多态性。
- 根据需要插入强制类型转换以保持类型安全。

### 8.5.4 调用遗留代码

设计 Java 泛型时，一个主要目标是允许泛型与遗留代码之间具有互操作性。让我们看一个这种遗留代码的具体例子。Swing 用户界面工具包提供了一个 JSlider 类，它的“刻度”可以用包含文本或图像的标签来定制。这些标签通过以下调用设置

```java
void setLabelTable(Dictionary table)
```

Dictionary 类将整数映射到标签。在 Java 5 之前，该类被实现为 Object 实例的映射。Java 5 使 Dictionary 成为泛型类，但 JSlider 从未更新。此时，不带类型参数的 Dictionary 是一个原始类型。兼容性就在这里发挥作用。

当你填充字典时，可以使用泛型类型。

```java
Dictionary<Integer, Component> labelTable = new Hashtable<>();
labelTable.put(0, new JLabel(new ImageIcon("nine.gif")));
labelTable.put(20, new JLabel(new ImageIcon("ten.gif")));
. . .
```

当你把 Dictionary<Integer, Component> 对象传递给 setLabelTable 时，编译器会发出警告。

```java
slider.setLabelTable(labelTable); // warning
```

毕竟，编译器无法保证 setLabelTable 会对 Dictionary 对象做什么。该方法可能把所有键替换为字符串。这就破坏了键具有 `Integer` 类型的保证，未来的操作可能引发错误的强制类型转换异常。

你应该仔细想一想，并问一问 `JSlider` 实际上会拿这个 `Dictionary` 对象做什么。在我们的例子中，很清楚 `JSlider` 只读取信息，因此你可以忽略该警告。

现在考虑相反的情况：你从遗留类得到一个原始类型的对象。你可以把它赋给一个使用泛型的变量，但当然会收到警告。例如：

```java
Dictionary<Integer, Component> labelTable =
slider.getLabelTable(); // warning
```

这没问题——检查该警告，并确保标签表确实包含 `Integer` 和 `Component` 对象。当然，从来就没有绝对的保证。恶意程序员可能在滑块中安装了不同的 `Dictionary`。但同样，这种情况并不比泛型出现之前更糟。最坏情况下，你的程序会抛出异常。

在你仔细考虑完警告之后，可以使用一个*注解*让它消失。你可以注解一个局部变量：

```java
@SuppressWarnings("unchecked")
Dictionary<Integer, Component> labelTable =
slider.getLabelTable(); // no warning
```

或者你可以注解整个方法，像这样：

```java
@SuppressWarnings("unchecked")
public void configureSlider() { ... }
```

这个注解会关闭该方法内部所有代码的检查。

## 8.6 限制与局限性
