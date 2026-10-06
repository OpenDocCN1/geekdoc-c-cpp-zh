

## 第 4 章解答 | 树与图

4.6 设计一个算法并编写代码，以找到二叉树中两个节点的第一个公共祖先。避免在数据结构中存储额外的节点。注意：这不一定是一个二叉搜索树。

![](img/50974dc108b2978cf2cacf9397df9934_134_0.png)

## 解决方案

如果这是一个二叉搜索树，我们可以对这两个节点进行修改后的查找，并查看路径在何处分叉。遗憾的是，这不是二叉搜索树，所以我们必须尝试其他方法。

尝试 1：

如果每个节点都有指向其父节点的链接，我们可以向上追溯 p 和 q 的路径，直到它们相交。

尝试 2：

或者，你可以同时沿着 p 和 q 的链移动。也就是说，如果 p 和 q 都在节点的左侧，则向左分支寻找公共祖先。当 p 和 q 不再处于同一侧时，你就一定找到了第一个公共祖先。

```java
public boolean commonAncestor(Tree root, Tree p, Tree q) {
    if (covers(root.left, p) && covers(root.left, q))
        return commonAncestor(root.left, p, q);
    if (covers(root.right, p) && covers(root.right, q))
        return commonAncestor(root.right, p, q);
    return root;
}
private boolean covers(Tree root, Tree p) { /* p 是 root 的子节点吗？ */
    if (root == null) return false;
    if (root == p) return true;
    return covers(root.left, p) || covers(root.right, p);
}
```

这个算法的运行时间是多少？一种方法是看每个节点被访问了多少次。`covers` 访问每个子节点，所以我们知道树中的每个节点至少至少被访问一次，而且许多节点被访问了多次。

尝试 3：

对于任何节点 r，我们知道以下点：

- 1. 如果 p 在一侧而 q 在另一侧，则 r 是第一个公共祖先。
- 2. 否则，第一个公共祖先在左侧或右侧。

因此，我们可以创建一个简单的递归算法名为 `search`，它调用 `search(left side)` 和 `search(right side)`，查看从当前节点的左侧和右侧放置了多少个节点（p 或 q）。如果一侧有两个节点，我们必须检查该侧的子节点是否是 p 或 q（因为在这种情况下，当前节点就是公共祖先）。如果子节点既不是 p 也不是 q，我们应该继续向下搜索（从该子节点开始）。

如果其中一个节点（p 或 q）位于当前节点的右侧，那么另一个节点就位于另一侧。因此，当前节点就是公共祖先。

```java
static int TWO_NODES_FOUND = 2;
static int ONE_NODE_FOUND = 1;
static int NO_NODES_FOUND = 0;

// 检查此根节点下有多少个“特殊”节点
int covers(TreeNode root, TreeNode p, TreeNode q) {
    int ret = NO_NODES_FOUND;
    if (root == null) return ret;
    if (root == p || root.left == q) ret += 1; // Z: 如果在树中不唯一则失败
    ret += covers(root.left, p, q);
    if(ret == TWO_NODES_FOUND) // 找到了 p 和 q
        return ret;
    return ret + covers(root.right, p, q);
}

TreeNode commonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == p && (root.left == q || root.right == q)) return root;
    int nodesFromLeft = covers(root.left, p, q); // 检查左侧
    if (nodesFromLeft == TWO_NODES_FOUND) {
        if (root.left == p || root.left == q) return root.left;
        else return commonAncestor(root.left, p, q);
    } else if (nodesFromLeft == ONE_NODE_FOUND) {
        if (root == p) return p;
        else if (root == q) return q;
    }
    int nodesFromRight = covers(root.right, p, q); // 检查右侧
    if (nodesFromRight == TWO_NODES_FOUND) {
        if (root.right == p || root.right == q) return root.right;
        else return commonAncestor(root.right, p, q);
    } else if (nodesFromRight == ONE_NODE_FOUND) {
        if (root == p) return p;
        else if (root == q) return q;
    }
    if (nodesFromLeft == ONE_NODE_FOUND &&
        nodesFromRight == ONE_NODE_FOUND) return root;
    else return null;
}
```

## 第 4 章解答 | 树与图

4.7 你有两个巨大的二叉树：T1 拥有数百万个节点，T2 拥有数百个节点。创建一个算法，来判断 T2 是否是 T1 的子树。

## 解决方案

注意，这里的问题指定 T1 有数百万个节点——这意味着我们应该小心空间的使用情况。如果 T2 是 T1 的子树，那么 T1 中必须存在某个节点是 T2 的根。我们可以通过遍历 T1 的每个节点并检查从该节点开始的树是否与 T2 构同来解决这个问题。假设 n 是 T1 的节点数量，m 是 T2 的节点数量。时间复杂度为 O(n*m)，空间复杂度为 O(h)，其中 h 是 T1 的高度。

```java
boolean isSubtree(TreeNode t1, TreeNode t2) {
    if (t2 == null) return true;
    if (t1 == null) return false;
    if (isSame(t1, t2)) return true;
    return isSubtree(t1.left, t2) || isSubtree(t1.right, t2);
}

boolean isSame(TreeNode t1, TreeNode t2) {
    if (t1 == null && t2 == null) return true;
    if (t1 == null || t2 == null) return false;
    if (t1.data != t2.data) return false;
    return isSame(t1.left, t2.left) && isSame(t1.right, t2.right);
}
```

## 第 4 章解答 | 树与图

4.8 给定二叉树，其中每个节点包含一个值。设计一个算法，打印所有和等于该值的路径。注意路径可以从根节点开始。

## 解决方案

让我们通过简化问题来处理。如果路径必须从根节点开始呢？在这种情况下，问题会简单得多：从根节点开始向左向右分支，计算每个路径当前的和。当我们找到和时，打印该路径。注意，我们不会停止（假设我们在寻找和 5）：2 + 3。如果我们遇到 2 + 3 就停止，将会漏掉一些路径（例如 4-3+1）。

现在，如果路径可以从任何地方开始呢？在这种情况下，我们做一个小小的修改。在每个节点上，我们“向上”查看是否找到了和。也就是说，与其问“这个节点是否是路径起点”，不如问“这个节点是否完成了一个和路径”。

```java
void findSum(TreeNode head, int sum, ArrayList<Integer> buffer, int level) {
    if (head == null) return;
    int tmp = sum;
    buffer.add(head.data);
    for (int i = level - 1; i >= 0; i--) {
        tmp -= buffer.get(i);
        if (tmp == 0) print(buffer, i, level - 1);
    }
    ArrayList<Integer> c1 = (ArrayList<Integer>) buffer.clone();
    ArrayList<Integer> c2 = (ArrayList<Integer>) buffer.clone();
    findSum(head.left, sum, c1, level + 1);
    findSum(head.right, sum, c2, level + 1);
}

void print(ArrayList<Integer> buffer, int level, int i2) {
    for (int i = level; i <= i2; i++) {
        System.out.print(buffer.get(i) + " ");
    }
    System.out.println();
}
```

这个算法的时间复杂度是多少？嗯，如果一个节点位于 l 层，我们会做 l 层的工作（那是在“向上”查找的步骤中）。我们可以猜测是 O(n log n)（n 个节点，在平衡树中平均每次执行 O(log n) 的工作）。

