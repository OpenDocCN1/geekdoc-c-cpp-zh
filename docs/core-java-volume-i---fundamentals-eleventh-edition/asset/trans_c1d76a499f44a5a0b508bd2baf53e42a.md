

| `java.util.Collections` 1.2（续） |
|---|
| - `static void rotate(List<?> l, int d)` 1.4<br>旋转列表中的元素，将索引为 i 的条目移动到位置 (i + d) % l.size()。例如，将列表 [t, a, r] 旋转 2 位得到列表 [a, r, t]。该方法运行时间为 O(n)，其中 n 是列表的长度。<br>- `static int frequency(Collection<?> c, Object o)` 5<br>返回 c 中等于对象 o 的元素数量。<br>- `static boolean disjoint(Collection<?> c1, Collection<?> c2)` 5<br>如果两个集合没有共同元素，则返回 true。 |

| `java.util.Collection<?>` 1.2 |
|---|
| - `default boolean removeIf(Predicate<? super E> filter)` 8<br>移除所有匹配的元素。 |

| `java.util.List<E>` 1.2 |
|---|
| - `default void replaceAll(UnaryOperator<E> op)` 8<br>对该列表的所有元素应用此操作。 |

### 9.6.5 批量操作

有几种操作可以“批量”复制或移除元素。调用

```
coll1.removeAll(coll2);
```

会从 `coll1` 中移除所有存在于 `coll2` 中的元素。反过来，

```
coll1.retainAll(coll2);
```

会从 `coll1` 中移除所有不存在于 `coll2` 中的元素。下面是一个典型应用。

假设你想求两个集合的交集——即两个集合共有的元素。首先，创建一个新集合来保存结果。

```
var result = new HashSet<String>(firstSet);
```

这里，我们利用了这样一个事实：每个集合都有一个构造器，其参数是另一个保存初始化值的集合。

现在，使用 `retainAll` 方法：

```
result.retainAll(secondSet);
```

它会保留同时出现在两个集合中的所有元素。无需编写循环就形成了交集。

你可以进一步推广这个思路，将批量操作应用于一个*视图*。例如，假设你有一个将员工 ID 映射到员工对象的映射，并且你有一个包含所有将要被解雇员工 ID 的集合。

```
Map<String, Employee> staffMap = . . . ;
Set<String> terminatedIDs = . . . ;
```

只需形成键集并移除所有被解雇员工的 ID。

```
staffMap.keySet().removeAll(terminatedIDs);
```

由于键集是映射的一个视图，键及关联的员工姓名会自动从映射中移除。

通过使用子范围视图，你可以将批量操作限制在子列表和子集上。例如，假设你想将列表的前十个元素添加到另一个容器。形成一个子列表来选出前十个元素：

```
relocated.addAll(staff.subList(0, 10));
```

子范围也可以作为修改操作的目标。

```
staff.subList(0, 10).clear();
```

### 9.6.6 在集合与数组之间转换

Java 平台 API 的很大一部分是在集合框架创建之前设计的。因此，你偶尔需要在传统数组和更现代的集合之间进行转换。

如果你有一个需要转换为集合的数组，`List.of` 包装器可以用于此目的。例如：

```
String[] values = . . . ;
var staff = new HashSet<>(List.of(values));
```

从集合获取数组则稍微棘手一些。当然，你可以使用 `toArray` 方法：

```
Object[] values = staff.toArray();
```

但结果是一个*对象*数组。即使你知道你的集合包含特定类型的对象，也不能使用强制类型转换：

```
String[] values = (String[]) staff.toArray(); // ERROR
```

由 `toArray` 方法返回的数组创建为 `Object[]` 数组，你不能改变其类型。相反，使用 `toArray` 方法的一个变体，并向其提供一个你所需类型的长度为 0 的数组。然后返回的数组会创建为*相同的数组类型*：

```
String[] values = staff.toArray(new String[0]);
```

如果你愿意，可以构造一个具有正确大小的数组：

```
staff.toArray(new String[staff.size()]);
```

在这种情况下，不会创建新数组。

> **注意：** 你可能想知道为什么不能简单地将一个 `Class` 对象（例如 `String.class`）传递给 `toArray` 方法。然而，这个方法承担了“双重职责”——既要填充现有数组（前提是它足够长），又要创建新数组。

### 9.6.7 编写自己的算法

如果你编写自己的算法（或者实际上任何以集合为参数的方法），只要可能，就应使用*接口*，而不是具体实现。例如，假设你想处理条目。当然，你可以实现这样的方法：

```
public void processItems(ArrayList<Item> items)
{
    for (Item item : items)
        do something with item
}
```

然而，你现在限制了方法的调用者——调用者必须以 `ArrayList` 提供这些条目。如果这些条目恰好在另一个集合中，它们首先需要被重新包装。接受一个更通用的集合要好得多。

你应该问自己：能完成这项工作的最通用的集合接口是什么？你在乎顺序吗？那么你应该接受 `List`。但如果顺序无关紧要，你可以接受任何类型的集合：

```
public void processItems(Collection<Item> items)
{
    for (Item item : items)
        do something with item
}
```

现在，任何人都可以用 ArrayList 或 LinkedList 调用这个方法，甚至可以用通过 List.of 包装器包装的数组来调用。

> **提示：** 在这种情况下，通过接受 `Iterable<Item>` 可以做得更好。`Iterable` 接口有一个抽象方法 `iterator`，增强 for 循环在幕后使用它。`Collection` 接口扩展了 `Iterable`。

反过来，如果你的方法返回多个元素，你不会希望限制自己未来的改进。例如，考虑

```
public ArrayList<Item> lookupItems(. . .)
{
    var result = new ArrayList<Item>();
    . . .
    return result;
}
```

这个方法承诺返回 ArrayList，尽管调用者几乎肯定不关心它是什么类型的列表。相反，如果你返回 List，你可以随时添加一个分支，通过调用 List.of 返回空列表或单元素列表。

> **注意：** 如果使用集合接口作为参数和返回类型是如此好的做法，为什么 Java 库不始终遵循这一规则？例如，`JComboBox` 类有两个构造器：
>
>     JComboBox(Object[] items)
>     JComboBox(Vector<?> items)
>
> 原因仅仅是时机。Swing 库是在集合库之前创建的。

## 9.7 遗留集合

自 Java 首次发布以来，就存在许多“遗留”容器类，那时还没有集合框架。

如果你发现自己要与遗留类交互，可以使用 `Collections.list` 将元素收集到 `ArrayList` 中。例如，`LogManager` 类只愿意以 `Enumeration` 的形式公开日志记录器名称。以下是你如何获取全部名称：

```
ArrayList<String> loggerNames = Collections.list(LogManager.getLoggerNames());
```

或者，从 Java 9 开始，你可以将枚举转换为迭代器：

```
LogManager.getLoggerNames().iterator().forEachRemaining(n -> { ... });
```

你偶尔会遇到期望枚举参数的遗留方法。静态方法 `Collections.enumeration` 产生一个枚举对象，该对象枚举集合中的元素。例如：

```
List<InputStream> streams = ...;
var in = new SequenceInputStream(Collections.enumeration(streams));
    // the SequenceInputStream constructor expects an enumeration
```

> **注意：** 在 C++ 中，使用迭代器作为参数非常常见。幸运的是，在 Java 平台上，很少有程序员使用这种习惯用法。传递集合比传递迭代器要明智得多。集合对象更有用。接收者可以在需要时随时从集合获取迭代器，而且他们可以随意使用所有集合方法。然而，你会在一些遗留代码中看到枚举，因为在 Java 1.2 集合框架出现之前，它们是通用集合唯一可用的机制。

| `java.util.Enumeration<E>` | 1.0 |
|---|---|
| `boolean hasMoreElements()` | 如果还有更多元素待检查，则返回 true。 |
| `E nextElement()` | 返回下一个要检查的元素。如果 `hasMoreElements()` 返回 false，则不要调用此方法。 |
| `default Iterator<E> asIterator()` | 9<br>产生一个迭代器，用于遍历所枚举的元素。 |

