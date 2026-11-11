

![](img/127bccebb2cfadea3f02579edaad63c3_554_0.png)

**图9.11** 链表式哈希表

```
157-62-7935
456-62-5527
```

而`staff.values().iterator()`将按照以下顺序枚举这些值：

```
Amy Lee
Harry Hacker
Gary Cooper
Francesca Cruz
```

链表式哈希映射还可以使用*访问顺序*（而不是插入顺序）来遍历映射条目。每次调用`get`或`put`时，受影响的条目会从当前位置移除，放到条目链表的*末尾*。（只有条目链表中的位置受影响，哈希表桶不受影响。条目始终停留在与键的哈希码对应的桶中。）要构造这样的哈希映射，请调用

```java
new LinkedHashMap<K, V>(initialCapacity, loadFactor, true)
```

访问顺序对于实现缓存的“最近最少使用”规则非常有用。例如，你可能希望将经常访问的条目保留在内存中，而从数据库中读取不经常访问的对象。当你在表中找不到某个条目，且表已经相当满时，你可以获取一个表上的迭代器，并删除它枚举出的前几个元素。这些条目就是最近最少使用的条目。

你甚至可以自动化这个过程。创建一个`LinkedHashMap`的子类并覆盖该方法

```java
protected boolean removeEldestEntry(Map.Entry<K, V> eldest)
```

当你的方法返回true时，添加新条目就会导致最老的条目被移除。例如，下面的缓存最多保持100个元素：

```java
var cache = new LinkedHashMap<K, V>(128, 0.75F, true)
{
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest)
    {
        return size() > 100;
    }
};
```

或者，你可以检查最老的条目来决定是否移除它。例如，你可能希望检查条目中存储的时间戳。

### 9.4.6 枚举集与映射

EnumSet是一个高效的集合实现，其中的元素属于枚举类型。由于枚举类型的实例数量有限，EnumSet在内部只是简单地实现为一个位序列。如果对应的值存在于集合中，该位即被置为1。

EnumSet类没有公有构造函数。使用静态工厂方法来构造集合：

```java
enum Weekday { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY };
EnumSet<Weekday> always = EnumSet.allOf(Weekday.class);
EnumSet<Weekday> never = EnumSet.noneOf(Weekday.class);
EnumSet<Weekday> workday = EnumSet.range(Weekday.MONDAY, Weekday.FRIDAY);
EnumSet<Weekday> mwf = EnumSet.of(Weekday.MONDAY, Weekday.WEDNESDAY, Weekday.FRIDAY);
```

你可以使用Set接口的常用方法来修改EnumSet。

EnumMap是一种映射，其键属于枚举类型。它在内部简单地以值数组的形式高效实现。你需要在构造函数中指定键类型：

```java
var personInCharge = new EnumMap<Weekday, Employee>(Weekday.class);
```

> 注意：在EnumSet的API文档中，你会看到形式为`E extends Enum<E>`的古怪类型参数。这只是表示“E是一个枚举类型”。所有枚举类型都扩展了泛型Enum类。例如，`Weekday extends Enum<Weekday>`。

### 9.4.7 标识哈希映射

IdentityHashMap有一个相当专门的用途。在这里，键的哈希值不应由hashCode方法计算，而应由System.identityHashCode方法计算。正是Object.hashCode用来根据对象的内存地址计算哈希码的那个方法。此外，在比较对象时，IdentityHashMap使用==而不是equals。

换句话说，即使不同键对象的内容相等，它们也被视为不同。这个类对于实现对象遍历算法非常有用，例如对象序列化，在这些算法中你需要跟踪哪些对象已经被遍历过。

| `java.util.WeakHashMap<K, V>` 1.2 |
|---|
| • `WeakHashMap()`<br>• `WeakHashMap(int initialCapacity)`<br>• `WeakHashMap(int initialCapacity, float loadFactor)`<br>  构造一个具有指定容量和加载因子的空哈希映射。 |

| `java.util.LinkedHashSet<E>` 1.4 |
|---|
| • `LinkedHashSet()`<br>• `LinkedHashSet(int initialCapacity)`<br>• `LinkedHashSet(int initialCapacity, float loadFactor)`<br>  构造一个具有指定容量和加载因子的空链表式哈希集合。 |

| `java.util.LinkedHashMap<K, V>` 1.4 |
|---|
| • `LinkedHashMap()`<br>• `LinkedHashMap(int initialCapacity)`<br>• `LinkedHashMap(int initialCapacity, float loadFactor)`<br>• `LinkedHashMap(int initialCapacity, float loadFactor, boolean accessOrder)`<br>  构造一个具有指定容量、加载因子和顺序的空链表式哈希映射。accessOrder参数为true表示访问顺序，false表示插入顺序。<br>• `protected boolean removeEldestEntry(Map.Entry<K, V> eldest)`<br>  如果要移除最老的条目，应重写此方法以返回true。eldest参数是正在考虑移除的条目。在向映射中添加条目后会调用此方法。默认实现返回false——默认情况下不会移除旧元素。不过，你可以重新定义此方法以选择性地返回true——例如，如果最老的条目符合某种条件，或者映射超过一定大小。 |

| `java.util.EnumSet<E extends Enum<E>>` 5 |
|---|
| • `static <E extends Enum<E>> EnumSet<E> allOf(Class<E> enumType)`<br>  返回一个包含给定枚举类型所有值的可变集合。<br>• `static <E extends Enum<E>> EnumSet<E> noneOf(Class<E> enumType)`<br>  返回一个最初为空的可变集合。<br>• `static <E extends Enum<E>> EnumSet<E> range(E from, E to)`<br>  返回一个包含from和to之间（包括端点）所有值的可变集合。<br>• `static <E extends Enum<E>> EnumSet<E> of(E e)`<br>  ...<br>• `static <E extends Enum<E>> EnumSet<E> of(E e1, E e2, E e3, E e4, E e5)`<br>• `static <E extends Enum<E>> EnumSet<E> of(E first, E... rest)`<br>  返回一个包含给定元素的可变集合，这些元素不能为null。 |

| `java.util.EnumMap<K extends Enum<K>, V>` 5 |
|---|
| • `EnumMap(Class<K> keyType)`<br>  构造一个空的可变映射，其键具有给定类型。 |

| `java.util.IdentityHashMap<K, V>` 1.4 |
|---|
| • `IdentityHashMap()`<br>• `IdentityHashMap(int expectedMaxSize)`<br>  构造一个空的标识哈希映射，其容量是超过1.5 × expectedMaxSize的最小2的幂。（expectedMaxSize的默认值为21。） |

| `java.lang.System` | 1.0 |
|---|---|
| • `static int identityHashCode(Object obj)` 1.1 | 返回与`Object.hashCode`计算的相同哈希码（派生自对象的内存地址），即使obj所属的类已经重新定义了`hashCode`方法。 |

## 9.5 视图与包装器

如果查看图9.4和图9.5，你可能会认为为了实现数量不多的具体集合类而设计大量接口和抽象类有点小题大做。然而，这些图并没有展现全貌。通过使用*视图*，你可以获得实现了Collection或Map接口的其他对象。你在映射类的keySet方法中已经看到了一个这样的例子。乍一看，似乎该方法创建了一个新集合，用映射中的所有键填充它，然后返回它。但事实并非如此。相反，keySet方法返回一个类的对象，该类实现了Set接口，其方法操作原始映射。这样的集合称为*视图*。

视图技术在集合框架中有许多有用的应用。我们将在以下小节中讨论这些应用。

### 9.5.1 小型集合

Java 9引入了静态方法，可以生成包含给定元素的集合或列表，以及包含给定键/值对的映射。例如，

```java
List<String> names = List.of("Peter", "Paul", "Mary");
Set<Integer> numbers = Set.of(2, 3, 5);
```

生成了一个包含三个元素的列表和一个包含三个元素的集合。对于映射，你可以这样指定键和值：

```java
Map<String, Integer> scores = Map.of("Peter", 2, "Paul", 3, "Mary", 5);
```

元素、键或值不能为null。

List和Set接口有十一个方法，参数从零到十个不等，还有一个of方法，支持可变数量的参数。提供这些特化版本是为了提高效率。

