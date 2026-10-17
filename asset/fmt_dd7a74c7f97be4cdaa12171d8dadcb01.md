
`template <typename Key, typename E>`

```cpp
class TTNode {             // 2-3 树节点结构
public:
    E lval;                  // 节点的左记录
    Key lkey;               // 左记录的键
    E rval;                 // 节点的右记录
    Key rkey;               // 右记录的键
    TTNode* left;           // 指向左子节点的指针
    TTNode* center;         // 指向中间节点的指针
    TTNode* right;          // 指向右子节点的指针
TTNode() {
    center = left = right = NULL;
    lkey = rkey = EMPTYKEY;
}
TTNode(Key lkey, E lval, Key rkey, E rval, TTNode<Key, E>* p1, TTNode<Key, E>* p2, TTNode<Key, E>* p3) {
    lkey = lkey; rkey = rkey;
    lval = lval; rval = rval;
    left = p1; center = p2; right = p3;
}
TTNode() {
    bool isLeaf() { return left == NULL; }
TTNode<Key, E>*(it);
};
```

图 10.10 2-3 树的实现。

第 5.3.1 节的技术可以应用于此处来实现独立的内部节点和叶子节点类型。

通过 2-3 树的定义规则，我们可以推导出树节点数量与深度之间的关系。高度为 $k$ 的 2-3 树至少有 $2^{k-1}$ 个叶子节点，因为每个内部节点退化为完全二叉树形状。高度为 $k$ 的 2-3 树最多有 $3^{k-1}$ 个叶子节点，因为每个内部节点最多有三个子节点。

在 2-3 树中搜索值与在二叉搜索树中搜索相似。搜索从根节点开始。如果根节点不包含搜索键 K，则搜索进入可能包含 K 的唯一子树。根节点中存储的值决定了哪个子树是正确的。例如，在图 10.9 的树中搜索值 30，我们从根节点开始。因为 30 于 18 和 33 之间，它只可能在中间子树中。搜索节点的中间孩子即可所需的记录。搜索 15，第一步仍然是搜索根节点。因为 15 小于 18，所以取第一个（左侧）分支。在下一层，我们取第二个分支到达包含 15 的叶子节点。如果搜索键是 16，在遇到叶子节点 15 时，我们会发现搜索键不在树中。图 10.11 是 2-3 树搜索方法的实现。

# 第 10 章 索引

```cpp
// 查找与给定键值匹配的记录
template <typename key, typename E>
E TTTreeNode<key, E>* root, key k) const {
    if (root == NULL) return NULL; // 未找到值
    if (k < root->lkey) return root->lval;
    if (k > root->rkey) return root->rval;
    if (k < root->lkey) // 向左移动
        return findhelp(root->left, k); // EMPTYKEY
    else if (root->center) // 二子节点节点
        return findhelp(root->center, k); // 向中间移动
    else if (k < root->rkey) // 向中间移动
        return findhelp(root->center, k);
    else return findhelp(root->right, k); // 向右移动
}
```

图 10.11 2-3 树方法的实现。

![](img/0ae21f56d72533acf0527c86ba21e1e6_380_0.png)

图 10.12 向图 10.9 的 2-3 树简单插入。值 14 被插入到包含 15 的节点的叶子节点中。因为节点中有空间容纳第二个键，它被简单地添加到左侧，并将 15 移动到右侧位置。

向 2-3 树中插入与向二叉搜索树中插入相似，相似之处在于新记录被放置在适当的叶子节点中。与二叉搜索树插入不同，会创建一个新节点来保存插入的记录，也就是说，2-3 树不会向下增长。第一步是找到如果记录在树中本应包含它的叶子节点。如果该叶子节点只包含一个值，则可以将新记录添加到该节点中，而无需修改树，如图 10.12 所示。在这个示例中，插入了一个键值为 14 的记录。从根开始搜索，我们到达存储 15 的叶子节点。我们将 14 作为左值添加（将记录 15 推到最右侧位置）。

如果我们把新记录插入到已经包含两个记录的叶子节点 L 中，则必须创建更多空间。考虑 L 的两个记录和要插入的记录，而不必考虑哪两个已经在 L 中，哪一个是新记录的。第一步是将 L 分拆为两个节点。因此，必须创建一个新节点——称之为 L'。L' 接收这三个中最大的一个。

# 第 10.4 节 2-3 树

![](img/0ae21f56d72533acf0527c86ba21e1e6_381_0.png)

**图 10.13** 2-3 树节点分裂的示例。

2-3 树的插入和删除例程不在树的底部添加节点。相反，它们会导致叶子节点分裂或合并，引起向根节点移动的涟漪效应。如果必要，根节点将分裂，导致新根节点的创建并使树深一层。如果根的最后两个孩子合并，根节点将被移除，树将失去一级。无论何种，所有叶子节点始终处于同一层。当所有叶子节点都处于同一层时，我们说树是**高度平衡的**。因为 2-3 树是高度平衡的，并且每个内部节点至少有两个子节点，我们知道树的最大深度为 $\log n$。因此，2-3 树的插入和删除操作需要 $\Theta(\log n)$ 时间。

从 2-3 树中删除记录时，有三种情况需要考虑。最简单的情况是从包含两个记录的叶子节点中删除记录。在这种情况下，记录被简单地移除，不会影响其他节点。第二种情况发生在叶子节点中的唯一记录被移除时。第三种情况发生在从内部节点中删除记录时。在第二和第三种情况下，被删除的记录会被另一个可以替代它并保持顺序的记录替换。如果树足够稀疏，则没有这样的记录可用。在这种情况下，兄弟节点将合并。2-3 树的删除操作过于复杂，将不再进一步描述。相反，对删除的完整讨论将推迟到下一节，在其中可以对 B 树进行泛化。

![](img/0ae21f56d72533acf0527c86ba21e1e6_382_0.png)

**图 10.14** 插入导致 2-3 树分裂的示例。
(a) 值 19 被插入到图 10.9 的 2-3 树中。这导致包含 20 和 21 的节点分裂，提升了 20。(b) 反而导致包含 23 和 30 的内部节点分裂，提升了 23。(c) 最后，树根节点分裂，使 23 成为新根中的左记录。结果是树高了一层。

## 10.5 B 树

本节介绍 B 树。B 树通常归功于 R. Baker 和 E. McCright，他们在 1972 年的一篇论文中描述了 B 树。B 树已经

## 第 10.5 节 B 树

```cpp
template <typename Key, typename E>
TTNode<Key, E>* TTTree<Key, E>::insert() :
  insertleft(TTNode<Key, E>* rt, const Key k, const E e) {
    TTNode<Key, E>* ret;
    if (rt == NULL) // 空树：为根创建一个叶子节点
      return new TTNode<Key, E>(k, e, EMPTYKEY, NULL,
                                NULL, NULL, NULL);
    if (rt->isleaf()) // 在叶子节点：在此插入
      return rt->add(new TTNode<Key, E>(k, e, EMPTYKEY,
                                NULL, NULL, NULL));
  } // 添加到内部节点
  if (k < rt->rkey) {
    retval = insertleft(rt->left, k, e);
    if (retval == rt->left) return rt;
    else rt->add(retval);
  } else if (k == rt->rkey || (k > rt->rkey)) {
    retval = insertcenter(rt->center, k, e);
    if (retval == rt->center) return rt;
    else rt->add(retval);
  } else { // 向右插入
    retval = insertright(rt->right, k, e);
    if (retval == rt->right) return rt;
    else rt->add(retval);
  }
```

图 10.15 2-3 树插入例程。除了哈希方法之外，B 树或其变体是用于插入、删除和范围搜索的标准文件组织。它们有效地解决了实现基于磁盘的树时遇到的大部分问题：

- B 树是平衡的，所有叶子节点都在同一层。
- 更新和搜索操作只影响少量磁盘块。影响的块越少，需要的磁盘 I/O 就越少。
- B 树将记录（即键值相似的记录）保持在同一个磁盘块中，由于局部性原理有助于减少搜索时的磁盘 I/O。
- B 树保证树中的每个节点至少是满的。

一个阶数为 *m* 的 B 树具有以下属性：

- 根节点要么是一个叶子节点，要么至少有两个子节点。
- 每个内部节点介于 [m/2] 和 *m* 个子节点之间。

```cpp
// 向节点添加一个新的键值对。这种信息
// 以 2-3 树节点的形式出现，一个键和一个（可能为空的）子树
// 通过 center 指针连接；
template <typename Key, typename E>
Node<Key, E>* insert(TTNode<Key, E>* it, Key rval, Key lkey) {
  if (rkey < it->lkey) { //只有一个键，在此添加
    if (lkey < it->lkey) {
      rkey = it->lkey; rval = it->lval;
      right = center; center = it->center;
    }
    else {
      rkey = lkey; rval = lval; right = center;
      lkey = it->left; lval = it->lval;
      center = it->center;
    }
    return this;
  } else if (lkey >= it->lkey) { // 添加左侧
    center = new TTNode<Key, E>(rkey, rval, EMPTYKEY, NULL, center, right);
    rkey = EMPTYKEY; rval = NULL; right = NULL;
    it->left = left; left = it;
    return this;
  } else if (rkey < it->ikey) { // 添加中间
    it->center = new TTNode<Key, E>(rkey, rval, EMPTYKEY, NULL, it->center, right);
    it->left = this;
    rkey = EMPTYKEY; rval = NULL;
    return it;
  } else { // 添加右侧
    Node<Key, E>* N1 = new TTNode<Key, E>(rkey, rval, EMPTYKEY, NULL, this, NULL);
    it->left = right;
    right = NULL; rkey = EMPTYKEY; rval = NULL;
    return N1;
  }
}
```

图 10.16 2-3 树节点的 `add` 方法。

![](img/0ae21f56d72533acf0527c86ba21e1e6_385_0.png)

图 10.17 一个阶数为四的 B 树。

- 树中的所有叶子节点都在同一层，因此树始终是平衡的。

B 树是 2-3 树的泛化。另一种说法，2-3 树是阶数为三的 B 树。

## 第 10.5 节 B 树

![](img/0ae21f56d72533acf0527c86ba21e1e6_387_0.png)

**图 10.18** 四阶 B+-树的示例。内部节点必须存储二到四个子节点。对于此示例，假设记录的大小使得叶节点可以存储三到五条记录。

以形成一个双向链表。因此，可以通过访问链表上的所有叶节点来按排序顺序遍历整个记录集合。这里是 B+-树节点类的 C++ 风格伪代码。叶节点子类和内部节点子类将实现此基类。

```cpp
// B+-树的抽象类定义
template <typename Key, typename E> class BPNode {
public:
    BPNode* fptr; BPNode* rptr; // 指向兄弟节点的链接
    virtual BPNode(); // 基类析构函数
    virtual bool isLeaf() const = 0; // 如果节点是叶节点则为真
    virtual bool isFull() const = 0; // 如果节点已满则为真
    virtual int numKeys() const = 0; // 当前键的数量
    virtual Key* keys() const = 0; // 返回键数组
```

需要注意的实现细节是，图 10.17 显示内部节点包含三个键和四个指针；`BPNode` 略有不同，因为它存储的是“键-指针”对。图 10.17 显示的是传统画法的 B+-树。为了简化实际中的实现，节点实际上与每个指针关联。应该假设每个内部节点都持有该节点子树的最左侧位置，即该值小于或等于子树中的任何键值。B+-树通常在最左侧的叶节点中存储一个额外的虚拟记录，其键小于任何合法的键值。

B+-树非常适合范围查询。一旦找到了范围内的记录，就可以通过顺序处理第一个节点中的剩余记录，然后根据需要继续继续遍历叶节点链表，来访问范围内具有相应键的其余记录。图 10.18 展示了 B+-树。

在 B+-树中搜索与在普通 B 树中搜索几乎相同，区别在于搜索必须始终持续到正确的叶节点。即使在内部节点中找到了搜索键值，它也只是一个占位符，并不提供访问实际记录的方法。要在图 10.18 的 B+-树中找到值为 33 的记录，搜索从根节点开始。根节点中存储的值 33 仅作为占位符，表示在第二个子树中找到了值大于或等于 33 的键。从根节点的第二个孩子开始，采取第一个分支到达包含键值为 33 的实际记录（或指向实际记录的指针）的叶节点。图 10.19 显示了 B+-树搜索算法的伪代码草图。

```cpp
template <typename Key, typename E>
E BPTTree<Key, E>::findhelp(BPNode<Key, E>** rt, const Key k) const {
    int currec = binarySearch(rt->keys(), rt->numrecs(), k);
    if (rt->isLeaf()) {
        if (((BPLe<Key, E>*)rt)->keys()[currec] == k)
            return ((BPLe<Key, E>*)rt)->recs(currec);
        else return NULL;
    } else {
        return findhelp(((BInternal<Key, E>*)rt)->pointers(currec), k);
    }
}
```
