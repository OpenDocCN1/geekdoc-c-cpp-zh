

![](img/127bccebb2cfadea3f02579edaad63c3_514_0.png)

**图 9.3** 推进迭代器

```java
Iterator<String> it = c.iterator();
it.next(); // 跳过第一个元素
it.remove(); // 现在移除它
```

更重要的是，`next` 和 `remove` 方法的调用之间存在依赖关系。如果之前没有调用过 `next`，就直接调用 `remove` 是非法的。如果尝试这样做，会抛出 `IllegalStateException`。

如果你想移除两个相邻的元素，不能简单地调用

```java
it.remove();
it.remove(); // 错误
```

相反，你必须先调用 `next` 跳过一个要移除的元素。

```java
it.remove();
it.next();
it.remove(); // 正确
```

### 9.1.4 泛型工具方法

`Collection` 和 `Iterator` 接口是泛型的，这意味着你可以编写操作任何类型集合的工具方法。例如，下面是一个泛型方法，用于测试任意集合是否包含给定元素：

```java
public static <E> boolean contains(Collection<E> c, Object obj)
{
    for (E element : c)
        if (element.equals(obj))
            return true;
    return false;
}
```

Java 库的设计者认为其中一些工具方法非常有用，因此决定在库中提供它们。这样，库的使用者就不必重复造轮子了。`contains` 方法就是这样一个方法。

实际上，`Collection` 接口声明了相当多有用的方法，所有实现类都必须提供这些方法。其中包括

```java
int size()
boolean isEmpty()
boolean contains(Object obj)
boolean containsAll(Collection<?> c)
boolean equals(Object other)
boolean addAll(Collection<? extends E> from)
boolean remove(Object obj)
boolean removeAll(Collection<?> c)
void clear()
boolean retainAll(Collection<?> c)
Object[] toArray()
<T> T[] toArray(T[] arrayToFill)
```

其中许多方法不言自明；你可以在本节末尾的 API 注释中找到完整的文档。

当然，如果每个实现 `Collection` 接口的类都必须提供这么多例程方法，那将是一件麻烦事。为了让实现者的生活更轻松，库提供了一个 `AbstractCollection` 类，它将基本方法 `size` 和 `iterator` 保持为抽象，但根据它们实现了例程方法。例如：

```java
public abstract class AbstractCollection<E>
    implements Collection<E>
{
    . . .
    public abstract Iterator<E> iterator();

    public boolean contains(Object obj)
    {
        for (E element : this) // 调用 iterator()
            if (element.equals(obj))
                return true;
        return false;
    }
    . . .
}
```

现在，一个具体的集合类可以扩展 `AbstractCollection` 类。具体的集合类需要提供 `iterator` 方法，而 `contains` 方法已经由 `AbstractCollection` 超类处理了。但是，如果子类有更有效的方法来实现 `contains`，它可以自由地这样做。

这种方法有点过时了。如果这些方法是 `Collection` 接口的默认方法会更好。但事实并非如此。不过，已经添加了几个默认方法。其中大多数涉及流（我们将在第二卷中讨论）。此外，还有一个有用的方法

```java
default boolean removeIf(Predicate<? super E> filter)
```

用于移除满足条件的元素。

**`java.util.Collection<E>` 1.2**

- `Iterator<E> iterator()`  
  返回一个可用于访问集合中元素的迭代器。
- `int size()`  
  返回集合中当前存储的元素数量。
- `boolean isEmpty()`  
  如果此集合不包含任何元素，则返回 `true`。
- `boolean contains(Object obj)`  
  如果此集合包含与 `obj` 相等的对象，则返回 `true`。

**`java.util.Collection<E>` 1.2（续）**

| 方法 | 说明 |
|---|---|
| `boolean containsAll(Collection<?> other)` | 如果此集合包含另一个集合中的所有元素，则返回 `true`。 |
| `boolean add(E element)` | 向集合中添加一个元素。如果此调用导致集合发生更改，则返回 `true`。 |
| `boolean addAll(Collection<? extends E> other)` | 将另一个集合中的所有元素添加到此集合中。如果此调用导致集合发生更改，则返回 `true`。 |
| `boolean remove(Object obj)` | 从此集合中移除与 `obj` 相等的对象。如果移除了匹配的对象，则返回 `true`。 |
| `boolean removeAll(Collection<?> other)` | 从此集合中移除另一个集合中的所有元素。如果此调用导致集合发生更改，则返回 `true`。 |
| `default boolean removeIf(Predicate<? super E> filter)` | 移除所有 `filter` 返回 `true` 的元素。如果此调用导致集合发生更改，则返回 `true`。 |
| `void clear()` | 从此集合中移除所有元素。 |
| `boolean retainAll(Collection<?> other)` | 从此集合中移除所有与另一个集合中的元素不相等的元素。如果此调用导致集合发生更改，则返回 `true`。 |
| `Object[] toArray()` | 返回集合中对象的数组。 |
| `<T> T[] toArray(T[] arrayToFill)` | 返回集合中对象的数组。如果 `arrayToFill` 长度足够，则用此集合的元素填充它。如果有剩余空间，则追加一个 `null` 元素。否则，会分配并填充一个与 `arrayToFill` 组件类型相同、长度与此集合大小相同的新数组。 |

**`java.util.Iterator<E>` 1.2**

| 方法 | 说明 |
|---|---|
| `boolean hasNext()` | 如果还有另一个元素要访问，则返回 `true`。 |
| `E next()` | 返回下一个要访问的对象。如果已达到集合末尾，则抛出 `NoSuchElementException`。 |
| `void remove()` | 移除最后访问的对象。此方法必须紧跟元素访问之后调用。如果自上次元素访问以来集合已被修改，则此方法抛出 `IllegalStateException`。 |
| `default void forEachRemaining(Consumer<? super E> action)` | 访问元素并将它们传递给给定操作，直到没有剩余元素或操作抛出异常为止。 |

## 9.2 集合框架中的接口

Java 集合框架为不同类型的集合定义了许多接口，如图 9.4 所示。

集合有两个基本接口：`Collection` 和 `Map`。如你所见，你可以通过以下方法将元素插入集合：

```java
boolean add(E element)
```

然而，映射保存键/值对，你使用 `put` 方法插入它们：

```java
V put(K key, V value)
```

要从集合中读取元素，请使用迭代器访问它们。但是，你可以使用 `get` 方法从映射中读取值：

```java
V get(K key)
```

列表是一种*有序集合*。元素被添加到容器中的特定位置。可以通过两种方式访问元素：通过迭代器或通过整数索引。后者称为*随机访问*，因为可以按任意顺序访问元素。相反，使用迭代器时，必须按顺序访问它们。

![](img/127bccebb2cfadea3f02579edaad63c3_519_0.png)

**图 9.4** 集合框架的接口

`List` 接口定义了几个用于随机访问的方法：

```java
void add(int index, E element)
void remove(int index)
E get(int index)
E set(int index, E element)
```

`ListIterator` 接口是 `Iterator` 的子接口。它定义了一个用于在迭代器位置之前添加元素的方法：

```java
void add(E element)
```

坦率地说，集合框架的这一方面设计得很差。在实践中，有两种有序集合，它们的性能权衡差异很大。由数组支持的有序集合具有快速的随机访问能力，因此使用带有整数索引的 `List` 方法是有意义的。相比之下，链表虽然也是有序的，但随机访问速度较慢，最好使用迭代器进行遍历。提供两个接口本来是一件容易的事。

> **注意：** 为避免对链表执行随机访问操作，Java 1.4 引入了一个标记接口 `RandomAccess`。该接口没有方法，但你可以使用它来测试特定集合是否支持高效的随机访问：
> 
> ```java
> if (c instanceof RandomAccess)
> {
>     使用随机访问算法
> }
> else
> {
>     使用顺序访问算法
> }
> ```

`Set` 接口与 `Collection` 接口相同，但方法的行为定义得更严格。`set` 的 `add` 方法应拒绝重复项。`set` 的 `equals` 方法应这样定义：如果两个集合具有相同的元素，则它们是相同的，但不一定顺序相同。`hashCode` 方法应这样定义：具有相同元素的两个集合产生相同的哈希码。

如果方法签名相同，为什么还要单独定义一个接口？从概念上讲，并非所有集合都是集。制作 `Set` 接口使程序员能够编写只接受集的方法。

`SortedSet` 和 `SortedMap` 接口公开了用于排序的比较器对象，并定义了获取集合子集视图的方法。我们将在第 532 页的 9.5 节“视图和包装器”中讨论这些内容。

最后，Java 6 引入了 `NavigableSet` 和 `NavigableMap` 接口，它们包含用于在有序集和映射中进行搜索和遍历的额外方法。（理想情况下，这些方法应该直接包含在 `SortedSet` 和 `SortedMap` 接口中。）`TreeSet` 和 `TreeMap` 类实现了这些接口。

## 9.3 具体集合

表 9.1 显示了 Java 库中的集合，并简要描述了每个集合类的用途。（为简单起见，我们省略了线程安全的

