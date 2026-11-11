

```java
class ArrayAlg
{
    public static <T> T getMiddle(T... a)
    {
        return a[a.length / 2];
    }
}
```

该方法定义在一个普通类中，而不是泛型类中。然而，它是一个泛型方法，从尖括号和类型变量可以看出这一点。注意，类型变量插入在修饰符（本例中为 public static）之后、返回类型之前。

既可以在普通类中定义泛型方法，也可以在泛型类中定义泛型方法。

调用泛型方法时，可以将实际类型放在尖括号中，置于方法名之前：

```java
String middle = ArrayAlg.<String>getMiddle("John", "Q.", "Public");
```

在这种情况下（实际上在大多数情况下），可以从方法调用中省略 `<String>` 类型参数。编译器有足够的信息来推断你想要的方法。它将参数的类型与泛型类型 `T...` 进行匹配，并推断出 `T` 必须是 `String`。也就是说，你可以直接调用

```java
String middle = ArrayAlg.getMiddle("John", "Q.", "Public");
```

几乎在所有情况下，泛型方法的类型推断都能顺利进行。偶尔编译器会出错，这时你需要解读错误报告。考虑下面这个例子：

```java
double middle = ArrayAlg.getMiddle(3.14, 1729, 0);
```

错误消息会以晦涩的措辞（不同编译器版本措辞不同）抱怨说，这段代码有两种解释方式，而且两种都同样有效。简而言之，编译器将参数自动装箱为一个 `Double` 和两个 `Integer` 对象，然后试图找到这些类的公共超类型。它实际上找到了两个：`Number` 和 `Comparable` 接口，而 `Comparable` 本身就是一个泛型类型。在这种情况下，解决办法是将所有参数都写成 `double` 值。

**提示：**

如果你想查看编译器为泛型方法调用推断出哪种类型，Peter von der Ahé 推荐这个技巧：故意引入一个错误，并研究由此产生的错误消息。例如，考虑调用 `ArrayAlg.getMiddle("Hello", 0, null)`。将结果赋给一个 `JButton`，这不可能正确。你会得到如下错误报告：

```
found:
java.lang.Object&java.io.Serializable&java.lang.Comparable<? extends java.lang.Object&java.io.Serializable&java.lang.Comparable<?>>
```

通俗地说，你可以将结果赋给 `Object`、`Serializable` 或 `Comparable`。

**C++ 注：**

在 C++ 中，类型参数放在方法名之后。这可能导致棘手的解析歧义。例如，`g(f<a,b>(c))` 可能表示“用 `f<a,b>(c)` 的结果调用 `g`”，也可能表示“用两个布尔值 `f<a` 和 `b>(c)` 调用 `g`”。

## 8.4 类型变量的限定

有时，类或方法需要对类型变量施加限制。下面是一个典型示例。我们想计算数组中的最小元素：

```java
class ArrayAlg
{
   public static <T> T min(T[] a) // almost correct
   {
      if (a == null || a.length == 0) return null;
      T smallest = a[0];
      for (int i = 1; i < a.length; i++)
         if (smallest.compareTo(a[i]) > 0) smallest = a[i];
      return smallest;
   }
}
```

但这里有一个问题。看看 `min` 方法的代码内部。变量 `smallest` 的类型是 `T`，这意味着它可能是任意类的对象。我们怎么知道 `T` 所属的类有 `compareTo` 方法呢？解决方案是将 `T` 限制为实现 `Comparable` 接口的类——这是一个只包含一个方法 `compareTo` 的标准接口。可以通过为类型变量 `T` 指定一个*限定*来实现：

```java
public static <T extends Comparable> T min(T[] a) . . .
```

实际上，`Comparable` 接口本身就是一个泛型类型。目前，请忽略这种复杂性以及编译器生成的警告。第 475 页的 8.8 节“通配符类型”讨论了如何正确地将类型参数与 `Comparable` 接口一起使用。

现在，泛型 `min` 方法只能使用实现了 `Comparable` 接口的类的数组来调用，例如 `String`、`LocalDate` 等。用 `Rectangle` 数组调用 `min` 会导致编译时错误，因为 `Rectangle` 类没有实现 `Comparable`。

![](img/0e7b74ef51a065c077b42cd87b362288_652_0.png)

**C++ 注：**

在 C++ 中，你不能限制模板参数的类型。如果程序员用不合适的类型实例化模板，模板代码内部会报告一条（通常晦涩的）错误消息。

你可能想知道，在这种情况下为什么我使用 `extends` 关键字而不是 `implements` 关键字——毕竟 Comparable 是一个接口。记法

```java
<T extends BoundingType>
```

表示 T 应当是限定类型的子类型。T 和限定类型都可以是类或接口。选择 `extends` 关键字，是因为它合理地近似了子类型的概念，而且 Java 设计者不想为语言添加新关键字（例如 `sub`）。

一个类型变量或通配符可以有多个限定。例如：

```java
T extends Comparable & Serializable
```

各个限定类型之间用和号（`&`）分隔，因为逗号用于分隔类型变量。

与 Java 继承一样，你可以拥有任意多个接口超类型，但限定中最多只能有一个是类。如果限定中包含类，它必须是限定列表中的第一个。

在下一个示例程序（清单 8.2）中，我们将 `minmax` 方法改写为泛型方法。该方法计算泛型数组的最小值和最大值，并返回一个 `Pair<T>`。

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
      Gets the minimum and maximum of an array of objects of
      type T.
      @param a an array of objects of type T
      @return a pair with the min and max values, or null if a
      is null or empty
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

## 8.5 泛型代码和虚拟机

虚拟机没有泛型类型的对象——所有对象都属于普通类。早期版本的泛型实现甚至能够将使用泛型的程序编译成可在 1.0 虚拟机上执行的类文件！在接下来的几节中，你将看到编译器如何“擦除”类型参数，以及这一过程对 Java 程序员意味着什么。

### 8.5.1 类型擦除

每当你定义泛型类型时，都会自动提供一个相应的*原始*类型。原始类型的名称就是泛型类型的名称去掉类型参数后的名称。类型变量会被*擦除*，并替换为其限定类型（对于没有限定的变量，则替换为 *Object*）。

例如，`Pair<T>` 的原始类型看起来像这样：

```java
public class Pair
{
    private Object first;
    private Object second;

    public Pair(Object first, Object second)
    {
        this.first = first;
        this.second = second;
```

