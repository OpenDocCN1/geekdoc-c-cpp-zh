

## 稳定

只要两个值都不改变，x < y 的结果就保持不变。

## 安全

比较相同类型的值不会抛出异常。

我们可以以类似的方式为引用类型定义 CompareTo 和 operator<，不过我们还需要考虑 null 引用，它应始终被比较为小于任何非 null 值。

## 其他类型的排序

按 DateTime 或数字排序是按大小排序的一个例子，但其他排序方式也是可能的。字符串通常使用字典序（lexicographical ordering），大致意思是：如果一个字符串在词典（也就是常说的字典）中出现在另一个字符串之前，那么它就小于另一个字符串。

其他值在本质上是序数性的，例如一年中的月份。序数比较有时需要格外小心。以英语中的星期为例：星期日应该排在星期一之前吗？这个问题的答案取决于我们如何定义一周的第一天。

有些值本质上并不存在“小于另一个值”的关系。Color 类型就是一个例子：当我们按彩虹顺序枚举颜色时，红色排在蓝色之前——这是它们相对波长的属性——但在英语词典中蓝色肯定排在红色之前。在不同情况下，我们可能会对 Color 对象应用多种排序之一，但这些排序定义是外在于颜色概念的。

我们可以通过创建自己的比较器，甚至多个比较器来应对不同场景，从而针对具体情况自定义序列中元素的排序。IComparer<T> 接口是对第 5 章中 IEqualityComparer<T> 接口的补充。正如 IEqualityComparer<T> 建立了一种独立于被比较类型的相等性比较，IComparer<T> 的实现是一种外部定义的排序比较。清单 6-20 展示了一个自定义比较器类型，它按 LogEntry 对象的 Message 属性而非时间对它们进行排序。

```csharp
public sealed class LogEntryComparer : IComparer<LogEntry>
{
    public int Compare(LogEntry x, LogEntry y)
        => string.Compare(x.Message, y.Message, StringComparison.Ordinal);
}
```

清单 6-20：为 LogEntry 对象定义外部比较器

Compare 方法的语义与 IComparable.CompareTo 的语义一致：当 x 小于 y 时返回负整数，当 y 小于 x 时返回正整数，否则返回 0。标准库中的若干排序算法都重载了接受显式比较器对象作为参数的版本，包括此处展示的 Order 方法：

```csharp
var log = new List<LogEntry>();

--snip--

var comparer = new LogEntryComparer();
var alphabeticalLog = log.Order(comparer).ToList();
```

这个 alphabeticalLog 是一个新列表，其中 LogEntry 元素通过使用 LogEntryComparer.Compare 比较按字母顺序排序。List<T>.Sort、List<T>.BinarySearch 和 SortedList 的构造函数也提供了类似的重载。

排序是值的常见特征，但它不像基于值的相等性那样是本质特征。当一个值具有自然排序时，实现 CompareTo 方法是有意义的。另一方面，引用类型通常不会重写 CompareTo，除非它们也重写 Equals。将基于标识的相等性与基于值的排序混在一起，或者反过来，很可能会导致混乱，并可能产生难以追踪的错误。特别是，引用没有自然排序；说一个引用的值小于另一个引用毫无意义。

## 统一性与一致性的隐患

有时编码规范会建议我们对每个类型都重写 Equals 并实现 CompareTo。这类规则背后的想法通常是试图消除对对象使用的限制。没有实现 IComparable 的类型不能用作 SortedList 中的键。没有重写 Equals 和 GetHashCode 的类型不能可靠地用作 Dictionary 中的键。虽然我们可以使用 IComparer<T> 的实现来解决前者，使用自定义 IEqualityComparer<T> 来解决后者，但必须记住显式使用这些实现。

这类规范旨在提高一致性并消除常见需求中的障碍。其目标通常是使任何对象都能用作哈希容器中的键，或使这些对象的集合能根据其状态排序，而无需显式定义外部比较器。

建议这种统一性的规范忽视了这样一个事实：值与非值在语义和概念上是不同的，而且这种差异远远超出了引用类型和值类型的技术特征。引用语义有其自身的可取之处，尤其是当我们确实需要多个别名引用指向同一个可变实例时。这些特征并不适合用作集合中的键，也常常与排序产生冲突。一个可变对象的有序集合很可能因为改变其元素的状态而变得无序，这为我们要求所有值类型都不可变提供了又一个理由。一个已经排序的值集合应该保持有序。

正如我们所讨论的，有些类型没有自然排序。让我们重新审视 Color 的例子。坚持让 Color 类型实现 IComparable 接口会给我们留下一个问题：两个 Color 值的 CompareTo 应该如何表现？我们可以选择一种看似合理的实现，但这可能无法满足所有用例，从而在我们代码的其他方面造成困难。这就是为什么 record 和 record struct 虽然提供了 IEquatable<T> 接口的默认实现，却没有同时实现 IComparable<T>。即使各个字段可以用 CompareTo 比较，也并不意味着整个类型都能以这种方式比较。毕竟，Color 的所有字段都是实现了 IComparable<int> 的 int 值，但“小于”对 Color 值来说并不是有意义的比较。

对于值类型来说，重写 Equals 方法的主要目的并不是让它们能用作键。值不需要引用相等性，因为一个值与另一个具有相同属性的值是完全等价的。基于值的相等性是比较那些作为值的变量的唯一自然方式。

相比之下，引用类型通常依赖于基于标识的相等性。任何并非专门打算具有值语义的类型可能都不应该用作 Dictionary 中的键。

## 算术类型与非算术类型

正如并非所有值都有自然排序一样，有些值在本质上是算术的，有些则不是。例如，我们可以定义操作，让清单 6-11 中 Speed 类型的实例能够相加。像加法这样的操作可以用算术运算符自然地表示，例如在 startingSpeed + Speed.FromKmh(10) 这样的表达式中。

引入对算术操作（或任何操作）的支持，需要我们作为设计者进行一定的判断。我们需要留意所创建类型的常见用例，以及更广泛的期望，例如能够使用 + 运算符将两个实例加在一起。

与 Speed 不同，清单 6-17 中的 LogEntry 类型在本质上不是算术的，因此我们应该避免为其重载算术运算符。将两个 LogEntry 实例相加没有意义。

LogEntry 重载 operator== 和对应的 operator!= 进行相等性比较则是有意义的。LogEntry 是一个 record struct，因此编译器会自动提供相等运算符定义。既然我们已经为 LogEntry 实现了 IComparable<LogEntry>，还应该考虑重载 operator< 和 operator>，编译器不会提供这两个运算符。清单 6-21 展示了基于 CompareTo 方法实现这些运算符是直接了当的。

```csharp
public static bool operator<(LogEntry left, LogEntry right)
    => left.CompareTo(right) < 0;

public static bool operator>(LogEntry left, LogEntry right)
    => left.CompareTo(right) > 0;
```

清单 6-21：等价比较运算符定义

