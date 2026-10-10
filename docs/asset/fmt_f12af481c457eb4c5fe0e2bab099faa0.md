
```
// 查找给定坐标的记录

bool findhelp(BinNode<E>* root, int* coord,

E& e, int discrim) const {

// 节点的成员 "coord" 是一个整数数组，存储

// 节点的坐标

if (root == NULL) return false; // 空树

int* curcoord = (root->val())->coord();

if (equalCoord(curcoord, coord)) { // 找到了

    e = root->val();

    return true;

}

if (curcoord[discrim] < coord[discrim])

    return findhelp(root->left(), coord, e, (discrim+1)%D);

else

    return findhelp(root->right(), coord, e, (discrim+1)%D);

}
```

在 k-d 树中插入新节点类似于 BST 插入。遵循 k-d 搜索过程，直到找到 NULL 指针，这指示了插入新节点的正确位置。

**示例 13.6** 在图 11 所示的 k 树位置处插入记录，首先需要搜索到包含记录 B 的节点。此时，将记录插入到 B 的左子树中。

从 k-d 树中删除节点类似于从 BST 中删除，但稍微复杂一些。对于 BST，第一步是找到要删除的节点（称为 N）。然后需要找到 N 的一个后代，用于在树中替换 N。如果 N 没有子节点，则用 NULL 指针替换 N。注意，如果 N 有一个该子节点又有子节点，我们不能像 BST 那样简单将 N 的父节点赋值给 N 的子节点。这样做会改变子树中所有节点的级别，并且搜索的判别符也会改变。结果是该子树将不再是 k-d 树，因为节点的子节点可能会违反该判别符的 BST 属性。

与 BST 删除类似，存储在 N 中的记录应该被 N 的右子树中判别符值最小的记录替换，或者被 N 的左子树中该判别符值最大的记录替换。假设 N 位于奇数层，因此 $y$ 是判别符。那么 N 可以被其右子树中 $y$ 值最小的记录（称为 Ymin）替换。问题在于 Ymin 不一定是最左侧节点，就像在 BST 中那样。必须使用修改后的搜索程序来查找左子树中的 $y$ 值。`findmin` 的实现如图 13.12 所示。然后递归调用删除程序从树中移除 Ymin。最后，用 Ymin 的记录替换节点 N。

注意，只有当右子树存在时，我们才能用右子树中值最小的节点替换要删除的节点。

# 13.3 空间数据结构

```
// 返回 root 中对于选定判别符值最小的节点指针

BinNode<E> findmin(BinNode<E> root,

    int discrim, int curcurr) const {

    // discrim: 用于最小搜索的判别符键；

    // curcurr: 当前层 (mod D)

    if (root == NULL) return NULL;

    BinNode<E> minnode = findmin(root->left, discrim,

        curcurr+1)%D);

    if (discrim != curcurr) { // 如果不在判别符所在的层，

        // 必须搜索两个子树

    BinNode<E> rightmin =

        // 检查右侧是否有更小的键值

        minnode = min(minnode, rightmin, discrim);

    // 现在 minnode 拥有子节点中最小的值

    return findmin(minnode, root, discrim);

}
```

图 13.12 k树的 `findmin` 方法。在对应值判别符的层上，向左分支。在其他层上，两个子节点的子树都必须被访问。辅助函数接受两个节点和一个判别符作为输入，返回判别符值较小的节点。

遗憾的是，用左子树中判别符值最大的记录来替换 N 的记录是不满意的，因为这个新值可能会重复。如果是这样，那么 N 的左子树中判别符的值就相等了，这违反了规则。

## 13.3节 空间数据结构

![](img/0ae21f56d72533acf0527c86ba21e1e6_473_0.png)

**图 13.14** 在图 13.11 的 k-d 树中搜索。(a) 包含若干数据点的 $128 \times 128$ 区域的 k-d 树分解。(b) (a) 区域的 k-d 树。

```cpp
// 打印距离 "coord" "rad" 内的所有点

void regionhelp(BinNode* root, int* coord,

	int rad, int discrim) const {

	if (root == NULL) return; // 空树

	// 检查根是否在圆内

	if (InCircle(root->val(), coord, rad)) {

		int count = (root->val())->coord(coord, rad); // 执行适当的操作

		int* curcoord = (root->val())->coord();

		if (curcoord[discrim] > (coord[discrim] - rad))

			regionhelp(root->left(), coord, rad, (discrim+1) % D);

		if (curcoord[discrim] < (coord[discrim] + rad))

			regionhelp(root->right(), coord, rad, (discrim+1) % D);

	}

}
```
