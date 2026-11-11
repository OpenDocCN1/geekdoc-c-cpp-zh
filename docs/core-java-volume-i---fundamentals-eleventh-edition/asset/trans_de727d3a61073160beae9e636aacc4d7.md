
但这里有个问题。看看 `min` 方法的代码。变量 `smallest` 的类型是 T，这意味着它可能是任意类的对象。我们怎么知道 T 所属的类有一个 `compareTo` 方法呢？

解决方案是将 T 限制为实现 `Comparable` 接口的类——这是一个只包含一个方法 `compareTo` 的标准接口。可以通过为类型变量 T 指定一个界限来实现：

```java
public static <T extends Comparable> T min(T[] a) ...
```

实际上，`Comparable` 接口本身就是一个泛型类型。目前，我们将忽略这种复杂性以及编译器生成的警告。第459页的第8.8节“通配符类型”讨论了如何将类型参数与 `Comparable` 接口正确配合使用。

现在，泛型 `min` 方法只能用于调用那些元素类实现了 `Comparable` 接口的数组，例如 `String`、`LocalDate` 等。用 `Rectangle` 数组调用 `min` 会导致编译时错误，因为 `Rectangle` 类没有实现 `Comparable`。

> **C++ 注：** 在 C++ 中，你不能限制模板参数的类型。如果程序员用不合适的类型实例化模板，那么（通常是晦涩难懂的）错误消息会在模板代码内部报告出来。

你可能想知道，在这种情况下为什么我们使用 `extends` 关键字而不是 `implements` 关键字——毕竟 `Comparable` 是一个接口。下面这种写法

```java
<T extends BoundingType>
```

表示 T 应当是界定类型的子类型。T 和界定类型都可以是类或接口。选择 `extends` 关键字是因为它是对子类型概念的一个合理近似，而且 Java 设计者不想向语言中添加一个新关键字（例如 `sub`）。

类型变量或通配符可以有多个界限。例如：

```java
T extends Comparable & Serializable
```

各个界定类型用与号（`&`）分隔，因为逗号用于分隔类型变量。

与 Java 继承一样，你可以拥有任意多个接口超类型，但界限中至多只能有一个类。如果界限中包含一个类，那么它必须是界限列表中的第一个。

在下一个示例程序（清单 8.2）中，我们将 minmax 方法重写为泛型方法。该方法计算一个泛型数组的最小值和最大值，并返回一个 `Pair<T>`。

### 清单 8.2 pair2/PairTest2.java

```java
package pair2;

import java.time.*;

/**
 * @version 1.02 2015-06-21
 * @author Cay Horstmann
 */
public class PairTest2
{
   public static void main(String[] args)
   {
      LocalDate[] birthdays =
         {
            LocalDate.of(1906, 12, 9), // G. Hopper
            LocalDate.of(1815, 12, 10), // A. Lovelace
            LocalDate.of(1903, 12, 3), // J. von Neumann
            LocalDate.of(1910, 6, 22), // K. Zuse
         };
      Pair<LocalDate> mm = ArrayAlg.minmax(birthdays);
      System.out.println("min = " + mm.getFirst());
      System.out.println("max = " + mm.getSecond());
   }
}

class ArrayAlg
{
   /**
      Gets the minimum and maximum of an array of objects of type T.
      @param a an array of objects of type T
      @return a pair with the min and max values, or null if a is null or empty
   */
   public static <T extends Comparable> Pair<T> minmax(T[] a)
   {
      if (a == null || a.length == 0) return null;
      T min = a[0];
      T max = a[0];
      for (int i = 1; i < a.length; i++)
      {
         if (min.compareTo(a[i]) > 0) min = a[i];
         if (max.compareTo(a[i]) < 0) max = a[i];
      }
      return new Pair<>(min, max);
   }
}
```

## 8.5 泛型代码与虚拟机

虚拟机没有泛型类型的对象——所有对象都属于普通类。早期版本的泛型实现甚至能够把使用泛型的程序编译成可在 1.0 虚拟机上执行的类文件！在接下来的几节中，你将看到编译器如何“擦除”类型参数，以及这个过程对 Java 程序员意味着什么。

### 8.5.1 类型擦除

每当你定义一个泛型类型时，都会自动提供一个相应的*原始类型*。原始类型的名称就是泛型类型的名称去掉类型参数。类型变量会被*擦除*，并替换为其界定类型（对于没有界限的变量，则替换为 `Object`）。

例如，`Pair<T>` 的原始类型如下所示：

```java
public class Pair
{
   private Object first;
   private Object second;

   public Pair(Object first, Object second)
   {
      this.first = first;
      this.second = second;
   }

   public Object getFirst() { return first; }
   public Object getSecond() { return second; }

   public void setFirst(Object newValue) { first = newValue; }
   public void setSecond(Object newValue) { second = newValue; }
}
```

由于 `T` 是一个无界类型变量，所以它被直接替换为 `Object`。

结果就是一个普通类，就像在 Java 加入泛型之前你可能会实现的那样。

你的程序可能包含不同种类的 `Pair`，例如 `Pair<String>` 或 `Pair<LocalDate>`，但擦除会把它们全都变成原始 `Pair` 类型。

> **C++ 注：** 在这方面，Java 泛型与 C++ 模板非常不同。C++ 会为每个模板实例化产生不同的类型——这种现象称为“模板代码膨胀”。Java 不存在这个问题。

原始类型会用第一个界限替换类型变量；如果没有给出界限，则替换为 Object。例如，类 Pair<T> 中的类型变量没有显式界限，因此原始类型会用 Object 替换 T。假设我们声明一个略有不同的类型：

```java
public class Interval<T extends Comparable & Serializable> implements Serializable
{
    private T lower;
    private T upper;
    ...
    public Interval(T first, T second)
    {
        if (first.compareTo(second) <= 0) { lower = first; upper = second; }
        else { lower = second; upper = first; }
    }
}
```

原始类型 Interval 如下所示：

```java
public class Interval implements Serializable
{
    private Comparable lower;
    private Comparable upper;
    ...
    public Interval(Comparable first, Comparable second) { . . . }
}
```

> **注意：** 你可能想知道，如果交换界限会发生什么：class Interval<T extends Serializable & Comparable>。在这种情况下，原始类型会用 Serializable 替换 T，并且编译器会在必要时插入到 Comparable 的强制类型转换。因此，为了提高效率，你应该把标记接口（即没有方法的接口）放在界限列表的末尾。

### 8.5.2 转换泛型表达式

当你编写对泛型方法的调用时，如果返回类型已被擦除，编译器会插入强制类型转换。例如，考虑下面这组语句

```java
Pair<Employee> buddies = . . .;
Employee buddy = buddies.getFirst();
```

`getFirst` 擦除后的返回类型是 `Object`。编译器会自动插入到 `Employee` 的强制类型转换。也就是说，编译器把这个方法调用转换成两条虚拟机指令：

- 调用原始方法 `Pair.getFirst`
- 将返回的 `Object` 强制转换为 `Employee` 类型

当你访问泛型字段时，也会插入强制类型转换。假设 `Pair` 类的 first 和 second 字段是 public 的。（这也许不是好的编程风格，但它是合法的 Java。）那么表达式

```java
Employee buddy = buddies.first;
```

在生成的字节码中也会插入强制类型转换。

### 8.5.3 转换泛型方法

泛型方法也会发生类型擦除。程序员通常会把这样一个泛型方法

```java
public static <T extends Comparable> T min(T[] a)
```

看作一整个方法家族，但在擦除之后，只剩下一个方法：

```java
public static Comparable min(Comparable[] a)
```

注意，类型参数 `T` 已被擦除，只留下它的界定类型 `Comparable`。

方法擦除会带来一些复杂情况。考虑这个例子：

```java
class DateInterval extends Pair<LocalDate>
{
    public void setSecond(LocalDate second)
    {
        if (second.compareTo(getFirst()) >= 0)
            super.setSecond(second);
        . . .
    }
}
```

日期区间是一对 `LocalDate` 对象，我们会希望重写这些方法，以确保第二个值永远不会小于第一个值。这个类被擦除为

```java
class DateInterval extends Pair // after erasure
{
    public void setSecond(LocalDate second) { . . . }
    . . .
}
```
