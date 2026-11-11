
队列接口的一种最简形式可能如下所示：

```java
public interface Queue<E> // a simplified form of the interface in the standard library
{
    void add(E element);
    E remove();
    int size();
}
```

该接口并未说明队列是如何实现的。队列的两种常见实现中，一种使用“循环数组”，另一种使用链表（见图 9.2）。

![](img/127bccebb2cfadea3f02579edaad63c3_509_0.png)

**图 9.2** 队列实现

每种实现都可以由一个实现 Queue 接口的类来表示。

```java
public class CircularArrayQueue<E> implements Queue<E> // not an actual library class
{
    private int head;
    private int tail;

    CircularArrayQueue(int capacity) { . . . }
    public void add(E element) { . . . }
    public E remove() { . . . }
    public int size() { . . . }
    private E[] elements;
}

public class LinkedListQueue<E> implements Queue<E> // not an actual library class
{
    private Link head;
    private Link tail;

    LinkedListQueue() { . . . }
    public void add(E element) { . . . }
    public E remove() { . . . }
    public int size() { . . . }
}
```

> **注意：** Java 类库实际上并没有名为 CircularArrayQueue 和 LinkedListQueue 的类。我们使用这些类作为示例，来解释集合接口与集合实现之间的概念区别。如果你需要一个循环数组队列，请使用 ArrayDeque 类。对于链表队列，只需使用 LinkedList 类——它实现了 Queue 接口。

在程序中使用队列时，一旦集合已经构造完成，你无需知道实际使用的是哪种实现。因此，只在构造集合对象时才使用具体类是有意义的。使用*接口类型*来持有集合引用。

```java
Queue<Customer> expressLane = new CircularArrayQueue<>(100);
expressLane.add(new Customer("Harry"));
```

采用这种方法，如果你改变主意，也可以轻松改用另一种实现。你只需在程序中的一个地方进行修改——即构造函数调用处。如果你最终认为 LinkedListQueue 是更好的选择，那么代码就变成

```java
Queue<Customer> expressLane = new LinkedListQueue<>();
expressLane.add(new Customer("Harry"));
```

为什么要在一种实现和另一种实现之间做选择？接口并未说明某种实现的效率。循环数组比链表稍微高效一些，因此通常更可取。然而，和往常一样，这是有代价的。循环数组是一种*有界*集合——它的容量有限。如果你的程序要收集的对象数量没有上限，那么最终可能还是链表实现更合适。

当你研究 API 文档时，会发现另一组名称以 Abstract 开头的类，例如 AbstractQueue。这些类是为类库实现者准备的。如果你想要实现自己的队列类（这种可能性也许不大），你会发现扩展 AbstractQueue 比实现 Queue 接口的所有方法更容易。

### 9.1.2 集合接口

Java 类库中集合类的基础接口是 Collection 接口。该接口有两个基本方法：

```java
public interface Collection<E>
{
    boolean add(E element);
    Iterator<E> iterator();
    . . .
}
```

除了这两个方法之外，还有几个方法；我们将在后面讨论它们。

add 方法向集合中添加一个元素。如果添加元素确实改变了集合，add 方法返回 true；如果集合没有变化，则返回 false。例如，如果你尝试向一个集（set）中添加一个对象，而该对象已经存在，那么添加请求不会产生任何效果，因为集会拒绝重复元素。

iterator 方法返回一个实现 Iterator 接口的对象。你可以使用该迭代器对象逐个访问集合中的元素。我们将在下一节讨论迭代器。

### 9.1.3 迭代器

Iterator 接口有四个方法：

```java
public interface Iterator<E>
{
    E next();
    boolean hasNext();
    void remove();
    default void forEachRemaining(Consumer<? super E> action);
}
```

通过反复调用 next 方法，你可以逐个访问集合中的元素。然而，如果到达集合末尾，next 方法会抛出 NoSuchElementException。因此，在调用 next 之前需要先调用 hasNext 方法。如果迭代器对象还有更多元素可访问，该方法返回 true。如果你想检查集合中的所有元素，请获取一个迭代器，然后在 hasNext 返回 true 时持续调用 next 方法。例如：

```java
Collection<String> c = ...;
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

“for each”循环适用于任何实现了 Iterable 接口的对象，该接口只有一个抽象方法：

```java
public interface Iterable<E>
{
    Iterator<E> iterator();
    ...
}
```

Collection 接口扩展了 Iterable 接口。因此，你可以对标准库中的任何集合使用“for each”循环。

除了编写循环，你还可以使用一个消费元素的 lambda 表达式来调用 forEachRemaining 方法。该 lambda 表达式会针对迭代器的每个元素被调用，直到没有元素剩余。

```java
iterator.forEachRemaining(element -> do something with element);
```

元素的访问顺序取决于集合类型。如果你遍历 ArrayList，迭代器从索引 0 开始，并在每一步递增索引。然而，如果你访问 HashSet 中的元素，得到的顺序基本上是随机的。你可以确信在迭代过程中会遇到集合的所有元素，但不能对它们的顺序做任何假设。这通常不是问题，因为对于计算总和或计数匹配项等计算而言，顺序并不重要。

> **注意：** 老手会注意到，Iterator 接口的 next 和 hasNext 方法与 Enumeration 的 nextElement 和 hasMoreElements 方法用途相同。Java 集合库的设计者本可以选择使用 Enumeration 接口。但他们不喜欢那些冗长的方法名，于是引入了一个方法名更短的新接口。

Java 集合库中的迭代器与其他库中的迭代器之间存在一个重要的概念差异。在传统的集合库（例如 C++ 的标准模板库）中，迭代器模仿数组索引。给定这样的迭代器，你可以查找存储在该位置的元素，就像如果你有数组索引 i，就可以查找数组元素 a[i] 一样。与查找无关，你还可以将迭代器前进到下一个位置。这与通过调用 i++ 来推进数组索引而不执行查找是相同的操作。然而，Java 迭代器并非如此工作。查找和位置变更紧密耦合。查找元素的唯一方法是调用 next，而该查找会推进位置。

相反，可以把 Java 迭代器看作位于元素之间。当你调用 next 时，迭代器会跳过下一个元素，并返回它刚刚越过的那个元素的引用（见图 9.3）。

**注意：** 这里还有一个有用的类比。你可以把 Iterator.next 看作等同于 InputStream.read。从流中读取一个字节会自动“消费”该字节。下一次调用 read 会消费并返回输入中的下一个字节。类似地，反复调用 next 可以让你读取集合中的所有元素。

Iterator 接口的 remove 方法会移除上一次调用 next 所返回的元素。在许多情况下，这是合理的——你需要先看到元素，才能决定它是否应该被移除。但如果你想移除某个特定位置上的元素，仍然需要先跳过该元素。例如，下面展示了如何移除字符串集合中的第一个元素：
