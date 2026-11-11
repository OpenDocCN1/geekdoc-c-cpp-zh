

- `default boolean removeIf(Predicate<? super E> filter)` 8 移除所有匹配的元素。

**`java.util.List<E>` 1.2**

- `default void replaceAll(UnaryOperator<E> op)` 8 将操作应用于此列表的所有元素。

### 9.6.5 批量操作

有若干操作可以“批量”复制或移除元素。调用

```java
coll1.removeAll(coll2);
```

将从 `coll1` 中移除所有存在于 `coll2` 中的元素。相反，

```java
coll1.retainAll(coll2);
```

将从 `coll1` 中移除所有*不*存在于 `coll2` 中的元素。下面是一个典型的应用。

假设你想要找出两个集合的*交集*——即两个集合共同拥有的元素。首先，创建一个新的集合来保存结果。

```java
var result = new HashSet<String>(firstSet);
```

这里，我们利用了一个事实：每个集合都有一个构造器，其参数是另一个包含初始化值的集合。

现在，使用 `retainAll` 方法：

```java
result.retainAll(secondSet);
```

它会保留两个集合中都出现的所有元素。这样你就无需编写循环就构造出了交集。

你可以进一步扩展这个思路，将批量操作应用于视图。例如，假设你有一个将员工 ID 映射到员工对象的映射，并且你有一个包含所有将被解雇员工 ID 的集合。

```java
Map<String, Employee> staffMap = . . .;
Set<String> terminatedIDs = . . .;
```

只需构造键集，然后移除所有被解雇员工的 ID。

```java
staffMap.keySet().removeAll(terminatedIDs);
```

由于键集是映射的一个视图，这些键及关联的员工姓名会自动从映射中移除。

通过使用子范围视图，你可以将批量操作限制在子列表和子集上。例如，假设你想将列表的前十个元素添加到另一个容器中。构造一个子列表来选出前十个：

```java
relocated.addAll(staff.subList(0, 10));
```

子范围也可以作为修改操作的目标。

```java
staff.subList(0, 10).clear();
```

### 9.6.6 集合与数组之间的转换

Java 平台 API 的很大一部分是在集合框架出现之前设计的。因此，你偶尔需要在传统数组和更现代的集合之间进行转换。

如果你有一个需要转换为集合的数组，`List.of` 方法可以满足这个需求。例如：

```java
String[] names = . . .;
List<String> staff = List.of(names);
```

从集合中获取数组则要稍微棘手一些。你可以使用 `toArray` 方法：

```java
Object[] names = staff.toArray();
```

但结果是一个*对象*数组。即使你知道你的集合中包含特定类型的对象，你也不能使用强制类型转换：

```java
String[] names = (String[]) staff.toArray(); // ERROR
```

`toArray` 方法返回的数组是以 `Object[]` 数组的形式创建的，你无法改变其类型。相反，你应该向 `toArray` 方法传递一个数组构造器表达式。这样返回的数组就会以*正确的数组类型*创建：

```java
String[] values = staff.toArray(String[]::new);
```

![](img/0e7b74ef51a065c077b42cd87b362288_805_0.png)

**注释：**

在 JDK 11 之前，你必须使用另一种形式的 `toArray` 方法，传入一个正确类型的数组：

```java
String[] values = staff.toArray(new String[0]);
```

这种 `toArray` 方法会构造另一个相同类型的数组。或者，如果数组长度足够，它会被重新使用：

```java
staff.toArray(new String[staff.size()]);
```

**提示：**

在这种情况下，通过接受 `Iterable<Item>` 你可以做得更好。`Iterable` 接口只有一个抽象方法 `iterator`，增强的 `for` 循环在后台使用它。`Collection` 接口扩展了 `Iterable`。

反过来，如果你的方法返回多个元素，你不想限制自己未来的改进。例如，考虑

```java
public ArrayList<Item> lookupItems(. . .)
{
    var result = new ArrayList<Item>();
    . . .
    return result;
}
```

这个方法承诺返回一个 `ArrayList`，尽管调用者几乎肯定不关心它是什么类型的列表。如果你改为返回 `List`，你可以随时通过调用 `List.of` 添加一个返回空列表或单元素列表的分支。

**注释：**

既然使用集合接口作为参数和返回类型是个好主意，为什么 Java 库没有始终遵循这一规则呢？例如，`JComboBox` 类有两个构造器：

```java
JComboBox(Object[] items)
JComboBox(Vector<?> items)
```

原因很简单，就是时机问题。Swing 库是在集合库之前创建的。

## 9.7 遗留集合

自 Java 首次发布以来，在集合框架出现之前，已经存在许多“遗留”容器类。

它们已被整合到集合框架中——参见图 9.12。我将在接下来的小节中简要介绍它们。

![](img/0e7b74ef51a065c077b42cd87b362288_808_0.png)

**图 9.12** 集合框架中的遗留类

### 9.7.1 Hashtable 类

经典的 `Hashtable` 类与 `HashMap` 类的用途相同，并且本质上具有相同的接口。与 `Vector` 类的方法一样，`Hashtable` 的方法是同步的。如果不需要与遗留代码兼容，你应该改用 `HashMap`。如果需要并发访问，请使用 `ConcurrentHashMap`——参见[第12章](#)。

### 9.7.2 枚举

遗留集合使用 `Enumeration` 接口来遍历元素序列。`Enumeration` 接口有两个方法：`hasMoreElements` 和 `nextElement`。它们与 `Iterator` 接口的 `hasNext` 和 `next` 方法完全类似。

如果你在遗留类中遇到这个接口，可以使用 `Collections.list` 将元素收集到 `ArrayList` 中。例如，`LogManager` 类只愿意以 `Enumeration` 的形式公开日志记录器名称。下面是如何获取所有这些名称：

```java
ArrayList<String> loggerNames = Collections.list(LogManager.getLoggerNames());
```

另外，从 Java 9 开始，你可以将枚举转换为迭代器：

```java
LogManager.getLoggerNames().asIterator().forEachRemaining(n -> { ... });
```

你偶尔会遇到一个需要枚举参数的遗留方法。静态方法 `Collections.enumeration` 会生成一个枚举对象，用于枚举集合中的元素。例如：

```java
List<InputStream> streams = ...;
var in = new SequenceInputStream(Collections.enumeration(streams));
// the SequenceInputStream constructor expects an enumeration
```

**注释：**

在 C++ 中，使用迭代器作为参数是非常常见的。幸运的是，在 Java 平台上，很少有程序员使用这种习惯用法。传递集合比传递迭代器要明智得多。集合对象更有用。接收者随时可以在需要时从集合中获取迭代器，而且他们还可以使用所有的集合方法。然而，你会在一些遗留代码中发现枚举，因为在 Java 1.2 中集合框架出现之前，枚举是通用集合唯一可用的机制。

**`java.util.Enumeration<E>` 1.0**

- `boolean hasMoreElements()` 如果还有更多元素待检查，则返回 true。
- `E nextElement()` 返回下一个待检查的元素。如果 `hasMoreElements()` 返回 `false`，则不要调用此方法。
- `default Iterator<E> asIterator()` 9 生成一个迭代器，用于遍历被枚举的元素。

**`java.util.Collections` 1.2**

- `static <T> Enumeration<T> enumeration(Collection<T> c)` 返回一个枚举，用于枚举 c 中的元素。
- `public static <T> ArrayList<T> list(Enumeration<T> e)` 返回一个包含 e 所枚举元素的数组列表。

