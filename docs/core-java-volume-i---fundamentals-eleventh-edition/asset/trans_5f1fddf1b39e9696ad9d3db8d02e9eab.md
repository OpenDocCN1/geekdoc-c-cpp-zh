
你从不指定 lambda 表达式的结果类型。它总是从上下文中推断出来。例如，表达式

```java
(String first, String second) -> first.length() - second.length()
```

可以用在期望得到 `int` 类型结果的上下文中。

> **注意：** lambda 表达式在某些分支中返回值而在其他分支中不返回值是非法的。例如，`(int x) -> { if (x > 0) return 1; }` 是无效的。

清单 6.6 中的程序展示了如何将 lambda 表达式用于比较器和动作监听器。

### 清单 6.6 `lambda/LambdaTest.java`

```java
package lambda;

import java.util.*;

import javax.swing.*;
import javax.swing.Timer;

/**
 * This program demonstrates the use of lambda expressions.
 * @version 1.0 2015-05-12
 * @author Cay Horstmann
 */
public class LambdaTest
{
   public static void main(String[] args)
   {
      var planets = new String[] { "Mercury", "Venus", "Earth", "Mars",
         "Jupiter", "Saturn", "Uranus", "Neptune" };
      System.out.println(Arrays.toString(planets));
      System.out.println("Sorted in dictionary order:");
      Arrays.sort(planets);
      System.out.println(Arrays.toString(planets));
      System.out.println("Sorted by length:");
      Arrays.sort(planets, (first, second) -> first.length() - second.length());
      System.out.println(Arrays.toString(planets));

      var timer = new Timer(1000, event ->
         System.out.println("The time is " + new Date()));
      timer.start();
```

```java
var timer = new Timer(1000, event ->
{
    System.out.println("At the tone, the time is "
        + Instant.ofEpochMilli(event.getWhen()));
    Toolkit.getDefaultToolkit().beep();
});
```

这比使用实现 `ActionListener` 接口的类那种替代方案要易读得多。

事实上，在 Java 中，将 lambda 表达式转换为函数式接口是你能对 lambda 表达式做的*唯一*事情。在其他支持函数字面量的编程语言中，你可以声明诸如 `(String, String) -> int` 这样的函数类型，声明这些类型的变量，并使用这些变量来保存函数表达式。然而，Java 设计者决定坚持使用熟悉的接口概念，而不是向语言中添加函数类型。

> **注意：** 你甚至不能将 lambda 表达式赋值给 `Object` 类型的变量——`Object` 不是函数式接口。

Java API 在 `java.util.function` 包中定义了许多非常通用的函数式接口。其中一个接口 `BiFunction<T, U, R>` 描述参数类型为 T 和 U、返回类型为 R 的函数。你可以将我们的字符串比较 lambda 保存在该类型的变量中：

```java
BiFunction<String, String, Integer> comp
    = (first, second) -> first.length() - second.length();
```

然而，这对排序没有帮助。没有哪个 `Arrays.sort` 方法需要 `BiFunction`。如果你以前使用过函数式编程语言，可能会觉得这很奇怪。但对 Java 程序员来说，这很自然。像 `Comparator` 这样的接口有特定用途，而不仅仅是一个具有给定参数和返回类型的方法。当你想用 lambda 表达式做某事时，你仍然需要牢记该表达式的用途，并为其使用特定的函数式接口。

`java.util.function` 包中一个特别有用的接口是 `Predicate`：

```java
public interface Predicate<T>
{
    boolean test(T t);
    // additional default and static methods
}
```

`ArrayList` 类有一个 `removeIf` 方法，其参数是 `Predicate`。它专门设计用于传入 lambda 表达式。例如，下面的语句从数组列表中移除所有 null 值：

```java
list.removeIf(e -> e == null);
```

另一个有用的函数式接口是 `Supplier<T>`：

```java
public interface Supplier<T>
{
   T get();
}
```

供应者没有参数，在被调用时产生一个 T 类型的值。供应者用于惰性求值。例如，考虑以下调用

```java
LocalDate hireday = Objects.requireNonNullElse(day,
   LocalDate.of(1970, 1, 1));
```

这并非最优。我们预期 day 很少为 null，因此只想在必要时构造默认的 `LocalDate`。通过使用供应者，我们可以推迟计算：

```java
LocalDate hireday = Objects.requireNonNullElseGet(day,
   () -> LocalDate.of(1970, 1, 1));
```

`requireNonNullElseGet` 方法仅在需要该值时调用供应者。

## 6.2.4 方法引用

有时，lambda 表达式只涉及一个方法。例如，假设你只想在每次定时器事件发生时打印事件对象。当然，你可以调用

```java
var timer = new Timer(1000, event -> System.out.println(event));
```

如果你能直接把 `println` 方法传递给 `Timer` 构造函数，那就更好了。下面是实现方式：

```java
var timer = new Timer(1000, System.out::println);
```

表达式 `System.out::println` 是一个方法引用。它指示编译器生成一个函数式接口的实例，重写该接口的单个抽象方法来调用给定的方法。在这个例子中，生成一个 `ActionListener`，其 `actionPerformed(ActionEvent e)` 方法调用 `System.out.println(e)`。

> **注意：** 与 lambda 表达式一样，方法引用不是对象。当它被赋值给类型为函数式接口的变量时，才会产生一个对象。

> **注意：** `PrintStream` 类（`System.out` 是它的一个实例）中有十个重载的 `println` 方法。编译器需要根据上下文判断使用哪一个。在我们的例子中，方法引用 `System.out::println` 必须转换为一个具有如下方法的 `ActionListener` 实例
>
> ```java
> void actionPerformed(ActionEvent e)
> ```
>
> 由于 `Object` 与 `ActionEvent` 最匹配，因此从十个重载的 `println` 方法中选择了 `println(Object x)` 方法。当调用 `actionPerformed` 方法时，会打印事件对象。
>
> 现在假设我们将同一个方法引用赋值给另一个不同的函数式接口：
>
> ```java
> Runnable task = System.out::println;
> ```
>
> `Runnable` 函数式接口有一个无参数的单个抽象方法
>
> ```java
> void run()
> ```
>
> 在这种情况下，会选择无参数的 `println()` 方法。调用 `task.run()` 会向 `System.out` 打印一个空行。

再举一个例子，假设你想不区分字母大小写地对字符串排序。你可以传入这个方法表达式：

```java
Arrays.sort(strings, String::compareToIgnoreCase)
```

从这些示例中可以看出，`::` 运算符将方法名与对象名或类名分隔开。有三种变体：

- 1. `object::instanceMethod`
- 2. `Class::instanceMethod`
- 3. `Class::staticMethod`

在第一种变体中，方法引用等价于一个 lambda 表达式，其参数被传递给该方法。对于 `System.out::println`，对象是 `System.out`，方法表达式等价于 `x -> System.out.println(x)`。

在第二种变体中，第一个参数成为该方法的隐式参数。例如，`String::compareToIgnoreCase` 与 `(x, y) -> x.compareToIgnoreCase(y)` 相同。

在第三种变体中，所有参数都被传递给静态方法：`Math::pow` 等价于 `(x, y) -> Math.pow(x, y)`。

表 6.1 带你了解其他示例。

注意，只有当 lambda 表达式的主体调用单个方法且不做其他任何事情时，才能将 lambda 表达式改写为方法引用。考虑这个 lambda 表达式

```
s -> s.length() == 0
```

这里有一个单独的方法调用。但还有一个比较，因此这里不能使用方法引用。

> **注意：** 当有多个同名重载方法时，编译器会尝试从上下文中找出你指的是哪一个。例如，`Math.max` 方法有两个版本，一个用于整数，一个用于 double 值。选择哪一个取决于 `Math::max` 所转换成的函数式接口的方法参数。与 lambda 表达式一样，方法引用并不孤立存在。它们总是被转换为函数式接口的实例。

> **注意：** 有时，API 中包含专门用作方法引用的方法。例如，`Objects` 类有一个 `isNull` 方法，用于测试对象引用是否为 null。乍一看，这似乎没什么用，因为测试 `obj == null` 比 `Objects.isNull(obj)` 更易读。但你可以将方法引用传递给任何带有 `Predicate` 参数的方法。例如，要从列表中移除所有 null 引用，可以调用
>
> ```java
> list.removeIf(Objects::isNull);
> // A bit easier to read than list.removeIf(e -> e == null);
> ```

> **注意：** 带对象的方法引用与其等价的 lambda 表达式之间有细微差别。考虑 `separator::equals` 这样的方法引用。如果 `separator` 为 null，那么形成 `separator::equals` 会立即抛出 `NullPointerException`。而 lambda 表达式 `x -> separator.equals(x)` 只有在被调用时才会抛出 `NullPointerException`。

你可以在方法引用中捕获 `this` 参数。例如，`this::equals` 与 `x -> this.equals(x)` 相同。使用 `super` 也是有效的。方法表达式

```
super::instanceMethod
```
