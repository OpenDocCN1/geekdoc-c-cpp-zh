
对于 `Map` 接口，无法提供可变参数版本，因为参数类型在键类型和值类型之间交替。有一个静态方法 `ofEntries`，它接受任意数量的 `Map.Entry<K, V>` 对象，你可以用静态方法 `entry` 创建这些对象。例如，

```java
import static java.util.Map.*;
...
Map<String, Integer> scores = ofEntries(
    entry("Peter", 2),
    entry("Paul", 3),
    entry("Mary", 5));
```

`of` 和 `ofEntries` 方法生成的对象所属的类，会为每个元素提供一个实例变量，或者底层由数组支持。

这些集合对象是*不可修改的*。任何修改其内容的尝试都会导致 `UnsupportedOperationException`。

如果你想要一个可变集合，可以将不可修改集合传给构造器：

```java
var names = new ArrayList<>(List.of("Peter", "Paul", "Mary"));
```

方法调用

```java
Collections.nCopies(n, anObject)
```

返回一个不可变对象，该对象实现 `List` 接口，并造成一种包含 n 个元素的假象，其中每个元素都显示为 `anObject`。

例如，以下调用创建一个包含 100 个字符串的 List，全部设为 "DEFAULT"：

```java
List<String> settings = Collections.nCopies(100, "DEFAULT");
```

存储开销非常小——该对象只存储一次。

> **注意：** `of` 方法是在 Java 9 中引入的。以前有一个静态 `Arrays.asList` 方法，返回一个可变但不可调整大小的列表。也就是说，你可以调用 `set`，但不能在列表上添加或删除。还有遗留方法 `Collections.emptySet` 和 `Collections.singleton`。

> **注意：** `Collections` 类包含许多实用方法，其参数或返回值是集合。不要将其与 `Collection` 接口混淆。

> **提示：** Java 没有 Pair 类，一些程序员使用 `Map.Entry` 作为简陋的配对。在 Java 9 之前，这很痛苦——你必须构造一个新的 `AbstractMap.SimpleImmutableEntry<>(first, second)`。如今，你可以调用 `Map.entry(first, second)`。

## 9.5.2 子范围

你可以为许多集合形成子范围视图。例如，假设你有一个列表 staff，并且想提取元素 10 到 19。使用 sublist 方法获取该列表子范围的视图：

```java
List<Employee> group2 = staff.subList(10, 20);
```

第一个索引包含在内，第二个索引不包含——就像 String 类的 substring 操作的参数一样。

你可以对子范围应用任何操作，它们会自动反映整个列表。例如，你可以清除整个子范围：

```java
group2.clear(); // staff reduction
```

这些元素会自动从 staff 列表中清除，并且 group2 变为空。

对于排序集和映射，你使用排序顺序，而不是元素位置，来形成子范围。SortedSet 接口声明了三个方法：

```java
SortedSet<E> subSet(E from, E to)
SortedSet<E> headSet(E to)
SortedSet<E> tailSet(E from)
```

这些方法返回所有大于等于 from 且严格小于 to 的元素的子集。对于排序映射，类似的方法

```java
SortedMap<K, V> subMap(K from, K to)
SortedMap<K, V> headMap(K to)
SortedMap<K, V> tailMap(K from)
```

返回映射的视图，其中包含键落在指定范围内的所有条目。

Java 6 引入的 NavigableSet 接口对这些子范围操作提供了更多控制。你可以指定边界是否包含：

```java
NavigableSet<E> subSet(E from, boolean fromInclusive, E to, boolean toInclusive)
NavigableSet<E> headSet(E to, boolean toInclusive)
NavigableSet<E> tailSet(E from, boolean fromInclusive)
```

## 9.5.3 不可修改视图

Collections 类有一些方法，可以生成集合的*不可修改视图*。这些视图会向现有集合添加运行时检查。如果检测到修改集合的尝试，就会抛出异常，并且集合保持不变。

你可以通过八个方法获得不可修改视图：

- `Collections.unmodifiableCollection`
- `Collections.unmodifiableList`
- `Collections.unmodifiableSet`
- `Collections.unmodifiableSortedSet`
- `Collections.unmodifiableNavigableSet`
- `Collections.unmodifiableMap`
- `Collections.unmodifiableSortedMap`
- `Collections.unmodifiableNavigableMap`

每个方法都定义为作用于一个接口。例如，`Collections.unmodifiableList` 可用于 `ArrayList`、`LinkedList` 或任何其他实现 `List` 接口的类。

例如，假设你想让代码的某一部分查看但不能修改集合的内容。你可以这样做：

```java
var staff = new LinkedList<String>();
...
lookAt(Collections.unmodifiableList(staff));
```

`Collections.unmodifiableList` 方法返回一个实现 `List` 接口的类的对象。其访问器方法从 `staff` 集合中检索值。当然，`lookAt` 方法可以调用 `List` 接口的所有方法，而不仅是访问器。但所有修改器方法（如 `add`）都已被重新定义为抛出 `UnsupportedOperationException`，而不是将调用转发给底层集合。

不可修改视图并不会使集合本身不可变。你仍然可以通过其原始引用（在本例中是 `staff`）修改集合。并且你仍然可以对集合的元素调用修改器方法。

这些视图包装的是*接口*，而不是实际的集合对象，因此你只能访问接口中定义的方法。例如，`LinkedList` 类有便利方法 `addFirst` 和 `addLast`，它们不是 `List` 接口的一部分。这些方法无法通过不可修改视图访问。

> **警告：** `unmodifiableCollection` 方法（以及本节后面讨论的 `synchronizedCollection` 和 `checkedCollection` 方法）返回的集合，其 `equals` 方法**不会**调用底层集合的 `equals` 方法。相反，它继承 `Object` 类的 `equals` 方法，该方法只测试对象是否相同。如果你把一个集或列表只当作集合来使用，就无法再测试内容是否相等。视图之所以这样处理，是因为在这一层次结构级别上，相等性测试没有明确定义。视图对 `hashCode` 方法也采用同样的方式。
>
> 但是，`unmodifiableSet` 和 `unmodifiableList` 方法使用底层集合的 `equals` 和 `hashCode` 方法。

## 9.5.4 同步视图

如果你从多个线程访问集合，就需要确保集合不会被意外损坏。例如，如果一个线程试图修改哈希表，而另一个线程正在重新哈希元素，那将是灾难性的。

库设计者没有实现线程安全的集合类，而是使用视图机制使常规集合线程安全。例如，`Collections` 类中的静态 `synchronizedMap` 方法可以将任何映射转换为具有同步访问方法的 `Map`：

```java
var map = Collections.synchronizedMap(new HashMap<String, Employee>());
```

现在你可以从多个线程访问该映射对象。诸如 get 和 put 之类的方法已同步——每次方法调用必须完全完成后，另一个线程才能调用另一个方法。我们将在第 12 章更详细地讨论数据结构的同步访问问题。

## 9.5.5 检查视图

检查视图旨在为泛型类型可能出现的问题提供调试支持。如第 8 章所述，实际上可以将错误类型的元素偷偷放入泛型集合。例如：

```java
var strings = new ArrayList<String>();
ArrayList rawList = strings; // warning only, not an error,
                             // for compatibility with legacy code
rawList.add(new Date()); // now strings contains a Date object!
```

错误的 add 命令不会在运行时被检测到。相反，稍后代码的另一部分调用 get 并将结果强制转换为 String 时，会发生类强制转换异常。
