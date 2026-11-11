
## 表 6.1 方法引用示例

| 方法引用 | 等价的 Lambda 表达式 | 说明 |
|---|---|---|
| `separator::equals` | `x -> separator.equals(x)` | 这是一个带有对象和实例方法的方法表达式。lambda 参数作为该方法的显式参数传入。 |
| `String::trim` | `x -> x.trim()` | 这是一个带有类和实例方法的方法表达式。lambda 参数成为隐式参数。 |
| `String::concat` | `(x, y) -> x.concat(y)` | 同样，这里有一个实例方法，但这次带有一个显式参数。和之前一样，第一个 lambda 参数成为隐式参数，其余参数传给该方法。 |
| `Integer.valueOf` | `x -> Integer.valueOf(x)` | 这是一个带有静态方法的方法表达式。lambda 参数传给该静态方法。 |
| `Integer.sum` | `(x, y) -> Integer.sum(x, y)` | 这是另一个静态方法，但这次带有两个参数。两个 lambda 参数都传给该静态方法。`Integer.sum` 方法就是专门为用作方法引用而创建的。如果写成 lambda，你只需写 `(x, y) -> x + y`。 |
| `Integer::new` | `x -> new Integer(x)` | 这是一个构造器引用——见 6.2.5 节。lambda 参数传给该构造器。 |
| `Integer[]::new` | `n -> new Integer[n]` | 这是一个数组构造器引用——见 6.2.5 节。lambda 参数是数组长度。 |

使用 this 作为目标，并调用给定方法的超类版本。下面是一个展示其机制的人为示例：

```java
class Greeter
{
    public void greet(ActionEvent event)
    {
        System.out.println("Hello, the time is "
            + Instant.ofEpochMilli(event.getWhen()));
    }
}
```

```java
class RepeatedGreeter extends Greeter
{
    public void greet(ActionEvent event)
    {
        var timer = new Timer(1000, super::greet);
        timer.start();
    }
}
```

当 RepeatedGreeter.greet 方法启动时，会构造一个 Timer，它在每个计时器 tick 上执行 super::greet 方法。

### 6.2.5 构造器引用

构造器引用与方法引用类似，只不过方法名是 new。例如，Person::new 是对某个 Person 构造器的引用。是哪个构造器？这取决于上下文。假设你有一个字符串列表。然后你可以通过对每个字符串调用构造器，将它转换为 Person 对象数组，调用方式如下：

```java
ArrayList<String> names = ...;
Stream<Person> stream = names.stream().map(Person::new);
List<Person> people = stream.collect(Collectors.toList());
```

我们将在第二卷第一章讨论流、map 和 collect 方法的细节。目前重要的是，map 方法会为每个列表元素调用 Person(String) 构造器。如果有多个 Person 构造器，编译器会选择带有 String 参数的那个，因为它从上下文中推断出该构造器是用字符串调用的。

你可以用数组类型构成构造器引用。例如，int[]::new 是一个带有一个参数的构造器引用：数组的长度。它等价于 lambda 表达式 x -> new int[x]。

数组构造器引用有助于克服 Java 的一个限制。无法构造泛型类型 T 的数组。表达式 new T[n] 是错误的，因为它会被擦除为 new Object[n]。这对库来说是一个问题。

在我们的例子中，lambda 表达式有一个自由变量 `text`。表示该 lambda 表达式的数据结构必须存储自由变量的值——在我们的例子中，就是字符串 `"Hello"`。我们说这些值已被 lambda 表达式捕获。（具体如何做到是实现的细节。例如，可以将 lambda 表达式转换为一个带有单个方法的对象，这样自由变量的值就被复制到该对象的实例变量中。）

> **注意：** 代码块连同自由变量值的技术术语是 *闭包*。如果有人吹嘘自己的语言有闭包，请放心，Java 也有。在 Java 中，lambda 表达式就是闭包。

如你所见，lambda 表达式可以捕获外围作用域中某个变量的值。在 Java 中，为了确保捕获的值定义明确，有一个重要限制。在 lambda 表达式中，你只能引用值不会改变的变量。例如，下面这样是非法的：

```java
public static void countDown(int start, int delay)
{
    ActionListener listener = event ->
    {
        start--; // ERROR: Can't mutate captured variable
        System.out.println(start);
    };
    new Timer(delay, listener).start();
}
```

这个限制是有原因的。当多个动作并发执行时，修改 lambda 表达式中的变量是不安全的。对于到目前为止我们见过的那些动作，这不会发生，但一般来说，这是一个严重的问题。关于这个重要问题的更多信息，请参见第 12 章。

在 lambda 表达式中引用一个在外部被修改的变量也是非法的。例如，下面这样是非法的：

```java
public static void repeat(String text, int count)
{
    for (int i = 1; i <= count; i++)
    {
        ActionListener listener = event ->
        {
            System.out.println(i + " " + text);
            // ERROR: Cannot refer to changing i
        };
        new Timer(1000, listener).start();
    }
}
```

规则是：lambda 表达式中的任何被捕获变量都必须是 *事实上的最终变量*。事实上的最终变量是指初始化后从未被赋予新值的变量。在我们的例子中，text 始终引用同一个 String 对象，因此捕获它是可以的。然而，i 的值会被修改，因此 i 不能被捕获。

lambda 表达式的主体具有 *与嵌套块相同的作用域*。名称冲突和遮蔽的规则同样适用。在 lambda 中声明与某个局部变量同名的参数或局部变量是非法的。

```java
Path first = Path.of("/usr/bin");
Comparator<String> comp
   = (first, second) -> first.length() - second.length();
// ERROR: Variable first already defined
```

在一个方法内，不能有两个同名的局部变量，因此也不能在 lambda 表达式中引入这样的变量。当你在 lambda 表达式中使用 this 关键字时，你指的是创建该 lambda 的方法的 this 参数。例如，考虑

```java
public class Application
{
   public void init()
   {
      ActionListener listener = event ->
         {
            System.out.println(this.toString());
            ...
         };
      ...
   }
}
```

表达式 this.toString() 调用的是 Application 对象的 toString 方法，*而不是* ActionListener 实例的方法。在 lambda 表达式中使用 this 并没有什么特别之处。lambda 表达式的作用域嵌套在 init 方法内部，而 this 在该方法的任何位置都具有相同含义。

### 6.2.7 处理 Lambda 表达式

到目前为止，你已经看到如何生成 lambda 表达式，并将它们传给期望函数式接口的方法。现在让我们看看如何编写能够使用 lambda 表达式的方法。

使用 lambda 的重点是 *延迟执行*。毕竟，如果你想现在执行某些代码，直接执行即可，而不必把它包在 lambda 里。稍后执行代码有很多原因，例如：

- 在单独的线程中运行代码
- 多次运行代码
- 在算法中的正确时点运行代码（例如排序中的比较操作）
- 在发生某事时运行代码（按钮被点击、数据到达等）
- 仅在必要时运行代码

让我们看一个简单的例子。假设你想将某个动作重复 n 次。该动作和次数被传给 repeat 方法：

```java
repeat(10, () -> System.out.println("Hello, World!"));
```

为了接收这个 lambda，我们需要选择一个（或在少数情况下提供）函数式接口。表 6.2 列出了 Java API 中提供的最重要的函数式接口。在这种情况下，我们可以使用 Runnable 接口：

```java
public static void repeat(int n, Runnable action)
{
    for (int i = 0; i < n; i++) action.run();
}
```

注意，lambda 表达式的主体在调用 action.run() 时执行。

现在让这个例子稍微复杂一些。我们想告诉该动作它发生在哪次迭代中。为此，我们需要选择一个函数式接口，它有一个带 int 参数且返回 void 的方法。处理 int 值的标准接口是

```java
public interface IntConsumer
{
    void accept(int value);
}
```

下面是 repeat 方法的改进版本：

```java
public static void repeat(int n, IntConsumer action)
{
    for (int i = 0; i < n; i++) action.accept(i);
}
```
