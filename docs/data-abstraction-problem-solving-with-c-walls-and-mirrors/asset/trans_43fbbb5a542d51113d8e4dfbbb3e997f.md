

```cpp
i = h(searchKey)
if (hashTable[i] == nullptr)
hashTable[i] = p
{
    // 将新项添加到链的头部
    p->setNext(hashTable[i])
    hashTable[i] = p
}
return true
```

请记住，我们假设给定的键不在字典中。
HashedDictionary 实现文件中 `add` 的定义如下：

```cpp
template <class KeyType, class ItemType>
bool HashedDictionary<KeyType, ItemType>::add(const ItemType& newItem,
                                                                    const KeyType& searchKey)
{
    // 创建字典条目
    HashedEntry<KeyType, ItemType> *entryToAddPtr = new HashedEntry<KeyType, ItemType>(newItem);
    // 计算数组的哈希索引
    int itemHashIndex = getHashIndex(searchKey);
    // 添加到 itemHashIndex 处的链
    if (hashTable[itemHashIndex] == nullptr)
    {
        hashTable[itemHashIndex] = entryToAddPtr;
    } else
    {
        entryToAddPtr->setNext(hashTable[itemHashIndex]);
        hashTable[itemHashIndex] = entryToAddPtr;
    } // end if
    return true;
} // end add
```

`remove` 方法。要根据给定键从字典中删除条目，请按照以下伪代码所示的操作：

```cpp
remove(searchKey: KeyType): boolean
i = h(searchKey)
if (hashTable[i] != nullptr)
{
    // 在 hashTable[i] 指向的链中搜索 searchKey
    if (searchKey 在第一个节点中)
    {
        p = hashTable[i]
        hashTable[i] = hashTable[i]->getNext()
        delete p
        return true
    }
} else
{
    curPtr = 指向包含 searchKey 的项的指针
    prevPtr = 指向链中上一个项的指针
    prevPtr->setNext(curPtr->getNext())
    delete curPtr
    return true
}
else
    return false
```

HashedDictionary 对 `remove` 的定义如下：

```cpp
template <class HashedKey, class ItemType>
bool HashedDictionary<HashedKey, ItemType>::remove(const KeyType& searchKey) {
    bool itemFound = false;
    // 计算数组的哈希索引
    int itemHashIndex = getHashIndex(searchKey);
    if (hashTable[itemHashIndex] != nullptr) {
        // 特殊情况 - 第一个节点是目标
        if (searchKey == hashTable[itemHashIndex]) {
            HashedEntry<HashedKey, ItemType>* entryToRemove = hashTable[itemHashIndex];
            hashTable[itemHashIndex] = hashTable[itemHashIndex]->getNext();
            delete entryToRemove; // 为了安全
            itemFound = true;
        }
        else // 搜索链的剩余部分
            HashedEntry<HashedKey, ItemType>* prevPtr = hashTable[itemHashIndex];
            HashedEntry<HashedKey, ItemType>* curPtr = prevPtr->getNext();
            while ((curPtr != nullptr) && !itemFound) {
                // 在链中找到要删除的项
                if (searchKey == curPtr->getKey()) {
                    prevPtr->setNext(curPtr->getNext());
                    delete curPtr;
                    curPtr = nullptr; // 为了安全
                    itemFound = true;
                }
                else // 查看链中的下一个项
                    prevPtr = curPtr;
                    curPtr = curPtr->getNext();
                } // end if
            } // end while
        } // end if
    }
    return itemFound;
} // remove
```

HashedDictionary 类的其余实现部分留作练习题。

# 总结

- 1. ADT 字典支持以值为导向的操作，例如“检索关于 John Smith 的所有信息”。
- 2. 字典的线性实现（基于数组和基于链表）仅在有限的情况下是合适的，例如当字典较小或对于某些操作时。在这些情况下，线性实现的简单性可能是一个优势。然而，字典的线性实现不适合作为一个通用的可重用类。
- 3. 基于非线性（二叉搜索树）的 ADT 字典实现提供了两种实现的最佳优点。基于链的实现允许字典动态增长，并允许通过指针更改而不是移动来进行数据的插入和删除。此外，二叉搜索树允许你在搜索具有特定值的项时使用类似于二分查找的算法。这些特性使得非线性字典在许多应用中远优于线性实现。
- 4. 哈希作为一种字典实现，计算的是数据项应该所在的位置，而不是去搜索它。哈希允许非常高效的检索、插入和删除。
- 5. 哈希函数应该极其容易计算——它只需要几次操作——并且应该将键散布在整个哈表中。
- 6. 当两个搜索键哈希到同一个数组时，就会发生冲突。解决冲突的方法有两种：探测（probing）和链法（chaining）。
- 7. 链法是时间效率最高的冲突解决方案。
- 8. 哈希不能高效地支持需要项排序的操作——例如，按排序顺序遍历表。
- 9. 当遍历等字典操作对特定应用不重要时，如果你知道字典项的最大数量，并且有充足的存储空间，哈希是更好的选择。

# 练习题

- 1. 实现第 18-2 所示的字典的实现。
- 2. 考虑 `replace(newItem, searchKey)`，如果字典包含该项，则替换它。
    a. 为 `ArrayDictionary`、`TreeDictionary` 和 `HashedDictionary` 实现 `replace`。
    b. 对于 `TreeDictionary`，在什么情况下可以替换项？（见第 16 节）
- 3. 想象一个像英语字典的程序。用户输入单词，程序通过哈希查找单词是否已出现。因此，哪种字典实现作为检索时效率最高？
- 4. 编译器使用符号表来跟踪标识符。当遇到标识符时如果是新的，将其插入表中。因此，字典需要频繁的插入和检索。哪种实现作为单词检查器效率最高？
- 5. 两个字典的并集（union）和交集（intersection）操作。每个操作返回一个新字典。提出并讨论这些操作的实现。
- 6. 虽然在某些应用程序中允许搜索键重复是合理的，但字典中的项可能与另一个字典具有相同的搜索键。修改实现以测试并不允许任何重复，而不是简单的假设它们不会发生。哪些字典操作会受到影响？对无排序线性实现有什么影响？
- 7. 虽然字典中允许重复搜索键是合理的，但对于某些应用程序，测试它们比假设它们不会发生要明智。
    a. 插入相同搜索键项的实现是什么？这对删除和检索操作有什么影响？
    b. 具有相同搜索键但不相同的项的实现是什么？具体来说 `add`、`remove` 和 `getitem` 会做什么？
- 8. 假设你想支持字典的删除操作——例如 `removeByName` 和 `removeByID`。描述这些的高效实现。
- 9. 重复第 8 题，但使用二叉搜索树组织一个搜索键，使用排序链来组织第二个键。
- 10. 当使用哈希和线性探测解决冲突时，你可以编写字典操作 `add`、`remove` 和 `getitem` 的伪代码吗？
- 11. 当使用哈希和链法解决冲突时，写出删除操作的伪代码。
- 12. 哈希表 ADT 实现的成功取决于良好哈希函数的选择。良好的哈希函数易于计算并均匀分布数据。评价以下哈希函数的合理性。哪些模式会哈希到同一个位置？
- 13. 哈希表大小为 2048。搜索键是英语单词。哈希函数是：
  $h(key) = (\text{单词字母在字母表中的位置之和}) \mod 2048$
- b. 哈希表大小为 2048。键是以字母开头的字符串。哈希函数是：
  $h(key) = (\text{键第一个字母在字母表中的位置}) \mod 2048$

因此，“BUT” 映射到 2。如果字符串是随机的，这个哈希函数有多合适？如果字符串是英语单词呢？

