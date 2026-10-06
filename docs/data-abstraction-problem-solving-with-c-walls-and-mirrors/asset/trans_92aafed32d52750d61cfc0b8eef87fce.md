
# 第 3 章 基于数组的实现

## 3.3 在实现中使用递归

上一章给出了如何使用递归来处理数组的几个示例。如果你检查我们刚刚开发的 `ArrayBag` 的定义，你会看到两个可以被递归替换的循环：一个在公共方法 `getIndexOf()` 中，另一个在私有方法 `getIndexOf` 中。让我们来看细节。

### 3.3.1 getIndexOf 方法

我们从在数组中搜索给定条目的私有方法开始。迭代定义按顺序逐个检查数组中的每个条目，直到找到所需的条目或到达数组末尾且未找到目标。假设 `searchIndex` 是下一个要检查的数组元素的索引。我们有两个基准情况：

- `items[searchIndex]` 是我们要寻找的条目，完成了。
- 如果 `searchIndex < itemCount`，我们完成了，因为该条目不在数组中。

递归步骤是使用 `items[searchIndex + 1]` 搜索数组剩余部分。为了实现这种递归，`getIndexOf` 需要 `searchIndex` 作为参数。由于该方法是私有的，我们不需要为它定义另一个私有方法供其调用。然而，我们必须在头文件中将其声明修改如下：

```cpp
int getIndexOf(const ItemType&target, int searchIndex) const;
```

我们可以为此方法编写以下递归函数：

```cpp
template<class ItemType>
ArrayBag<ItemType>::getIndexOf(const ItemType& target, int searchIndex) const
{
    int result = -1;
    if (searchIndex < itemCount)
    {
        if (items[searchIndex] == target)
        {
            result = searchIndex;
        }
        else
        {
            result = getIndexOf(target, searchIndex + 1);
        } // end if
    } // end if
    return result;
}
```

由于我们更改了方法的头文件，我们需要定位并更改 `ArrayBag` 其他方法中对 `getIndexOf` 的调用。因此，我们将方法 `remove` 和 `contains` 内部调用从

```cpp
getIndexOf(anEntry);
```

更改为

```cpp
getIndexOf(anEntry, 0);
```

### 3.3.2 getFrequencyOf 方法

`getFrequencyOf` 方法同样在搜索数组，与 `indexOf` 类似，但与 `indexOf` 不同，`getFrequencyOf` 必须检查数组中的每一个条目。也就是说，如果数组匹配我们要寻找的条目，搜索也不会结束。

假设 `searchIndex` 是下一个要检查的元素的索引。该搜索的递归定义只有一个基准情况：如果 `searchIndex` 等于 `itemCount`，我们完成了。然而，我们有两个递归步骤：

- 如果 `items[searchIndex]` 是我们要寻找的条目，则该条目的出现频率比其在数组剩余部分的出现频率多 1。
- 如果 `items[searchIndex]` 不是我们要寻找的条目，则该条目的出现频率与其 `getFrequencyOf` 的另一个参数相同，这里的递归方法需要

正如我们必须为 `getIndexOf` 添加另一个参数一样，这里的递归方法需要 `searchIndex` 作为参数。然而，`getFrequencyOf` 是一个公共方法，所以我们不能更改它的签名。相反，`getFrequencyOf` 必须调用一个辅助递归搜索的私有方法。因此，在头文件的私有部分添加以下声明：

```cpp
int countFrequency(const ItemType& target, int searchIndex) const;
```

`getFrequencyOf` 方法简单地调用这个私有方法，因此它的定义如下：

```cpp
template<class ItemType>
int ArrayBag<ItemType>::getFrequency(const ItemType& anEntry) const {
    return countFrequency(anEntry, 0);
} // end getFrequency
```

私有方法 `countFrequency` 的递归定义为：

```cpp
template<class ItemType>
int ArrayBag<ItemType>::countFrequency(const ItemType& target,
                               int searchIndex) const {
    if (searchIndex < itemCount) {
        if (items[searchIndex] == target) {
            return 1 + countFrequency(target, searchIndex + 1);
        }
        else {
            return countFrequency(target, searchIndex + 1);
        } // end if
    }
    else {
        return 0; // Base case
    }
} // end countFrequency
```

从风格上来说，我们倾向于让方法只有一个出口。为了修改 `countFrequency` 使其只有一个返回语句而不是三个，我们定义了一个局部变量 `frequency` 来包含返回值。该方法随后有如下定义。注意，基准情况是隐式的。

```cpp
template<class ItemType>
int ArrayBag<ItemType>::countFrequency(const ItemType& target,
                               int searchIndex) const
{
  int frequency = 0;
  if (searchIndex < itemCount) {
    if (items[searchIndex] == target) {
      frequency = 1 + countFrequency(target, searchIndex + 1);
    } else {
      frequency = countFrequency(target, searchIndex + 1);
    } // end if
  }
  return frequency;
} // end countFrequency
```

# 总结

- 1. 通过使用类来实现 ADT，你封装了 ADT 的数据和操作。通过这种，你可以向使用 ADT 的程序隐藏实现细节。
- 2. 通过使用类来实现 ADT，你封装了 ADT 的数据和操作。通过这种，你可以向使用 ADT 的程序隐藏实现细节。
- 3. 通过使用类来实现 ADT，你封装了 ADT 的数据和操作。通过这种，你可以向使用 ADT 的程序隐藏实现细节。
- 4. 通过使用类来实现 ADT，你封装了 ADT 的数据和操作。通过这种，你可以向使用 ADT 的程序隐藏实现细节。
- 5. 通过使用类来实现 ADT，你封装了 ADT 的数据和操作。通过这种，你可以向使用 ADT 的程序隐藏实现细节。
- 6. 通过使用类来实现 ADT，你封装了 ADT 的数据和操作。通过这种，你可以向使用 ADT 的程序隐藏实现细节。
- 7. 通过使用类来实现 ADT，你封装了 ADT 的数据和操作。通过这种，你可以向使用 ADT 的程序隐藏实现细节。
- 8. 通过使用类来实现 ADT，你封装了 ADT 的数据和操作。通过这种，你可以向使用 ADT 的程序隐藏实现细节。

# 练习

- 1. 通过使用类来实现 ADT，你封装了 ADT 的数据和操作。通过这种，你可以向使用 ADT 的程序隐藏实现细节。
- 2. 设计并实现一个表示日期的 ADT。你可以用整数表示月份、日期和年份（例如，4/1/2014）。
包含将日期进一的操作，并使用数字或单词显示日期。作为增强，包含星期几。
- 3. 设计并实现一个以美元和分为单位的货币价格的 ADT。完成实现后，编写一个客户端函数计算客户为价格为 y 的物品支付找零 x。
- 4. 设计并实现一个表示银行账户的 ADT。ADT 的数据应包括客户姓名、账号和余额。初始化操作应将数据设置为客户端提供的值。包括存款、取款、计算利以及显示账户统计的操作。
- 5. 为 `ArrayBag` 类添加并、交集和差方法。第 1 章的 6、7、8 题描述了这些操作。
- 6. 使用数组实现第 1 章第 5 题中的集合。
- 7. 使用数组实现第 1 章第 6 题中的堆栈。
- 8. 为 `ArrayBag` 指定并定义一个方法，从包中移除随机条目。
- 9. 为类添加一个构造函数，从给定的数组创建一个包。
