

关于自动装箱还有其他一些微妙之处。首先，由于包装类引用可以为 null，自动拆箱可能会抛出 `NullPointerException`：

```java
Integer n = null;
System.out.println(2 * n); // throws NullPointerException
```

此外，如果在条件表达式中混合使用 Integer 和 Double 类型，那么 Integer 值会被拆箱，提升为 double，然后装箱为 Double：

```java
Integer n = 1;
Double x = 2.0;
System.out.println(true ? n : x); // prints 1.0
```

最后，我们强调一下，装箱和拆箱是*编译器*的服务，而非虚拟机。编译器在生成类的字节码时插入必要的调用。虚拟机只是执行这些字节码。

你经常看到数字包装类还有另一个原因。Java 的设计者发现包装类是放置某些基本方法的好地方，例如将数字字符串转换为数字的方法。

要将字符串转换为整数，请使用以下语句：

```java
int x = Integer.parseInt(s);
```

这与 Integer 对象无关——parseInt 是一个静态方法。但 Integer 类是放置它的好地方。

API 注释展示了 Integer 类的一些更重要方法。其他数字类实现了相应的方法。

> **警告：** 有些人认为包装类可以用来实现修改数值参数的方法。然而，这是不正确的。回想第 4 章，编写一个递增整数参数的 Java 方法是不可能的，因为 Java 方法的参数总是按值传递。

```java
public static void triple(int x) // won't work
{
    x = 3 * x; // modifies local variable
}
```

我们能否通过使用 Integer 而不是 int 来克服这个问题？

```java
public static void triple(Integer x) // won't work
{
    . . .
}
```

问题在于 Integer 对象是*不可变的*：包装器内部包含的信息无法更改。你不能使用这些包装类来创建修改数值参数的方法。

如果你真的想编写一个方法来更改数值参数，可以使用 org.omg.CORBA 包中定义的*持有者*类型之一：IntHolder、BooleanHolder 等等。每个持有者类型都有一个 public（!）字段 value，你可以通过它访问存储的值。

```java
public static void triple(IntHolder x)
{
    x.value = 3 * x.value;
}
```

- **java.lang.Integer** 1.0
  - `int intValue()`：返回此 Integer 对象的值为 int（覆盖 Number 类中的 intValue 方法）。
  - `static String toString(int i)`：返回一个新的 String 对象，表示以 10 为基数的数字 i。
  - `static String toString(int i, int radix)`：允许你返回以 radix 参数指定的基数表示的数字 i 的表示形式。
  - `static int parseInt(String s)` / `static int parseInt(String s, int radix)`：返回包含在字符串 s 中的数字所表示的整数。对于第一个方法，字符串必须表示以 10 为基数的整数；对于第二个方法，字符串必须表示以 radix 参数给定的基数表示的整数。
  - `static Integer valueOf(String s)` / `static Integer valueOf(String s, int radix)`：返回一个新的 Integer 对象，初始化为包含在字符串 s 中的数字所表示的整数。对于第一个方法，字符串必须表示以 10 为基数的整数；对于第二个方法，字符串必须表示以 radix 参数给定的基数表示的整数。

| `java.text.NumberFormat` 1.1 |
|---|
| • `Number parse(String s)`<br>返回数值，假定指定的 String 表示一个数字。 |

## 5.5 具有可变数量参数的方法

可以提供以可变数量参数调用的方法。（这些有时被称为“varargs”方法。）

你已经见过这样的方法：`printf`。例如，调用

```java
System.out.printf("%d", n);
```

和

```java
System.out.printf("%d %s", n, "widgets");
```

都调用同一个方法，尽管一个调用有两个参数，另一个有三个参数。

`printf` 方法是这样定义的：

```java
public class PrintStream
{
    public PrintStream printf(String fmt, Object... args) { return format(fmt, args); }
}
```

这里，省略号 `...` 是 Java 代码的一部分。它表示该方法可以接收任意数量的对象（除了 `fmt` 参数之外）。

`printf` 方法实际上接收两个参数：格式字符串和一个保存所有其他参数的 `Object[]` 数组。（如果调用者提供整数或其他原始类型值，自动装箱会将它们转换为对象。）现在它面临一项艰巨的任务：扫描 `fmt` 字符串，并将第 i 个格式说明符与 `args[i]` 的值匹配起来。

换句话说，对于 `printf` 的实现者来说，`Object...` 参数类型与 `Object[]` 完全相同。

编译器需要转换每次对 `printf` 的调用，将参数捆绑到一个数组中，并在必要时进行自动装箱：

```java
System.out.printf("%d %s", new Object[] { new Integer(4), "widgets" });
```

你可以定义自己的可变参数方法，并且可以为参数指定任何类型，甚至原始类型。这里有一个简单的例子：一个计算可变数量值最大值的函数。

```java
public static double max(double... values)
{
    double largest = Double.NEGATIVE_INFINITY;
    for (double v : values) if (v > largest) largest = v;
    return largest;
}
```

只需这样调用该函数：

```java
double m = max(3.1, 40.4, -5);
```

编译器将一个新的 double[] { 3.1, 40.4, -5 } 传递给 max 函数。

> **注意：** 将数组作为可变参数方法的最后一个参数传递是合法的。例如：
>
> ```java
> System.out.printf("%d %s", new Object[] { new Integer(1), "widgets" });
> ```

因此，你可以将最后一个参数为数组的现有函数重新定义为可变参数方法，而不会破坏任何现有代码。例如，MessageFormat.format 在 Java 5 中以这种方式得到了增强。如果你愿意，甚至可以将 main 方法声明为

```java
public static void main(String... args)
```

## 5.6 枚举类

你在第 3 章看到了如何定义枚举类型。这是一个典型的例子：

```java
public enum Size { SMALL, MEDIUM, LARGE, EXTRA_LARGE }
```

这个声明定义的类型实际上是一个类。该类恰好有四个实例——不可能构造新对象。

因此，你永远不需要对枚举类型的值使用 equals。只需使用 == 来比较它们即可。

如果你愿意，可以向枚举类型添加构造器、方法和字段。当然，构造器只在构造枚举常量时被调用。这里有一个例子：

```java
public enum Size
{
    SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");

    private String abbreviation;

    private Size(String abbreviation) { this.abbreviation = abbreviation; }
    public String getAbbreviation() { return abbreviation; }
}
```

枚举的构造器总是私有的。你可以省略 private 修饰符，如前面的示例所示。将枚举构造器声明为 public 或 protected 是语法错误。

所有枚举类型都是 `Enum` 类的子类。它们从该类继承了许多方法。最有用的是 `toString`，它返回枚举常量的名称。例如，`Size.SMALL.toString()` 返回字符串 `"SMALL"`。

`toString` 的反向操作是静态 `valueOf` 方法。例如，语句

```java
Size s = Enum.valueOf(Size.class, "SMALL");
```

将 `s` 设置为 `Size.SMALL`。

每个枚举类型都有一个静态 `values` 方法，返回枚举所有值的数组。例如，调用

```java
Size[] values = Size.values();
```

返回包含元素 `Size.SMALL`、`Size.MEDIUM`、`Size.LARGE` 和 `Size.EXTRA_LARGE` 的数组。`ordinal` 方法返回枚举常量在枚举声明中的位置，从零开始计数。例如，`Size.MEDIUM.ordinal()` 返回 1。

清单 5.12 中的简短程序演示了如何使用枚举类型。

> **注意：** 为了简单起见，我们忽略了 `Enum` 类的类型参数。例如，枚举类型 `Size` 实际上继承 `Enum<Size>`。该类型参数在 `compareTo` 方法中使用。（我们将在第 6 章讨论 `compareTo` 方法，在第 8 章讨论类型参数。）

**清单 5.12** `enums/EnumTest.java`

```java
package enums;

import java.util.*;
```

