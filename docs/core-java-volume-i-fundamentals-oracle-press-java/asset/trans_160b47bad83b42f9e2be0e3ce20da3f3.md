
Java 类库中集合类的基本接口是 `Collection` 接口。该接口有两个基本方法：

```java
public interface Collection<E>
{
    boolean add(E element);
    Iterator<E> iterator();
    . . .
}
```

除了这两个方法之外，还有几个方法；我们稍后讨论它们。

add 方法向集合中添加一个元素。如果添加元素确实改变了集合，add 方法返回 true；如果集合未改变，则返回 false。例如，如果你试图向一个集（set）中添加一个对象，而该对象已经存在，那么添加请求不会产生任何效果，因为集会拒绝重复项。

`iterator` 方法返回一个实现了 `Iterator` 接口的对象。你可以使用迭代器对象逐个访问集合中的元素。我们将在下一节讨论迭代器。

### 9.1.3 迭代器

`Iterator` 接口有四个方法：

```java
public interface Iterator<E>
{
    E next();
    boolean hasNext();
    void remove();
    default void forEachRemaining(Consumer<? super E> action);
}
```

通过反复调用 next 方法，你可以逐个访问集合中的元素。然而，如果到达集合末尾，`next` 方法会抛出 `NoSuchElementException`。因此，在调用 `next` 之前需要调用 `hasNext` 方法。如果迭代器对象还有更多元素要访问，该方法返回 `true`。如果你想检查集合中的所有元素，可以请求一个迭代器，然后在 `hasNext` 返回 `true` 时持续调用 `next` 方法。例如：

```java
Collection<String> c = . . .;
Iterator<String> iter = c.iterator();
while (iter.hasNext())
{
    String element = iter.next();
    do something with element
}
```

你可以将这样的循环更简洁地写成“for each”循环：

```java
for (String element : c)
{
    do something with element
}
```

编译器只是将“for each”循环转换为使用迭代器的循环。

“for each”循环适用于任何实现了 `Iterable` 接口的对象，该接口只有一个抽象方法：

```java
public interface Iterable<E>
{
    Iterator<E> iterator();
    . . .
}
```

`Collection` 接口扩展了 `Iterable` 接口。因此，你可以对标准库中的任何集合使用“for each”循环。

除了编写循环之外，你还可以调用 `forEachRemaining` 方法，并传入一个消费元素的 lambda 表达式。该 lambda 表达式会针对迭代器的每个元素被调用，直到没有剩余元素为止。

```java
iterator.forEachRemaining(element -> do something with element);
```

元素的访问顺序取决于集合类型。如果遍历 `ArrayList`，迭代器从索引 0 开始，并在每一步递增索引。然而，如果访问 `HashSet` 中的元素，你得到的顺序基本上是随机的。可以保证在迭代过程中会遇到集合的所有元素，但无法对其顺序做任何假设。这通常不是问题，因为对于计算总和或统计匹配项等计算而言，顺序并不重要。

![](img/0e7b74ef51a065c077b42cd87b362288_716_0.png)

> **注意：**
>
> 老用户会注意到，`Iterator` 接口的 `next` 和 `hasNext` 方法与 `Enumeration` 的 `nextElement` 和 `hasMoreElements` 方法作用相同。Java 集合库的设计者本可以选择使用 `Enumeration` 接口。但他们不喜欢那些繁琐的方法名，于是引入了一个方法名更短的新接口。

Java 集合库中的迭代器与其他库中的迭代器之间存在重要的概念差异。在传统的集合库中，例如 C++ 的标准模板库，迭代器是仿照数组索引建模的。给定这样的迭代器，你可以查找存储在该位置上的元素，很像如果你有一个数组索引 `i`，就可以查找数组元素 `a[i]`。与查找无关，你可以将迭代器推进到下一个位置。这与通过调用 `i++` 推进数组索引而不执行查找是相同的操作。然而，Java 迭代器不是这样工作的。查找和位置变更紧密耦合。查找元素的唯一方法是调用 next，而该查找会推进位置。

相反，要把 Java 迭代器看作位于*元素之间*。当你调用 next 时，迭代器会*跳过*下一个元素，并返回对刚刚越过的元素的引用（见图 9.3）。

> **注意：**
>
> 这里还有一个有用的类比。你可以把 `Iterator.next` 看作等同于 `InputStream.read`。从流中读取一个字节会自动“消费”该字节。下一次调用 `read` 会消费并返回输入中的下一个字节。同样，重复调用 `next` 可以让你读取集合中的所有元素。

`Iterator` 接口的 `remove` 方法删除最后一次调用 `next` 返回的元素。在许多情况下，这样做是合理的——你需要先看到元素，才能决定它就是应该被删除的那个元素。但如果你想删除特定位置的元素，仍然需要跳过该元素。例如，下面展示了如何删除字符串集合中的第一个元素：

```java
Iterator<String> it = c.iterator();
it.next(); // skip over the first element
it.remove(); // now remove it
```

![](img/0e7b74ef51a065c077b42cd87b362288_718_0.png)

**图 9.3** 推进迭代器

更重要的是，对 `next` 和 `remove` 方法的调用之间存在依赖关系。如果调用 `remove` 之前没有调用 `next`，那么调用 `remove` 是非法的。如果尝试这样做，就会抛出 `IllegalStateException`。

如果你想删除两个相邻元素，不能简单地调用

```java
it.remove();
it.remove(); // ERROR
```

相反，你必须先调用 `next` 跳过要删除的元素。

```java
it.next();
it.remove();
it.next();
it.remove(); // OK
```

### 9.1.4 泛型实用方法

Collection 和 Iterator 接口是泛型的，这意味着你可以编写能操作任何类型集合的实用方法。例如，下面是一个泛型方法，用于测试任意集合是否包含给定元素：

```java
public static <E> boolean contains(Collection<E> c, Object obj)
{  for (E element : c)
       if (element.equals(obj))
           return true;
   return false;
}
```

Java 库的设计者认为，其中一些实用方法非常有用，库应当提供它们。这样，库用户就不必不断重复造轮子。contains 方法就是这样一个方法。

事实上，Collection 接口声明了相当多有用的方法，所有实现类都必须提供这些方法。其中包括

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
```

其中许多方法不言自明；你可以在本节末尾的 API 注释中找到完整文档。

当然，如果每个实现 `Collection` 接口的类都必须提供这么多常规方法，那会很麻烦。为了让实现者的工作更轻松，库提供了一个 `AbstractCollection` 类，它把基本方法 `size` 和 `iterator` 保留为抽象方法，但基于这些方法实现常规方法。例如：

```java
public abstract class AbstractCollection<E>
    implements Collection<E>
{
    . . .
    public abstract Iterator<E> iterator();

    public boolean contains(Object obj)
    {
        for (E element : this) // calls iterator()
            if (element.equals(obj))
                return true;
        return false;
    }
    . . .
}
```

具体集合类现在可以扩展 `AbstractCollection` 类。提供 `iterator` 方法由具体集合类负责，但 `contains` 方法已由 `AbstractCollection` 超类处理。不过，如果子类有更高效的 `contains` 实现方式，它可以自行这样做。

这种方法有点过时。如果这些方法是 `Collection` 接口的默认方法，那会更好。但事实并非如此。不过，已经添加了几个默认方法。其中大多数与流有关（将在第 II 卷讨论）。此外，还有一个有用的方法
