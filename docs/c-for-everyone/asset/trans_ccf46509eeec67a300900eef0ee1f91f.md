
```cpp
int Heap::size() const
{
    return elements.size() - 1;
}

void Heap::fix_heap()
{
    int root = elements[1];

    int last_index = elements.size() - 1;
    // Promote children of removed root while they are larger than last

    int index = 1;
    bool more = true;
    while (more)
    {
        int child_index = get_left_child_index(index);
        if (child_index <= last_index)
        {
            // Get larger child

            // Get left child first
            int child = get_left_child(index);

            // Use right child instead if it is larger
            if (get_right_child_index(index) <= last_index
                && get_right_child(index) > child)
            {
                child_index = get_right_child_index(index);
                child = get_right_child(index);
            }

            // Check if smaller child is larger than root
            if (child > root)
            {
                // Promote child
                elements[index] = child;
                index = child_index;
            }
            else
            {
                // Root is larger than both children
                more = false;
            }
        }
        else
        {
            // No children
            more = false;
        }
    }

    // Store root element in vacant slot
    elements[index] = root;
}

int Heap::get_left_child_index(int index)
{
    return 2 * index;
}
```

## 自测

![](img/5e58fb4c840712efd6ed6fa82bb97f57_634_0.png)

**19.** 我们能否将二叉搜索树存储在数组中，以便通过查看数组位置 2 * index + 1 和 2 * index + 2 来快速定位子节点？

**20.** 考虑以下排序算法。设 a 是一个有 n 个元素的数组。在第一阶段，将 a[0]、a[1] 等插入存储在同一数组中的堆。（经过 k 次插入后，堆占据数组的前 k 个元素，尚未插入的元素占据剩余的 n − k 个元素。）在第二阶段，不断从堆中删除最大元素，并将其存储到堆末尾的空缺位置，即 a[n − 1]、a[n − 2] 等位置。该算法的效率如何？

**21.** 自测 20 中描述的算法相比归并排序算法有什么优势？

**22.** 考虑以下堆

```
        10
      9     8
    7   6   5   4
  3   2   1
```

插入值 11 后，堆是什么？

**23.** 考虑以下堆

```
        10
      9     8
    7   6   5   4
  3   2   1
```

移除最大值后，堆是什么？

**24.** 数组 1 2 3 4 5 6 7 8 9 10 和 10 9 8 7 6 5 4 3 2 1 分别对应什么二叉树？其中哪一个是最大堆？

**动手实践** 现在你可以尝试本章末尾的这些练习：P14.17、P14.18。

## 本章小结

### 描述集合数据类型及其在 C++ 库中的实现。

- 集合是不同元素的无序集合。
- 集合没有重复元素。添加一个已经存在的重复元素会被忽略。
- 标准 C++ 的 set 类按有序顺序存储值。
- 多重集合（或包）与集合类似，但元素可以出现多次。

### 解释二叉搜索树的实现及其性能特征。

- 二叉树由节点组成，每个节点至多有两个子节点。
- 二叉搜索树中的所有节点都满足以下性质：左侧后代的数据值小于该节点的数据值，右侧后代的数据值更大。
- 要在二叉搜索树中插入一个值，可将其递归地插入左子树或右子树。
- 从二叉搜索树中删除只有一个子节点的节点时，由该子节点替换要删除的节点。
- 从二叉搜索树中删除有两个子节点的节点时，用右子树中最小的节点替换它。
- 如果二叉搜索树是平衡的，那么插入一个元素需要 O(log(n)) 时间。
- 树的遍历方案包括前序遍历、中序遍历和后序遍历。

### 描述映射数据类型及其在 C++ 库中的实现。

- 映射保存键对象和值对象之间的关联。
- 多重映射可以让同一个键关联多个值。

### 描述优先队列数据类型的行为。

- 从优先队列中删除元素时，会取出优先级最高的元素。

### 描述堆数据结构及其操作的效率。

- 堆是一棵几乎完全树，其中所有节点的值至少与其后代的值一样大。
- 插入或删除堆元素是 O(log(n)) 操作。
- 堆的规则布局使得可以高效地将堆节点存储在数组中。

## 复习练习

- **R14.1** 学校网站维护一个在学生计算机上被阻止的网站集合。检查被阻止网站的程序应使用 vector、链表、list 还是 set 来存储网站地址？
- **R14.2** 图书馆想跟踪哪些书被借给了哪些读者。他们应使用从书到读者的 map 还是 multimap？
- **R14.3** 图书馆想跟踪哪些读者借了哪些书。他们应使用从读者到书的 map 还是 multimap？
- **R14.4** 在急诊中，会为每位接诊病人建立病例记录，描述病例的严重程度。当医生有空时，他们先处理最严重的病例。病例记录应存储在 set、map 还是优先队列中？
- **R14.5** 你为科学实验保存一组 Point 对象。（Point 有 x 和 y 坐标。）定义一个合适的 `operator<`，以便可以构成 `set<Point>`。
- **R14.6** `set<T>` 可以实现为节点存储 T 类型数据的二叉树。如何实现 `multiset<T>`？
- **R14.7** 二叉树和二叉搜索树有什么区别？各举一个例子。
- **R14.8** 平衡树和不平衡树有什么区别？各举一个例子。
- **R14.9** 将以下元素插入二叉搜索树。画出每次插入后得到的树。

  - 亚当
  - 夏娃
  - 罗密欧
  - 朱丽叶
  - 汤姆
  - 黛安娜
  - 哈利

- **R14.10** 按相反顺序插入练习 R14.9 的元素。然后确定 `BinarySearchTree.print` 函数如何打印练习 R14.9 中的树和这棵树。解释打印结果之间有何关系。
- **R14.11** 考虑以下树。`BinarySearchTree.print` 函数按什么顺序打印节点？

  ![](img/5e58fb4c840712efd6ed6fa82bb97f57_636_0.png)

- **R14.12** 集合如何实现快速的插入和删除执行？
- **R14.13** 二叉树的哪些性质使它成为搜索树？哪些性质使它成为平衡树？
- **R14.14** map 与 vector 有何相似之处？有何不同？
- **R14.15** 为什么优先队列严格来说不是队列？
- **R14.16** 证明高度为 *h* 的堆至少包含 2<sup>h−1</sup> 个元素，但少于 2<sup>h</sup> 个元素。
- **R14.17** 假设堆节点存储在数组中，从索引 1 开始。证明索引为 *i* 的堆节点的子节点索引为 2 · *i* 和 2 · *i* + 1，而索引为 *i* 的节点的父堆节点索引为 *i*/2。

## 编程练习

**P14.1** 使用 `map<int, double>` 存储系数，重新实现练习 P13.14 中的 `Polynomial` 类。

**P14.2** 编写函数

```cpp
set<int> set_union(set<int> a, set<int> b)
set<int> intersection(set<int> a, set<int> b)
```

它们计算集合 a 和 b 的并集和交集。（不要将第一个函数命名为 `union`——那是 C++ 中的保留字。）

