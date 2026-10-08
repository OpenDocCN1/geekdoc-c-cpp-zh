

# 第 7 章：操作集合

```
- (void)insertObject:(id)anObject
    atIndex:(NSUInteger)anIndex
{
    if (![anObject isKindOfClassClass:type])
    {
        return;
    }
    [realArray insertObject:anObject
        atIndex:anIndex];
}
- (void)removeObjectAtIndex:(NSUInteger)idx
{
    [realArray removeObjectAtIndex:idx];
}
```

源自 checkedArray.m

这意味着在 NSArray 或 NSMutableArray 上声明的所有其他方法都将正常工作。

**注意：** 在 C++ 中，基本类型方法将是父类中的纯**虚拟**方法，编译器会阻止你直接实例化父类，或者任何没有实现这些方法的子类。Objective-C 中没有相应的对应机制。

子类化的更常见的原因是你想为底层表示实现一个不同的数据结构。例如，如果你打算在数组的一端插入对象，然后从另一端移除它们，你可能想使用可调整大小的环形缓冲区（ring buffer）作为你的数组实现。

如果是这种情况，你仍然应该重写相同的方法，但这次要用你自己的存储机制的实现来替换它们。然后你可以在任何可以使用父类的地方使用子类——包括将其传递给其他库——但将使用你自己的存储器。

# 在 C++ 集合中存储 Objective-C 对象

```
std::trl::unordered_map<id, __weak id,
object_hash<id>, object_equal<id>> map;
@autoreleasepool {
NSString *str = [[NSString alloc]
initWithUTF8String: argv[0]];
map[@"arg0"] = str;
NSLog("%s@", map[@"arg0"]);
str = nil;
}
NSLog("%s@", map[@"arg0"]);
```

源自 collection.mm

Objective-C++ 的历史问题之一是集合类型之间互操作的困难。Objective-C 集合旨在存储 Objective-C 对象，因此在存储 C++ 结构体时是不可用的。C++ 集合要灵活得多。它们是以模板实现的；因此，理论上它们可以存储任何类型。

在实践中，在 C++ 集合中存储 Objective-C 对象由于内存管理而变得复杂。Objective-C 对象期望任何想要保留其所有权引用的对象发送 -retain 消息。C++ 集合并非为了 Objective-C 而编写的，它们没有这样做，因此在配合 Objective-C++ 使用它们时必须非常小心。

有了自动引用计数（ARC），这变得简单多许多。当你使用带有 Objective-C 对象类型的 C++ 模板时，它会被展开，模板中的每次赋值都会在其周围自动插入相关的引用计数调用。这甚至扩展到了支持它们的系统的弱引用。本节开头的示例展示了如何使用 C++ map 类型来实现等同于带有强弱指针的 NSMapTable 的。

C++ unordered_map 需要两个支持类，一个用于定义相等性，另一个用于对对象进行哈希。这些通过简单地封装相关的 Objective-C 消息来实现。

可以进行类似的操作，尽管没有弱指针，但可以使用一个 C++ 智能指针类，该类在构造时发送 -retain 消息，在销毁时发送 -release 消息。然而，这可能会慢得多，因为它无法从 ARC 优化中受益。典型的

```
template <typename X>
struct object_equal {
    bool operator()(const X s1, const X s2) const {
        return (s1==s2) || [(id)s1 isEqual:(id)s2];
    }
}
template <typename X>
struct object_hash {
    size_t operator()(const X s1) const {
        return (size_t)[(id)s1 hash];
    }
}
```

源自 collection.mm

对 C++ 集合进行操作可能会多次分配指针。这将导致大量的 retain 和 release 操作，ARC 优化器随后会在冗余的地方移除它们。如果使用智能指针类，它们将产生大量的消息发送。

在 C++ 术语中，这意味着 __unsafe_retained id 是一个简单的旧数据（POD）类型，而 __weak id 和 __strong id 实现了（隐含地）重载的赋值运算符和非平凡拷贝构造函数。如果你不理解这意味着什么，不用担心；只需假设可以在 C++ 中使用 ARC，一切都会像魔法一样正常工作。

# 日期和时间

在 Objective-C 中，有两个概念属于时间的大义范畴。一个是绝对时间，另一个是时间间隔（time intervals）。时间间隔很容易处理。它们是简单的标量值，通常以秒为单位。NSTInterval 类型用于存储时间间隔。这通常被定义为双精度浮点值，为大多数用途提供了足够的精度。

你会在各种框架中找到其他其他表示时间间隔的方法。例如 OS X 上的 QTKit，它将时间间隔存储为有理数。这允许你重复相加而不会遇到由于浮点舍入误差导致的漂移，这在处理媒体时非常重要。在部电影的长度范围内，复合浮点误差可能会导致视频和音频轨道明显不同步。

时间间隔给出两个绝对时间之间的差值。绝对时间的定义相当困难。时区甚至不同的日历使得定义绝对时间变得相对困难。Foundation 框架中许多与时间和、日期相关的代码都是为了解决这个问题。

# 查找当前日期

```
NSDate *now = [NSDate date];
NSDate *date = [NSDate dateWithTimeIntervalSince1970:time(NULL)];
```

源自 date.m

NSDate 类封装了一个绝对时间值。它以两个组件的形式存储。其中一个是定义良好的固定点：纪元日（epoch date）。另一个是自该纪元以来的时间间隔。

NSDate 支持两个标准的纪元日，都是根据格里高亚历定义的。一个是 UNIX 纪元，1970 年 1 月 1 日。这个纪元日是在第一批 UNIX 系统中定义的，后来被纳入 ISO C 标准。C time() 函数将返回该日期以来的秒数。

另一个纪元时间作为 OpenStep 规范的一部分定义的，被称为参考日期（reference date）。这稍微不那么任意；它是当前千禧的开始：2001 年 1 月 1 日。

NSDate 的作用之一是让你无需知道你正在使用哪种纪元。你可以使用 -compare: 或任何相关方法比较两个日期，无论它们内部在使用的是什么。

如果你使用 +alloc/-init 或 +date 创建一个新日期，它将被设置为当前时间。日期是可变对象，但通常最好将它们视为不可变。修改日期的方法只有一个：-addTimeInterval:。它在 OS X 10.6 中被弃用，并且在旧代码中可能会导致问题，因为许多人倾向于忘记可以修改日期并只需保留它们，而不是复制它们。

# 第 8 章：日期和时间

# 为了显示转换日期

```
NSDate *now = [NSDate date];
NSCalendar *cal = [NSCalendar currentCalendar];
unsigned int components = NSYearCalendarUnit;
NSInteger year = [[components: components
fromDate: now] year];
NSString *date = [NSDateFormatter
localizedStringFromDate: now
dateStyle:DateFormatterLongStyle
timeStyle:DateFormatterNoStyle];
```

源自 calendar.m

NSDate 存储一个绝对时间，但如果你向用户展示自 1970-01-01 或 2001-01-01 以来过的秒数，他们可能会更愿意接受。除非当然，你的目标市场是机器人。

西方世界的大部分地区在过去几百年里的某个时间点统一使用了格里高亚历法。最早的采用者（他们可能经历了了所有的 Bug）包括 1582 年的西班牙、葡萄牙和意大利。最晚的是中国，在 1929 年。

这为本地化带来了一些显著的问题。如果你有一个代表 UNIX 纪元之前 120 年的日期，你该如何显示它？在格里高亚历中，它将是 1850 年 1 月 1 日，但在什么

