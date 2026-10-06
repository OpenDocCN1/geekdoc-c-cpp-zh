

## 问题 3：从 `contains` 中调用 `getFrequencyOf` 方法有什么优缺点？

注意：测试额外的方法
当你为 `ArrayBag` 类定义额外的方法时，你应该对它们进行测试。虽然你可能只关注这些额外方法，但你实际上应该循序渐进地构建一个测试程序。等待，测试你目前为止定义的所有方法。通过为 `DEFAULT_CAPACITY` 设置一个较小的值，你可以轻松地测试当包满时会发生什么。

注意：两种类型的循环
为了统计某个条目在数组中出现的次数，`getFrequencyOf` 方法使用了一个遍历数组所有条目的循环。事实上，循环体执行了 `itemCount` 次。相比之下，为了指示某个条目是否出现在数组中，方法中的循环在发现所需的条目后就会结束。该循环体的执行次数在一次到 `itemCount` 次之间。你应该熟悉执行固定次数或可变次数的循环。

## 3.2.5 删除元素的方法

我们直到现在推迟了 `remove` 方法的定义，因为它比其他方法需要更多的思考。然而，`clear` 方法相对简单，尽管我们把它留到了最后。

`remove` 方法现在想要从包中删除一个给定的条目——我们称之为条目。如果该条目在包中出现多次，我们将只删除其中一次。具体删除哪一次是不未指定的。我们将简单地删除搜索时遇到的该条目的第一次出现。遵循我们在 `BagInterface` 中的规范，我们将根据删除是否成功来返回 `true` 或 `false`。

假设包不是空的，我们搜索数组项，直到在数组中找到该条目或记录下它在数组中的位置。图 3-4 展示了处理后的数组。

## 图 3-4

成功搜索字符串 "Alice" 后的数组项

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| 数组索引 | Doug | Alice | Nancy | Ted | Vandee | Sue | |

![](img/d0cb86b2f18b2db569968ad7c743510e_133_0.png)

视频笔记
ArrayBag 方法

## 108 第 3 章 基于数组的实现

FIGURE 3-5 (a) 在删除 `items[index]` 中的条目并递减 `itemCount` 后数组项中的空隙；(b) 移动后续项以避免空隙；(c) 移动后的数组

![](img/d0cb86b2f18b2db569968ad7c743510e_134_0.png)

| | 12 | 3 | 19 | 100 | .... | 5 | 10 | 18 | ? | ? |
|---|---|---|---|---|---|---|---|---|---|---|
| itemCount items | | 0 | 1 | 2 | 3 | 4 | | k-1 | k | | maxItems-1 |

| 数组索引

| | 12 | 3 | 19 | .... | 5 | 10 | 18 | ? | .... | ? |
|---|---|---|---|---|---|---|---|---|---|---|
| itemCount items | | 0 | 1 | 2 | 3 | 4 | | k-1 | k | | maxItems-1 |

| | 12 | 3 | 100 | .... | 5 | 10 | 18 | ? | ? |
|---|---|---|---|---|---|---|---|---|---|
| itemCount items | | 0 | 1 | 2 | 3 | | k-1 | | | maxItems-1 |

现在如何从数组中删除项。你可以将其置空，但这种策略会导致数组中出现空隙，如图 3-5a 所示。充满空隙的数组有三个显著问题：

- `itemCount - 1` 不再是数组中最后一个项的索引。你需要另一个变量 `lastPosition` 来包含此索引。
- 由于项是分散的，方法可能必须查看数组的每个元素，即使只存在几项项也是如此。
- 当 `items[maxItems-1]` 被占用时，空隙可能看起来是满的，即使项的数量少于 `maxItems`。

我们可以通过将每个后续条目复制到数组中的前一个元素中来解决这个问题，从被删除项之后的条目开始，到最后一个结束，如图 3-5b 所示。然而，这种耗时的方法并不是必要的。记住，我们并不要求维护包条目的任何特定顺序。因此，与其在删除条目后移动条目，我们可以用数组中的最后一个项替换被删除的条目，如下。在 `items[index]` 中定位 `aEntry` 后（如图 3-6a 所示），我们将 `items[itemCount-1]` 中的条目复制到 `items[index]`，然后通过递减 `itemCount` 来忽略 `items[itemCount-1]` 中的条目。

从包中移除空隙需要以下伪代码。在数组中使用它之前，我们计算一次 `itemCount–1` 而不是两次。

```
在数组 items 中搜索 anEntry
if (anEntry 位于包的 items[index]) 
    递减 itemCount
```

## ADT Bag 的基于数组的实现

```
items[index] = items[itemCount-1]
decrement itemCount
return true
}
else
return false
```

对 `anEntry` 的搜索与 `contains` 方法相同，但我们想知道该条目是否存在以及它在数组中的位置。这就是为什么我们使用上一节中定义的 `getIndexOf` 方法。头文件中 `getIndexOf` 的实现如下：

```cpp
template<class ItemType>
int getIndexOf(const ItemType& target) const
{
  bool found = false;
  int result = -1;
  int searchIndex = 0;

  while (searchIndex < itemCount)
  {
    if (items[searchIndex] == target)
    {
      found = true;
      result = searchIndex;
    }
    else
    {
      searchIndex++;
    }
  }
  return result;
}
```

## 图 3-6 避免数组中的空隙

![](img/d0cb86b2f18b2db569968ad7c743510e_135_0.png)

## 3.2.6 测试

为了测试我们完成的类，可以在 `bagTester` 中添加以下语句：

```cpp
cout << "contains("Alice");
```

