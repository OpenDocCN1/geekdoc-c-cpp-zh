

## 图 2-9 伪代码中 writeBackward2("cat") 的框跟踪（续）

Enter writeBackward2 with string:
Leave writeBackward2 with string:
About to write first character of string: t
Leave writeBackward2 with string: t

![](img/288a0c22d14d2450c1e772f228f867b0_92_0.png)

此调用完成执行，并返回。

输出流：

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t
Enter writeBackward2 with string:
Leave writeBackward2 with string:
About to write first character of string: t
t
Leave writeBackward2 with string: t
Leave writeBackward2 with string: at
About to write first character of string: at
a
Leave writeBackward2 with string: at

![](img/288a0c22d14d2450c1e772f228f867b0_92_1.png)

此调用完成执行，并返回。

输出流：

Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t
Enter writeBackward2 with string:
Leave writeBackward2 with string:
About to write first character of string: t
t
Leave writeBackward2 with string: t
Leave writeBackward2 with string: at
About to write first character of string: at
a
Leave writeBackward2 with string: at
About to write first character of string: cat
c
Leave writeBackward2 with string: cat

问题 3 给定一个整数 n > 0，编写一个递归函数 countDown，它输出整数 n, n - 1, ..., 1。提示：你可以完成什么任务，以及可以请朋友为你完成什么任务？

## 2.4 与数组的递归

当你使用数组时，递归可以是一个实用且强大的工具。作为我们的第一个示例，我们将数组的内容逆序写出。然后我们将探讨几个涉及搜索数组的问题。

![](img/288a0c22d14d2450c1e772f228f867b0_93_0.png)

### 2.4.1 以逆序写出数组的条目

此问题的解决方案与我们在 2.3.1 节中编写逆序字符串时的第一个解决方案非常相似。我们可以编写以下伪代码：

```
writeArrayBackward(anArray: char[])
    if (the array is empty)
        Do nothing--this is the base case
    else
    {
        Write the last character in anArray
        writeArrayBackward(anArray minus its last character)
    }
```

我们如何将去掉最后一个字符的 anArray 传递给 writeArrayBackward？我们可以传递数组中剩余的字符数。在每次递归调用中，我们将此数字减 1。或者，我们可以传递最后一个字符的索引。也就是说，如果 last 是此索引，writeArrayBackward 将作用于数组 anArray[0..last]，即从 anArray[0] 到 anArray[last] 的部分。随后的递归调用将作用于子数组 anArray[0..last - 1]。此思想的更一般变体还传递第一个数组字符的索引。因此，我们不再假设此索引为 0，而是将 anArray[first..last] 传递给 writeArrayBackward。

我们可以按如下方式编写函数 writeArrayBackward：

```
/** Writes the characters in an array backward.
   @param anArray  The array contains size characters, where size > 0.
   @param first    The index of the first character in the array.
   @param last     The index of the last character in the array. */
void writeArrayBackward(const char anArray[], int first, int last)
{
    if (first <= last)
    {
        // Write the last character
        cout << anArray[last];

        // Write the rest of the array backward
        writeArrayBackward(anArray, first, last - 1);
    } // end if

    // first > last is the base case - do nothing
} // end writeArrayBackward
```

问题 4 在 writeArrayBackward 的先前定义中，为什么当 first 的值超过 last 的值时会出现基本情况？
问题 5 编写一个递归函数，计算并返回数组中前 n（n >= 1）个实数的乘积。
问题 6 说明你为上一个问题编写的函数如何满足递归函数的属性。
问题 7 编写一个递归函数，计算并返回数组 anArray[first..last] 中整数的乘积。

### 2.4.2 二分查找

搜索是一项经常发生的重要任务。通常，搜索是针对数组中的特定条目。我们现在将考察几个具有递归解决方案的搜索问题。我们的目标是进一步加深你对递归的理解。

本章最初通过直观的方法介绍二分查找算法，从高层次上展示了一种在字典中查找单词的方法。我们现在将充分开发此算法，并说明一些重要的编程问题。

回顾字典问题的先前解决方案：

```
search(aDictionary: Dictionary, word: string)
if (aDictionary is one page in size)
    Scan the page for word
else
    {
    Open aDictionary to a point near the middle
    Determine which half of aDictionary contains word
    if (word is in the first half of aDictionary)
        search(first half of aDictionary, word)
    else
        search(second half of aDictionary, word)
    }
```

![](img/288a0c22d14d2450c1e772f228f867b0_94_0.png)

现在稍微修改问题，在整数数组 anArray 中搜索给定值（即目标值）。数组（如同字典）必须已排序，否则二分查找不适用。因此，假设

```
anArray[0] anArray[1] anArray[2] ... anArray[size - 1]
```

其中 size 是数组的大小。针对数组问题的高级二分查找为

```
binarySearch(anArray: ArrayType, target: ValueType)
if (anArray is of size 1)
    Determine if anArray's value is equal to target
else
    {
    Find the midpoint of anArray
    Determine which half of anArray contains target
    if (target is in the first half of anArray)
        binarySearch(first half of anArray, target)
    else
        binarySearch(second half of anArray, target)
    }
```

尽管该解决方案在概念上是正确的，但在实现算法之前，你必须考虑几个细节：

- 1. 你如何将 anArray 的一半传递给 binarySearch 的递归调用？你可以在每次调用时传递整个数组，但让 binarySearch 仅搜索 anArray[first..last]，即从 anArray[first] 到 anArray[last] 的部分。因此，你还会将整数 first 和 last 传递给 binarySearch：

```
binarySearch(anArray, first, last, target)
```

按照此约定，新的中点由以下给出

```
mid = (first + last) / 2
```

然后 binarySearch( anArray 的第一半, target ) 变为

```
binarySearch(anArray, first, mid - 1, target)
```

而 binarySearch( anArray 的第二半, target ) 变为

```
binarySearch(anArray, mid + 1, last, target)
```

数组的两半为 anArray[first..mid-1] 和 anArray[mid+1..last]；两半都不包含 anArray[mid]

- 2. 你如何确定数组的哪一半包含 target？以下的一种可能实现

```
if (target is in the first half of anArray)
```

为

```
if (target < anArray[mid])
```

确定 anArray[mid] 是否是你要查找的目标

但是，target 与 anArray[mid] 之间没有相等性测试。此遗漏可能导致算法遗漏 target。在前一折半算法将 anArray 分成两半后，anArray[mid] 不在数组的任何一半中。（在这种情况下，两半并不构成一个整体！）因此，你现在必须确定 anArray[mid] 是否是你要查找的值；因为之后它将不在剩余的一半中。折半标准与终止条件（基本情况）之间的交互作用很微妙，并且常常是错误的根源。我们需要重新考虑基本情况。

- 3. 基本情况应该是什么？按当前编写，binarySearch 仅在出现大小为 1 的数组时终止；这是唯一的基本情况。通过更改折半过程，使 anArray[mid] 保留在两半中的一半，可以正确实现二分查找，使其仅具有这一个基本情况。但是，拥有两个不同的基本情况可能更清晰，如下所示：

  - first > last。当目标不在原始数组中时，你将达到此基本情况。
  - target == anArray[mid]。当目标在原始数组中时，你将达到此基本情况。

这些基本情况与你以前遇到的任何基本情况都有些不同。从某种意义上说，算法根据其达到的基本情况来确定问题的答案。许多搜索问题都有这种特点。

- 4. binarySearch 如何指示搜索结果？如果 binarySearch 在数组中成功定位目标，它可以返回等于目标的数组值的索引。由于此索引永远不会为负，如果在数组中未找到目标，binarySearch 可以返回一个负值。

以下的 C++ 函数 binarySearch 实现了这些想法。binarySearch 的两个递归调用标记为 X 和 Y，以便在以后对此函数的框跟踪中使用。

