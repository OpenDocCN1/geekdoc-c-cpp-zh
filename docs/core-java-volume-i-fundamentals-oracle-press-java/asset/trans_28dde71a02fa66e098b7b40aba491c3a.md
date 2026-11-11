

然后，Employee 类只需扩展这个抽象类并提供 `compareTo` 方法：

```java
class Employee extends Comparable // why not?
{
    public int compareTo(Object other) { . . . }
}
```

不幸的是，使用抽象基类来表达通用属性存在一个重大问题。一个类只能扩展一个类。假设 Employee 类已经扩展了另一个类，比如 Person。那么它就不能再扩展第二个类。

```java
class Employee extends Person, Comparable // ERROR
```

但是每个类可以实现任意多个接口：

```java
class Employee extends Person implements Comparable // OK
```

其他编程语言，特别是 C++，允许一个类拥有多个超类。这一特性称为*多重继承*。Java 的设计者选择不支持多重继承，因为这会使语言要么非常复杂（如 C++），要么效率较低（如 Eiffel）。

相反，接口提供了多重继承的大部分好处，同时避免了复杂性和低效率。

![](img/0e7b74ef51a065c077b42cd87b362288_468_0.png)

> **C++ 附注：**
>
> C++ 具有多重继承以及随之而来的所有复杂性，例如虚基类、支配规则和横向指针转换。很少有 C++ 程序员使用多重继承，有些人说永远不应使用它。其他程序员建议仅将多重继承用于“混入”式继承。在混入风格中，一个主基类描述父对象，而附加基类（所谓的混入）可以提供辅助特性。这种风格类似于具有单个超类和附加接口的 Java 类。

> **提示：**
>
> 你已经在第 3 章见过 `CharSequence` 接口。`String` 和 `StringBuilder`（以及一些更少见的类字符串类）都实现了这个接口。该接口包含所有管理字符序列的类共有的方法。一个公共接口鼓励程序员编写使用 `CharSequence` 接口的方法。这些方法可用于 `String`、`StringBuilder` 以及其他类字符串类的实例。
>
> 遗憾的是，`CharSequence` 接口相当贫乏。你可以获取长度、遍历码点或代码单元、提取子序列，并按字典顺序比较两个序列。Java 17 增加了一个 `isEmpty` 方法。
>
> 如果你处理字符串，并且这些操作足以完成你的任务，那么应接受 `CharSequence` 实例而不是字符串。

### 6.1.4 静态方法与私有方法

从 Java 8 开始，允许向接口添加静态方法。从来没有什么技术理由禁止这样做。它只是看起来违背了接口作为抽象规范的精神。

到目前为止，将静态方法放在伴生类中一直很常见。在标准库中，你会发现成对的接口和工具类，例如 `Collection`/`Collections` 或 `Path`/`Paths`。

你可以从 URI 或从一系列字符串构造指向文件或目录的路径，例如 `Paths.get("jdk-17", "conf", "security")`。在 Java 11 中，`Path` 接口提供了等价的方法：

```java
public interface Path
{
    public static Path of(URI uri) { . . . }
    public static Path of(String first, String... more) { . . . }
    . . .
}
```

这样一来，Paths 类就不再必要了。

同样，当你实现自己的接口时，也不再需要为工具方法提供单独的伴生类。

从 Java 9 开始，接口中的方法可以是私有的。私有方法可以是静态方法或实例方法。由于私有方法只能在接口自身的方法中使用，因此它们的用途仅限于作为接口其他方法的辅助方法。

### 6.1.5 默认方法

你可以为任何接口方法提供*默认*实现。必须用 default 修饰符标记这样的方法。

```java
public interface Comparable<T>
{
    default int compareTo(T other) { return 0; }
        // by default, all elements are the same
}
```

当然，这并不十分有用，因为每个现实的 Comparable 实现都会覆盖此方法。但在其他情况下，默认方法可能有用。例如，在第 9 章中，你将看到一个用于访问数据结构中元素的 Iterator 接口。它声明了一个 remove 方法，如下所示：

```java
public interface Iterator<E>
{
    boolean hasNext();
    E next();
    default void remove() { throw new UnsupportedOperationException("remove"); }
    ...
}
```

如果实现迭代器，你需要提供 `hasNext` 和 `next` 方法。这些方法没有默认实现——它们取决于你正在遍历的数据结构。但如果你的迭代器是只读的，就不必担心 remove 方法。

默认方法可以调用其他方法。例如，`Collection` 接口可以定义一个便捷方法

```java
public interface Collection
{
    int size(); // an abstract method
    default boolean isEmpty() { return size() == 0; }
    ...
}
```

这样，实现 `Collection` 的程序员就不必担心实现 `isEmpty` 方法。

> **注意：**
>
> Java API 中的 `Collection` 接口实际上并没有这样做。相反，有一个 `AbstractCollection` 类实现了 `Collection`，并根据 `size` 定义 `isEmpty`。建议集合的实现者扩展 `AbstractCollection`。该技术已经过时。只需在接口中实现这些方法即可。

默认方法的一个重要用途是*接口演进*。例如，考虑多年来一直是 Java 一部分的 Collection 接口。假设很久以前，你提供了一个类

```java
interface Person
{
    default String getName() { return ""; }
}
interface Named
{
    default String getName() { return getClass().getName() + "_" + hashCode(); }
}
```

如果你形成一个同时实现这两个接口的类，会发生什么？

```java
class Student implements Person, Named { . . . }
```

该类继承了 Person 和 Named 接口提供的两个不一致的 getName 方法。Java 编译器不会选择其中一个，而是报告错误，并让程序员来解决歧义。只需在 Student 类中提供一个 getName 方法。在该方法中，你可以选择两个冲突方法之一，如下所示：

```java
class Student implements Person, Named
{
    public String getName() { return Person.super.getName(); }
    . . .
}
```

现在假设 Named 接口没有为 getName 提供默认实现：

```java
interface Named
{
    String getName();
}
```

Student 类能否从 Person 接口继承默认方法？这或许是合理的，但 Java 设计者决定采用统一性。两个接口如何冲突并不重要。如果至少有一个接口提供了实现，编译器就会报告错误，程序员必须解决歧义。

![](img/0e7b74ef51a065c077b42cd87b362288_474_0.png)

> **注意：**
>
> 当然，如果两个接口都没有为共享方法提供默认实现，那么我们就处于 Java 8 之前的情形，不存在冲突。实现类有两种选择：实现该方法，或者不实现它。在后一种情况下，该类本身是抽象的。

我们刚刚讨论了两个接口之间的名称冲突。现在考虑一个类，它扩展一个超类并实现一个接口，同时从两者继承相同的方法。例如，假设 `Person` 是一个类，而 `Student` 定义为

```java
class Student extends Person implements Named { ... }
```

在这种情况下，只有超类方法起作用，接口中的任何默认方法都会被直接忽略。在我们的示例中，Student 从 Person 继承 `getName` 方法，而 `Named` 接口是否为 `getName` 提供默认实现没有任何区别。这就是“类优先”规则。

“类优先”规则确保与 Java 7 的兼容性。如果你向接口添加默认方法，它对默认方法出现之前可以正常工作的代码没有影响。

![](img/0e7b74ef51a065c077b42cd87b362288_474_1.png)

> **警告：**
>
> 你永远不能创建重新定义 `Object` 类中某个方法的默认方法。例如，你不能为 `toString` 或 equals 定义默认方法，即使这对这样的接口可能很有吸引力

