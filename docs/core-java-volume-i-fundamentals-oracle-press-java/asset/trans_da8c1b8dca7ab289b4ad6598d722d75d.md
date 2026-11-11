
构造器必须与 `new` 结合使用。C++ 程序员常犯的一个错误是忘记 `new` 运算符：

```cpp
Employee number007("James Bond", 100000, 1950, 1, 1); // C++, not Java
```

这在 C++ 中可行，但在 Java 中不可行。

![](img/0e7b74ef51a065c077b42cd87b362288_227_0.png)

### 注意：

注意不要引入与实例字段同名的局部变量。例如，下面的构造器不会设置 name 或 salary 实例字段：

```java
public Employee(String n, double s, . . .)
{
    String name = n; // ERROR
    double salary = s; // ERROR
    . . .
}
```

该构造器声明了*局部变量* `name` 和 `salary`。这些变量只能在构造器内部访问。它们*遮蔽*了同名的实例字段。有些程序员在打字速度快于思考速度时会意外写出这种代码，因为他们的手指习惯了添加数据类型。这是一个棘手的错误，可能很难追踪。你只需在所有方法中都小心，不要使用与实例字段名称相同的变量名。

## 4.3.5 使用 `var` 声明局部变量

从 Java 10 开始，你可以使用 `var` 关键字声明局部变量，而不必指定其类型，前提是类型可以从初始值推断出来。例如，不必声明

```java
Employee harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);
```

只需写

```java
var harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);
```

这很好，因为它避免了重复类型名 `Employee`。

从现在起，在无需了解 Java API、仅从右侧就能明显看出类型的情况下，我将使用 *var* 表示法。但我不会对 `int`、`long` 或 `double` 等数值类型使用 *var*，这样你就不必留意 `0`、`0L` 和 `0.0` 之间的区别。一旦你对 Java API 更有经验，你可能会想更频繁地使用 *var* 关键字。

请注意，*var* 关键字只能用于方法内部的*局部*变量。你必须始终声明参数和字段的类型。

## 4.3.6 处理 null 引用

在[第 4.2.2.1 节](#)“对象与对象变量”（第 132 页）中，你看到对象变量持有对对象的引用，或特殊值 `null` 表示对象不存在。

这听起来像是一种处理特殊情况（例如未知的姓名或雇用日期）的便捷机制。但你需要非常小心 `null` 值。

如果对 `null` 值应用方法，就会发生 `NullPointerException`。

```java
LocalDate rightNow = null;
String s = rightNow.toString(); // NullPointerException
```

这是一个严重错误，类似于“索引越界”异常。如果你的程序没有“捕获”异常，程序就会终止。通常，程序不会捕获这类异常，而是依赖程序员从一开始就不要引发它们。

![](img/0e7b74ef51a065c077b42cd87b362288_229_0.png)

### 提示：

当你的程序因 `NullPointerException` 而终止时，堆栈跟踪会显示问题发生在代码的哪一行。从 Java 17 开始，错误消息会包含值为 null 的变量或方法的名称。例如，在调用

```java
String s = e.getHireDay().toString();
```

时，错误消息会告诉你 `e` 是 null，还是 `getHireDay` 返回了 null。

定义类时，最好明确哪些字段可以为 null。在我们的示例中，我们不希望 name 或 hireDay 字段为 null。（我们不必担心 salary 字段。它具有基本类型，永远不可能为 null。）

hireDay 字段保证非 null，因为它用新的 LocalDate 对象初始化。但是，如果以 null 作为 n 的参数调用构造器，name 将为 null。

有两种解决方案。“宽容”的做法是将 null 参数转换为合适的非 null 值：

```java
if (n == null) name = "unknown"; else name = n;
```

Objects 类为此提供了一个便捷方法：

```java
public Employee(String n, double s, int year, int month, int day)
{
    name = Objects.requireNonNullElse(n, "unknown");
    . . .
}
```

“严厉的爱”做法是拒绝 `null` 参数：

```java
public Employee(String n, double s, int year, int month, int day)
{
    name = Objects.requireNonNull(n, "The name cannot be null");
    . . .
}
```

如果有人用 `null` 名称构造 `Employee` 对象，就会发生 `NullPointerException`。乍一看，这似乎不是有用的补救措施。但有两个优点：

-   异常报告包含对问题的描述。
-   异常报告精确定位问题的位置。否则，`NullPointerException` 会在其他地方发生，且很难追溯回有问题的构造器参数。

> **注意：**
>
> 每当你接受对象引用作为构造参数时，问问自己是否真的打算对可能存在或不存在的值进行建模。如果不是，最好采用“严厉的爱”做法。

## 4.3.7 隐式参数和显式参数

方法对对象进行操作并访问其实例字段。例如，方法

```java
public void raiseSalary(double byPercent)
{
    double raise = salary * byPercent / 100;
    salary += raise;
}
```

会为调用此方法的对象中的 salary 实例字段设置新值。考虑以下调用

```java
number007.raiseSalary(5);
```

其效果是将 `number007.salary` 字段的值增加 5%。更具体地说，该调用执行以下指令：

```java
double raise = number007.salary * 5 / 100;
number007.salary += raise;
```

`raiseSalary` 方法有两个参数。第一个参数称为*隐式*参数，是出现在方法名之前的 Employee 类型对象。第二个参数是方法名后括号内的数字，是*显式*参数。（有些人把隐式参数称为方法调用的*目标*或*接收者*。）

如你所见，显式参数在方法声明中显式列出——例如 `double byPercent`。隐式参数不出现在方法声明中。

在每个方法中，关键字 `this` 都指向隐式参数。如果你愿意，可以按如下方式编写 `raiseSalary` 方法：

```java
public void raiseSalary(double byPercent)
{
    double raise = this.salary * byPercent / 100;
    this.salary += raise;
}
```

有些程序员喜欢这种风格，因为它清楚地区分实例字段和局部变量。

### C++ 注意：

在 C++ 中，通常将方法定义在类外：

```cpp
void Employee::raiseSalary(double byPercent) // C++, not Java
{
    . . .
}
```

如果在类内定义方法，那么它自动就是内联方法。

```cpp
class Employee
{
    . . .
    int getName() { return name; } // inline in C++
}
```

在 Java 中，所有方法都定义在类本身内部。这不会使它们成为内联方法。寻找内联替换机会是 Java 虚拟机的工作。即时编译器会监视对短小、经常调用且未被重写的方法的调用，并将它们优化掉。

## 4.3.8 封装的好处

最后，让我们更仔细地看看相当简单的 getName、getSalary 和 getHireDay 方法。

```java
public String getName()
{
    return name;
}
public double getSalary()
{
    return salary;
}
public LocalDate getHireDay()
{
    return hireDay;
}
```

这些是访问器方法的明显例子。由于它们只是返回实例字段的值，有时被称为*字段访问器*。

把 `name`、`salary` 和 `hireDay` 字段设为 public，而不是使用单独的访问器方法，不是更容易吗？

然而，`name` 字段是只读的。一旦在构造器中设置它，就没有方法可以更改它。因此，我们保证 `name` 字段永远不会被破坏。

`salary` 字段不是只读的，但它只能由 `raiseSalary` 方法更改。特别是，如果该值万一出错，只需要调试那个方法。如果 `salary` 字段是 public，那么搞乱该值的罪魁祸首可能在任何地方。

有时，你希望获取和设置实例字段的值。那么你需要提供*三项*内容：

-   一个私有实例字段；
-   一个 public 字段访问器方法；以及
-   一个 public 字段修改器方法。

这比提供一个 public 实例字段要繁琐得多，但好处相当多。

首先，你可以更改内部实现，而不会影响该类方法之外的任何代码。例如，如果 name 的存储
