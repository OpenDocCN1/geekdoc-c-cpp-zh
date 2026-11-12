

涉及从袋中移除条目的两种行为：移除特定条目和移除所有条目。假设我们为方法及其任何参数命名，并开始按如下伪代码指定它们：

```
// Removes one occurrence of a particular entry from the bag, if possible.
remove(anEntry)
```

```
// Removes all entries from the bag.
clear()
```

这些方法的返回类型是什么？
如果给定条目不在袋中，remove 方法将无法移除它。我们将让该方法返回一个布尔值，与 add 方法类似，以便指示是否成功。因此，该方法的 UML 规范为

```
+remove(anEntry: ItemType): boolean
```

clear 方法可以是一个 void 方法：我们只想清空袋子，而不获取其任何内容。因此，我们按如下方式细化其规范：

```
+clear(): void
```

其余行为不会更改袋子的内容。其中一种行为统计给定对象在袋中出现的次数。其伪代码规范为

```
// Counts the number of times a given entry appears in the bag.
getFrequencyOf(anEntry: ItemType): integer
```

另一种方法测试袋子是否包含给定对象。我们按如下伪代码指定它：

```
// Tests whether the bag contains a given entry.
contains(anEntry: ItemType): boolean
```

最后，我们想查看袋子的内容。我们不提供显示袋中条目的方法，而是定义一个将这些条目放入向量的方法。客户端随后可以按任意方式显示其中任何或全部条目。以下是我们最后一种方法的规范。

```
// Gets all entries in the bag.
toVector(): vector
```

在开发袋子方法的先前规范时，我们使用 UML 表示法对其进行了表示。图 1-7 显示了这样做的结果。

## 图 1-7 类 Bag 的 UML 表示法

| Bag |
| :--- |
| +getCurrentSize(): integer |
| +isEmpty(): boolean |
| +add(newEntry: ItemType): boolean |
| +remove(anEntry: ItemType): boolean |
| +clear(): void |
| +getFrequencyOf(anEntry: ItemType): integer |
| +contains(anEntry: ItemType): boolean |
| +toVector(): vector |

请注意，CRC 卡片和 UML 图并未反映所有细节，例如假设和异常情况。但是，在识别出此类条件后，您应指定方法在每种情况下的行为。您应记录关于希望方法如何行为的决定，如我们在以下表格中所做。稍后，您可以将这些非正式描述纳入记录方法的 C++ 注释中。

## 抽象数据类型：袋

- 有限数量的对象，不一定互不相同，无特定顺序，且具有相同的数据类型。
- 此集合中的对象数量。

| Pseudocode | Description |
| --- | --- |
| getCurrentSize() | 任务：报告此袋中当前的对象数量。输入：无。输出：袋中当前的对象数量。 |
| isEmpty() | 任务：查看此袋是否为空。输入：无。输出：根据袋是否为空返回 true 或 false。 |
| add(newEntry) | 任务：将给定对象添加到此袋中。输入：newEntry 是一个对象。输出：根据添加是否成功返回 true 或 false。 |
| remove(anEntry) | 任务：如果可能，从此袋中移除特定对象的一个出现。输入：anEntry 是一个对象。输出：根据移除是否成功返回 true 或 false。 |
| clear() | 任务：从此袋中移除所有对象。输入：无。输出：无。 |
| getFrequencyOf(anEntry) | 任务：统计对象在此袋中出现的次数。输入：anEntry 是一个对象。输出：anEntry 在袋中出现的整数次数。 |
| contains(anEntry) | 任务：测试此袋是否包含特定对象。输入：anEntry 是一个对象。输出：根据 anEntry 是否出现在袋中返回 true 或 false。 |
| toVector() | 任务：获取此袋中的所有对象。输入：无。输出：一个包含袋中当前所有条目的向量。 |

注意：处理异常情况

如前所述，您必须决定如何处理异常情况。ADT 袋的文档应反映这些决定以及前面讨论中的细节。例如，我们对 remove 方法的规范表明，如果客户端尝试从空袋中移除条目，它将返回 false。相反，我们本可以为该方法设置前提条件，即袋不能为空。然后，客户端有责任在调用方法之前检查前提条件是否满足。请注意，客户端可以使用 ADT 袋的其他方法，例如 isEmpty 和 getCurrentSize，来协助完成此任务。

注意：ADT 规范的初稿常常会忽略或忽视您确实需要考虑的情况。您可能会故意做出这些遗漏以简化初稿。一旦您编写了规范的主要部分，就可以专注于使规范完整的细节。

问题 1 使用 UML 表示法编写一个函数的规范，该函数计算 n 个任意整数数组中前五个正整数的和。

## 1.5.3 ADT 的接口模板

随着规范变得更加详细，它们应越来越反映您选择的编程语言。最终，您可以为袋子的方法编写 C++ 头部声明，并将它们组织成实现 ADT 的类的头文件。

清单 1-1 中的 C++ 头文件包含 ADT 袋的方法以及描述其行为的详细注释。如果您不熟悉 C++ 类、模板和虚方法，C++ 插曲 1 将对 C++ 类进行复习，并讨论 C++ 模板、虚方法和抽象基类。通过使用模板和抽象基类，我们可以从第一个 ADT 开始利用封装、多态和继承等面向对象设计概念。

注意：为了强调 ADT 设计与其数据结构实现之间的区别，本教科书在描述我们的 ADT 时使用模板和抽象基类。我们将包含抽象基类的头文件称为客户端接口。程序员在使用您程序中的类时，不应需要比客户端接口更多的内容，因为它完全指定了 ADT 的方法。

在检查清单 1-1 中的接口时，请注意为解决前一节中提到的异常情况所做的决定。特别是，add、remove 和 contains 方法均返回一个值。请注意我们用于指定方法的注释标签，它们以 @ 开头，并在附录 I 中描述。

目前，袋中的项目将是同一类的对象。为了容纳任何单个类类型的条目，袋方法为每个条目使用泛型 ItemType。为了赋予标识符 ItemType 含义，我们必须在类头之前的一行上编写 template<class ItemType>。一旦客户端选择了实际数据类型，编译器将在 ItemType 出现的任何地方使用该数据类型。

类 BagInterface 是一个 C++ 抽象基类。在 C++ 中，抽象基类（或简称抽象类）包含至少一个声明为虚函数且没有实现的方法。抽象类不能被实例化；它只能用作基类。子类必须实现抽象类中指定但未定义的方法。

```
LISTING 1-1 A file containing a C++ interface for bags

/** @file BagInterface.h */
#ifndef BAG_INTERFACE
#define _BAG_INTERFACE
#include <vector>

template<class ItemType>
class BagInterface
{
public:
//# Gets the current number of entries in this bag.
//@return The integer number of entries currently in the bag. */
virtual int getCurrentSize() const = 0;

//# Sees whether this bag is empty.
//@return True if the bag is empty, or false if not. */
virtual bool isEmpty() const = 0;

//# Adds a new entry to this bag.
//@post If successful, newEntry is stored in the bag and
// the count of items in the bag has increased by 1.
//@param newEntry The object to be added as a new entry.
//@return True if addition was successful, or false if not. */
virtual bool add(const ItemType& newEntry) = 0;

//# Removes one occurrence of a given entry from this bag,
// if possible.
//@post If successful, anEntry has been removed from the bag
// and the count of items in the bag has decreased by 1.
//@param anEntry The entry to be removed.
//@return True if removal was successful, or false if not. */
virtual bool remove(const ItemType& anEntry) = 0;

//# Removes all entries from this bag.
//@post Bag contains no items, and the count of items is 0. */
virtual void clear() = 0;

//# Counts the number of times a given entry appears in bag.
//@param anEntry The entry to be counted.
//@return The number of times anEntry appears in the bag. */
virtual int getFrequencyOf(const ItemType& anEntry) const = 0;
(continues)
```

