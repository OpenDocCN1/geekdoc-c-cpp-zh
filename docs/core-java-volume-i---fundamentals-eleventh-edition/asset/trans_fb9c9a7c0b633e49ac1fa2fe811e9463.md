
下面是你调用它的方式：

```
repeat(10, i -> System.out.println("Countdown: " + (9 - i)));
```

**表6.2 常见函数式接口**

| 函数式接口 | 参数类型 | 返回类型 | 抽象方法名 | 描述 | 其他方法 |
|---|---|---|---|---|---|
| Runnable | 无 | void | run | 运行一个没有参数或返回值的操作 |  |
| `Supplier<T>` | 无 | T | get | 提供一个类型为 T 的值 |  |
| `Consumer<T>` | T | void | accept | 消费一个类型为 T 的值 | andThen |
| `BiConsumer<T, U>` | T, U | void | accept | 消费类型为 T 和 U 的值 | andThen |
| `Function<T, R>` | T | R | apply | 一个参数类型为 T 的函数 | compose, andThen, identity |
| `BiFunction<T, U, R>` | T, U | R | apply | 一个带有类型为 T 和 U 的参数的函数 | andThen |
| `UnaryOperator<T>` | T | T | apply | 对类型 T 的一元运算符 | compose, andThen, identity |
| `BinaryOperator<T>` | T, T | T | apply | 对类型 T 的二元运算符 | andThen, maxBy, minBy |
| `Predicate<T>` | T | boolean | test | 一个返回布尔值的函数 | and, or, negate, isEqual |
| `BiPredicate<T, U>` | T, U | boolean | test | 一个带有两个参数的返回布尔值的函数 | and, or, negate |

表6.3列出了针对基本类型 `int`、`long` 和 `double` 的34个可用特化。正如你将在第8章中看到的，使用这些特化比使用泛型接口更高效。因此，在上一节的示例中，我使用了 `IntConsumer` 而不是 `Consumer<Integer>`。

**表6.3** 基本类型的函数式接口
`p, q` 是 int、long、double；`P, Q` 是 Int、Long、Double

| 函数式接口 | 参数类型 | 返回类型 | 抽象方法名 |
| :--- | :--- | :--- | :--- |
| BooleanSupplier | 无 | boolean | getAsBoolean |
| PSupplier | 无 | P | getAsP |
| PConsumer | P | void | accept |
| `ObjPConsumer<T>` | T, P | void | accept |
| `PFunction<T>` | P | T | apply |
| PToQFunction | P | Q | applyAsQ |
| `ToPFunction<T>` | T | P | applyAsP |
| `ToPBiFunction<T, U>` | T, U | P | applyAsP |
| PUnaryOperator | P | P | applyAsP |
| PBinaryOperator | P, P | P | applyAsP |
| PPredicate | P | boolean | test |

> **提示：** 只要可以，最好使用表6.2或表6.3中的接口。例如，假设你编写一个方法来处理符合某个条件的文件。有一个遗留接口 `java.io.FileFilter`，但最好使用标准的 `Predicate<File>`。不这样做的唯一理由是你已经有许多生成 `FileFilter` 实例的有用方法。

> **注意：** 大多数标准函数式接口都有用于生成或组合函数的非抽象方法。例如，`Predicate.isEqual(a)` 与 `a::equals` 相同，但如果 a 是 `null`，它也能工作。有用于组合谓词的默认方法 `and`、`or`、`negate`。例如，`Predicate.isEqual(a).or(Predicate.isEqual(b))` 与 `x -> a.equals(x) || b.equals(x)` 相同。

> **注意：** 如果你设计自己的接口，并且它只有一个抽象方法，你可以用 `@FunctionalInterface` 注解来标记它。这有两个优点。如果你不小心添加了另一个抽象方法，编译器会给出错误消息。并且 javadoc 页面会包含一条说明，指出你的接口是函数式接口。
>
> 并不要求使用该注解。任何只有一个抽象方法的接口，按定义就是函数式接口。但使用 `@FunctionalInterface` 注解是一个好主意。

### 6.2.8 关于比较器的更多内容

`Comparator` 接口有许多用于创建比较器的便捷静态方法。这些方法旨在与 lambda 表达式或方法引用一起使用。

静态 `comparing` 方法接受一个“键提取器”函数，该函数将类型 `T` 映射到可比较类型（例如 `String`）。该函数应用于要比较的对象，然后对返回的键进行比较。例如，假设你有一个 `Person` 对象数组。下面是如何按姓名对它们排序：

```
Arrays.sort(people, Comparator.comparing(Person::getName));
```

这当然比手动实现 `Comparator` 容易得多。而且，代码更清晰，因为很明显我们想按姓名比较人。

你可以使用 `thenComparing` 方法链接比较器来打破平局。例如，

```
Arrays.sort(people,
        Comparator.comparing(Person::getLastName)
            .thenComparing(Person::getFirstName));
```

如果两个人有相同的姓氏，则使用第二个比较器。

这些方法有几种变体。你可以指定一个比较器，用于 `comparing` 和 `thenComparing` 方法提取的键。例如，这里我们按姓名长度对人排序：

```
Arrays.sort(people, Comparator.comparing(Person::getName,
        (s, t) -> Integer.compare(s.length(), t.length())));
```

此外，`comparing` 和 `thenComparing` 方法都有避免对 `int`、`long` 或 `double` 值进行装箱的变体。产生上述操作的一种更简单方式是

```
    Arrays.sort(people, Comparator.comparingInt(p -> p.getName().length()));
```

如果你的键函数可以返回 `null`，你会喜欢 `nullsFirst` 和 `nullsLast` 适配器。这些静态方法接受一个现有比较器并修改它，使其在遇到 `null` 值时不会抛出异常，而是将它们排为比常规值更小或更大。例如，假设当一个人没有中间名时，`getMiddleName` 返回 `null`。那么你可以使用 `Comparator.comparing(Person::getMiddleName, Comparator.nullsFirst(. . .))`。

`nullsFirst` 方法需要一个比较器——在本例中，是一个比较两个字符串的比较器。`naturalOrder` 方法为任何实现 `Comparable` 的类创建一个比较器。我们需要的是 `Comparator.<String>naturalOrder()`。以下是按可能为 null 的中间名排序的完整调用。我使用了 `java.util.Comparator.*` 的静态导入，以使表达式更易读。注意 `naturalOrder` 的类型是推断出来的。

```
    Arrays.sort(people, comparing(Person::getMiddleName, nullsFirst(naturalOrder())));
```

静态 `reverseOrder` 方法给出自然顺序的逆序。要反转任何比较器，请使用 `reversed` 实例方法。例如，`naturalOrder().reversed()` 与 `reverseOrder()` 相同。

## 6.3 内部类

*内部类*是定义在另一个类内部的类。你为什么要这样做？有两个原因：

- 内部类可以对同一包中的其他类隐藏。
- 内部类方法可以访问定义它们所在作用域中的数据——包括原本会是私有的数据。

内部类过去对于简洁地实现回调非常重要，但如今 lambda 表达式做得更好。尽管如此，内部类对于组织代码仍然非常有用。以下各节将带你了解所有细节。

**C++ 注意：** C++ 有嵌套类。嵌套类包含在外层类的作用域内。下面是一个典型示例：一个链表类定义了一个用于保存链接的类，以及一个用于定义迭代器位置的类。

```cpp
class LinkedList
{
public:
    class Iterator // a nested class
    {
    public:
        void insert(int x);
        int erase();
        ...
    private:
        Link* current;
        LinkedList* owner;
    };
    ...
private:
    Link* head;
    Link* tail;
};
```

嵌套类类似于 Java 中的内部类。然而，Java 内部类有一个额外特性，使它们比 C++ 中的嵌套类更丰富、更有用。来自内部类的对象有一个隐式引用，指向实例化它的外部类对象。通过这个指针，它可以访问外部对象的全部状态。例如，在 Java 中，`Iterator` 类不需要显式指向它所指向的 `LinkedList` 的指针。

在 Java 中，静态内部类没有这个附加指针。它们相当于 C++ 中的嵌套类。

### 6.3.1 使用内部类访问对象状态

内部类的语法相当复杂。因此，我们提供一个简单但有些人为的示例来演示内部类的使用。我们重构 `TimeTest` 示例，并提取一个 `TalkingClock` 类。一个会说话的时钟用两个参数构造：播报之间的间隔，以及一个打开或关闭蜂鸣声的标志。
