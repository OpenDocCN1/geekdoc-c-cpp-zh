

在这个伪代码中，我们如何“修复整个树的根，使其不再有零个条目？”例如，我们可能有一个如下所示的树：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_591_0.png)

我们解决这个问题的方案是，首先设置一个指向唯一子节点的临时指针。接下来，将唯一子节点中的所有内容复制到根节点。最后，删除原始子节点。经过这种重新排列后，我们的树将少一层，如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_591_1.png)

根处的这种收缩（在 remove 成员函数内）是 B-tree 失去高度的唯一位置。现在我们面临的任务是设计 loose erase 函数。

## 从 B-Tree 中进行 Loose Erase

私有 loose_erase 函数的启动方式与 count 和 insert 函数相同，即查找第一个索引 i，使得 data[i] 不小于目标值。一旦找到此索引，就存在四种可能性，如下所示：

```
// Removing a target entry from a set (loose erase)
1. Make a local variable, i, equal to the first index such that data[i] is not less than target. If there is no such index, then i equal to data_count, indicating that all of the entries are less than the target.
2. Deal with one of these four possibilities:
2a. The root has no children, and we did not find the target: In this case, there is no work to do, since the target is not in the set (return false).
2b. The root has no children, and we found the target: In this case, remove the target from the data array, and return true.
2c. The root has children, and we did not find the target (see following).
2d. The root has children, and we found the target (see following).
```

情况 2c 和 2d 需要进一步完善。

案例 2c。在这种情况下，我们在根中未找到目标，但目标仍可能出现在 subset[i] 中。我们将进行递归调用（并保存其答案以便我们自己返回）：

```
subset[i]->loose_erase(target)
```

此调用将从 subset[i] 中删除目标，但随后我们面临的问题是 subset[i] 的根可能只有 MINIMUM - 1 个条目。如果是这样，我们将通过调用另一个私有成员函数来修复问题，其规格说明如下：

```
template <class Item>
void set<Item>::fix_shortage(std::size_t i);
// Precondition: (i < child_count) and the entire B-tree is valid EXCEPT that
//    subset[i] has MINIMUM - 1 entries.
// Postcondition: The tree has been rearranged so that the entire B-tree is
//    valid EXCEPT that the number of entries in the root of this set might be
//    one less than the allowed minimum.
```

我们稍后将探讨 fix_shortage 的设计。

案例 2d。在这种情况下，我们在根中找到了目标，但不能简单地从 data 数组中删除它，因为下面有子节点（删除条目将违反第 549 页的 B-Tree Rule 4）。相反，我们将进入 subset[i] 并删除该子集中的最大项。我们将复制这个最大项并将其放入 data[i]（其中包含目标）。总效果与删除目标相同。

例如，假设我们在此 B-tree 的根中在 data[1] 处找到了目标 28：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_592_0.png)

我们的计划是进入 subset[1]，删除最大项（26），并将这个 26 的副本放在目标之上。执行这些步骤后，B-tree 不再包含 28：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_592_1.png)

从 subset[i] 删除最大项并将最大项的副本放入 data[i] 的组合，可以通过调用另一个新的私有成员函数 remove_biggest 来完成，其规格说明如下：

```
template <class Item>
void set<Item>::remove_biggest(Item& removed_entry);
// Precondition: (data_count > 0) and the entire B-tree is valid.
// Postcondition: The largest item in the set has been removed, and a copy
//    of this removed entry has been placed in removed_entry. The entire
//    B-tree is still valid, EXCEPT that the number of entries in the root of this
//    set might be one less than the allowed minimum.
```

通过使用 remove_biggest，步骤 2d 的大部分可以通过一个函数调用完成：

```
subset[i]->remove_biggest(data[i]);
```

此函数调用返回后，我们已从 subset[i] 中删除了最大条目，并将该项的副本放入 data[i]（替换目标）。剩下的工作是修复 subset[i] 根中可能出现的短缺（因为 subset[i]->remove_biggest 的后置条件允许 subset[i] 的根最终具有 MINIMUM - 1 个条目的可能性）。我们如何修复这种短缺？我们可以使用在步骤 2c 末尾使用的同一个 fix_shortage 成员函数。因此，步骤 2d 的完整代码如下：

```
subset[i]->remove_biggest(data[i]);
if (subset[i]->data_count < MINIMUM)
    fix_shortage(i);
return true; // Indicate that we removed the target.
```

我们还有两个问题需要处理：fix_shortage 和 remove_biggest 的设计。

## 修复子节点短缺的私有成员函数

当调用 fix_shortage(i) 时，我们知道 subset[i] 只有 MINIMUM - 1 个条目。我们如何纠正这个问题？你可以考虑四种情况：

- fix_shortage 的情况 1：从 subset[i-1] 转移一个额外条目。

假设 subset[i-1] 具有超过最小数量的条目。然后我们可以执行这些转移：

- a. 将 data[i-1] 向下转移到 subset[i]->data 的前面。记住要移动现有条目以腾出空间，并将 subset[i]->data_count 加一。

fix_shortage 伪代码的四种情况

- b. 将 subset[i-1]->data 的最后一项向上转移以替换 data[i-1]，并从 subset[i-1]->data_count 减一。

- c. 如果 subset[i-1] 有子节点，则将 subset[i-1] 的最后一个子节点转移到 subset[i] 的前面。这涉及移动现有数组 subset[i]->subset 以在 subset[i]->subset[0] 处为新的子节点指针腾出空间。同时将 subset[i]->child_count 加一，并从 subset[i-1]->child_count 减一。

例如，让我们为这棵树（MINIMUM 设置为 2）调用 fix_shortage(2)：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_594_0.png)

在此示例中，我们需要修复只有一个条目的 subset[2]。按照上述步骤，我们可以从 subset[1] 转移一个条目。这个被转移的条目是 22，它被传递到 data[1]，而 28（来自 data[1]）下移成为问题节点的新第一个条目。还有一个子节点从 subset[1] 的末尾转移到 subset[2] 的前面，如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_594_1.png)

### fix_shortage 的情况 2：从 subset[i+1] 转移一个额外条目。

另一种可能性是从 subset[i+1] 转移一个额外条目。工作与你刚才看到的从 subset[i-1] 转移条目的工作类似。

### fix_shortage 的情况 3：将 subset[i] 与 subset[i-1] 合并。

假设 subset[i-1] 存在（换句话说，i > 0），但它只有 MINIMUM 个条目。在这种情况下，我们无法从 subset[i-1] 转移条目，但可以将 subset[i] 与 subset[i-1] 合并。合并分三步进行：

- a. 将 data[i-1] 向下转移到 subset[i-1]->data 的末尾。这实际上从根中删除了该项，因此将 data[i]、data[i+1] 等向左移动以填补空隙。同时记得从 data_count 减一，并将 subset[i-1]->data_count 加一。

- b. 将 subset[i] 的所有项和子节点转移到 subset[i-1] 的末尾。记住更新 subset[i-1]->data_count 和 subset[i-1]->child_count 的值。同时将 subset[i]->data_count 和 subset[i]->child_count 设置为零。

- c. 删除节点 subset[i]，并将 subset[i+1]、subset[i+2] 等向左移动以填补空隙。同时将 child_count 减一。

例如，让我们为这棵树（MINIMUM 设置为 2）调用 fix_shortage(2)：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_595_0.png)

在此示例中，subset[2] 与其左侧的兄弟节点合并。在合并过程中，28 也从根下移，成为合并节点的左侧条目。结果是以下树：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_595_1.png)

如你所见，这棵树在其自身根中条目过少，但这没关系，因为 fix_shortage 的后置条件允许结果树的根具有比所需数量少一个条目。

### fix_shortage 的情况 4：将 subset[i] 与 subset[i+1] 合并。

我们的第四种情况是将问题子集与 subset[i+1] 合并。工作与你刚才看到的与 subset[i-1] 合并的工作类似。

你现在有足够的信息来编写 fix_shortage 成员函数。你应该强调清晰的逻辑结构来确定哪四种情况是合适的。如果你为四种情况中的每一种提供四个新的私有成员函数来执行实际工作，你的实现会更加清晰。

