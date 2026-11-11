
两个具有不同坐标但面积相同的不同矩形。树的排序顺序必须是*全序*。任意两个元素都必须可比较，并且只有当元素相等时，比较结果才能为零。对于矩形来说，确实存在这样的排序顺序（对其坐标的字典序），但计算起来既不自然又很麻烦。相比之下，`Rectangle` 类已经定义了哈希函数。它只是对坐标进行哈希。

> **注意：** 从 Java 6 开始，`TreeSet` 类实现了 `NavigableSet` 接口。该接口增加了一些便捷方法，用于定位元素和向后遍历。详见 API 注释。

清单 9.3 中的程序构建了两个 `Item` 对象的树集。第一个集合按部件编号排序，这是 `Item` 对象的默认排序顺序。第二个集合使用自定义比较器按描述排序。

**清单 9.3  `treeSet/TreeSetTest.java`**

```java
package treeSet;

import java.util.*;

/**
 * This program sorts a set of Item objects by comparing their descriptions.
 * @version 1.13 2018-04-10
 * @author Cay Horstmann
 */
public class TreeSetTest
{
   public static void main(String[] args)
   {
      var parts = new TreeSet<Item>();
      parts.add(new Item("Toaster", 1234));
      parts.add(new Item("Widget", 4562));
      parts.add(new Item("Modem", 9912));
      System.out.println(parts);

      var sortByDescription = new TreeSet<Item>(Comparator.comparing(Item::getDescription));

      sortByDescription.addAll(parts);
      System.out.println(sortByDescription);
   }
}
```

**清单 9.4  `treeSet/Item.java`**

```java
package treeSet;

import java.util.*;

/**
 * An item with a description and a part number.
 */
public class Item implements Comparable<Item>
{
    private String description;
    private int partNumber;

    /**
     * Constructs an item.
     * @param aDescription the item's description
     * @param aPartNumber the item's part number
     */
    public Item(String aDescription, int aPartNumber)
    {
        description = aDescription;
        partNumber = aPartNumber;
    }

    /**
     * Gets the description of this item.
     * @return the description
     */
    public String getDescription()
    {
        return description;
    }

    public String toString()
    {
        return "[description=" + description + ", partNumber=" + partNumber + "]";
    }

    public boolean equals(Object otherObject)
    {
        if (this == otherObject) return true;
        if (otherObject == null) return false;
        if (getClass() != otherObject.getClass()) return false;
        var other = (Item) otherObject;
        return Objects.equals(description, other.description) && partNumber == other.partNumber;
    }

    public int hashCode()
    {
        return Objects.hash(description, partNumber);
    }

    public int compareTo(Item other)
    {
        int diff = Integer.compare(partNumber, other.partNumber);
        return diff != 0 ? diff : description.compareTo(other.description);
    }
}
```

| `java.util.TreeSet<E>` 1.2 | |
|---|---|
| `TreeSet()`<br>`TreeSet(Comparator<? super E> comparator)` | 构造一个空树集。 |
| `TreeSet(Collection<? extends E> elements)`<br>`TreeSet(SortedSet<E> s)` | 构造一个树集，并添加来自集合或有序集中的所有元素（在后一种情况下，使用相同的排序）。 |

| `java.util.SortedSet<E>` 1.2 | |
|---|---|
| `Comparator<? super E> comparator()` | 返回用于对元素排序的比较器；如果元素是通过 *Comparable* 接口的 *compareTo* 方法进行比较的，则返回 null。 |
| `E first()`<br>`E last()` | 返回有序集中的最小或最大元素。 |

| `java.util.NavigableSet<E>` 6 | |
|---|---|
| `E higher(E value)`<br>`E lower(E value)` | 返回大于 value 的最小元素，或小于 value 的最大元素；如果不存在这样的元素，则返回 null。 |
| `E ceiling(E value)`<br>`E floor(E value)` | 返回大于等于 value 的最小元素，或小于等于 value 的最大元素；如果不存在这样的元素，则返回 null。 |
| `E pollFirst()`<br>`E pollLast()` | 移除并返回此集合中的最小或最大元素；如果集合为空，则返回 null。 |
| `Iterator<E> descendingIterator()` | 返回一个按降序遍历此集合的迭代器。 |

### 9.3.5 队列与双端队列

正如我们已经讨论过的，队列允许你在尾部高效地添加元素，并从头部移除元素。双端队列，或 *deque*，允许你在头部和尾部高效地添加或移除元素。不支持在中间添加元素。Java 6 引入了 `Deque` 接口。该接口由 `ArrayDeque` 和 `LinkedList` 类实现，这两个类都提供了可随需要增长大小的双端队列。在第 12 章，你将看到有界队列和双端队列。

| `java.util.Queue<E>` 5 | |
|---|---|
| `boolean add(E element)`<br>`boolean offer(E element)` | 如果队列未满，则将给定元素添加到队列尾部并返回 true。如果队列已满，第一个方法抛出 `IllegalStateException`，而第二个方法返回 false。 |
| `E remove()`<br>`E poll()` | 如果队列非空，则移除并返回此队列头部的元素。如果队列为空，第一个方法抛出 `NoSuchElementException`，而第二个方法返回 `null`。 |
| `E element()`<br>`E peek()` | 如果队列非空，则返回此队列头部的元素但不移除。如果队列为空，第一个方法抛出 `NoSuchElementException`，而第二个方法返回 `null`。 |

| `java.util.Deque<E>` 6 | |
|---|---|
| `void addFirst(E element)`<br>`void addLast(E element)`<br>`boolean offerFirst(E element)`<br>`boolean offerLast(E element)` | 将给定元素添加到此双端队列的头部或尾部。如果双端队列已满，前两个方法抛出 `IllegalStateException`，而后两个方法返回 `false`。 |
| `E removeFirst()`<br>`E removeLast()`<br>`E pollFirst()`<br>`E pollLast()` | 如果双端队列非空，则移除并返回此双端队列头部或尾部的元素。如果双端队列为空，前两个方法抛出 `NoSuchElementException`，而后两个方法返回 `null`。 |
| `E getFirst()`<br>`E getLast()`<br>`E peekFirst()`<br>`E peekLast()` | 如果双端队列非空，则返回此双端队列头部或尾部的元素但不移除。如果双端队列为空，前两个方法抛出 `NoSuchElementException`，而后两个方法返回 `null`。 |

| `java.util.ArrayDeque<E>` 6 | |
|---|---|
| `ArrayDeque()`<br>`ArrayDeque(int initialCapacity)` | 构造一个无界双端队列，初始容量为 16 或给定的初始容量。 |

### 9.3.6 优先级队列

优先级队列在元素以任意顺序插入后，按排序顺序检索元素。也就是说，每当你调用 remove 方法时，你会得到当前优先级队列中最小的元素。然而，优先级队列不会对其所有元素进行排序。如果你遍历这些元素，它们不一定是有序的。优先级队列使用了一种优雅而高效的数据结构，称为堆。堆是一种自组织的二叉树，其中添加和移除操作会使最小元素向根节点移动，而不会浪费时间对所有元素进行排序。

与 `TreeSet` 一样，优先级队列既可以容纳实现了 `Comparable` 接口的类的元素，也可以容纳你在构造函数中提供的 `Comparator` 对象。

优先级队列的一个典型用途是作业调度。每个作业都有一个优先级。作业按随机顺序添加。每当一个新作业可以启动时，就从队列中移除最高优先级的作业。（由于传统上优先级 1 被视为“最高”优先级，因此移除操作会得到最小元素。）

**清单 9.5  `priorityQueue/PriorityQueueTest.java`**

```java
package priorityQueue;

import java.util.*;
import java.time.*;

/**
 * This program demonstrates the use of a priority queue.
 * @version 1.02 2015-06-20
 * @author Cay Horstmann
 */
```
