

以下步骤用于重建二叉树：

在二叉树的前序遍历中，先访问根节点，然后遍历左子树，最后遍历右子树。在二叉树的中序遍历中，先遍历左子树，然后访问根节点，最后遍历右子树。因此，在前序遍历中，第一个节点 A 必须是根节点。现在，通过在中序遍历中搜索节点 A，可以找出 A 左侧的所有元素是左子树的中序遍历，右侧的元素是右子树的中序遍历。因此，可以得到左子树和右子树的中序遍历和前序遍历。

![](img/723fa3ef35f5102eb67dc45b74bb823d_198_0.png)

类似地，节点 B 是左子树的根节点，节点 C 是右子树的根节点。可以找到 B 和 C 的左子树和右子树的中序遍历和前序遍历。节点 F 显然是节点 C 的左子节点。

![](img/723fa3ef35f5102eb67dc45b74bb823d_198_1.png)

类似地，节点 D 和 E 分别是节点 B 的左子树和右子树的根节点。节点 G 是节点 C 的右子树。此外，节点 I 是节点 D 的右子节点，节点 J 是节点 E 的右子节点，节点 K 是节点 K 的左子节点。

![](img/723fa3ef35f5102eb67dc45b74bb823d_198_2.png)

## 图 8.18 (a, b, c)：二叉树的重建

## 二叉搜索树

二叉搜索树（BST）是一种有序二叉树。P. F. Windley、A. D. Booth、A. J. T. Colin 和 T. N. Hibbard 于 1960 年发明了二叉搜索树。

**定义：** 二叉搜索树要么为空，要么树中的每个节点包含一个键，并且

- i) 左子树中的所有键都小于根节点的键，
- ii) 右子树中的所有键都大于根节点的键，
- iii) 左子树和右子树也是二叉搜索树。

![](img/723fa3ef35f5102eb67dc45b74bb823d_199_0.png)

## 图 8.19：二叉搜索树

## 二叉搜索树的操作

二叉搜索树支持的操作如下：

表 8.2：二叉搜索树的各种操作

| 操作 | 描述 |
|---|---|
| 遍历 | 此操作恰好遍历二叉搜索树的所有节点一次。 |
| 插入 | 此操作在二叉搜索树中插入一个节点 |
| 删除 | 此操作从二叉搜索树中删除一个节点 |
| 搜索 | 此操作在二叉搜索树中搜索所需的键值。 |
| 后继 | 此操作查找二叉搜索树中给定节点的后继。 |
| 前驱 | 此操作查找给定节点在二叉搜索树中的前驱。 |

## 二叉搜索树遍历

树遍历算法（前序、后序和中序）是遍历二叉搜索树的标准方式，与遍历二叉树类似。在二叉搜索树中，中序遍历始终按递增排序顺序检索数据项。

## 二叉搜索树中的插入

假设给定一个带有键的新数据项以及要插入键的树作为输入。插入操作从根节点开始。如果树为空，则将新项插入为根节点。否则，如果树非空，则将键的值与根节点进行比较。如果键小于根节点，则将其插入左子树，否则将其插入右子树。

## 示例：

在二叉搜索树中插入键：50, 30, 10, 90, 100, 40, 60, 20, 110, 5

插入 50：

![](img/723fa3ef35f5102eb67dc45b74bb823d_200_0.png)

插入 30：

![](img/723fa3ef35f5102eb67dc45b74bb823d_200_1.png)

插入 10：

![](img/723fa3ef35f5102eb67dc45b74bb823d_200_2.png)

插入 90：

![](img/723fa3ef35f5102eb67dc45b74bb823d_200_3.png)

插入 100：

![](img/723fa3ef35f5102eb67dc45b74bb823d_200_4.png)

插入 40：

![](img/723fa3ef35f5102eb67dc45b74bb823d_200_5.png)

插入 60：

![](img/723fa3ef35f5102eb67dc45b74bb823d_201_0.png)

插入 20：

![](img/723fa3ef35f5102eb67dc45b74bb823d_201_1.png)

插入 110：

![](img/723fa3ef35f5102eb67dc45b74bb823d_201_2.png)

插入 5：

![](img/723fa3ef35f5102eb67dc45b74bb823d_201_3.png)

## 使用递归方法向二叉搜索树插入项的算法

```
Algorithm: INSERT (ROOT, DATA)
1. IF ROOT = NULL THEN
   i) Allocate Memory for ROOT node.
   ii) ROOT->INFO=DATA
   iii) ROOT->LCHILD=NULL
   iv) ROOT->RCHILD=NULL
2. ELSE IF ROOT->INFO>DATA THEN
   CALL INSERT (ROOT->LCHILD, DATA)
3. ELSE IF ROOT->INFO<DATA THEN
   CALL INSERT (ROOT->RCHILD, DATA)
4. RETURN
```

## 二叉搜索树中的搜索

与遍历、插入操作类似，二叉搜索树的搜索算法也采用了递归技术。

假设给定一个键以及要在其中搜索该键的树作为输入。现在从根节点开始，检查当前节点的值是否等于键。如果当前节点为 null，则表示所搜索的键值不存在于二叉搜索树中。如果节点具有正在搜索的键，则搜索成功。

否则，当前节点的键要么小于搜索键值，要么大于搜索键值。在第一种情况下，左子树中的所有键都小于搜索键值。这意味着不需要在左子树中搜索。因此，只需搜索右子树。同样，在第二种情况下，只需搜索右子树。

## 使用递归从二叉搜索树搜索项的算法

```
Algorithm: BSTSearch (ROOT, DATA, P)
1. IF ROOT = NULL THEN
   i) PRINT: NOT FOUND
   ii) P = NULL
   iii) RETURN
2. IF ROOT->INFO=DATA THEN
   SET P=ROOT
3. ELSE IF ROOT->INFO>DATA THEN
   CALL BSTSearch(ROOT->LCHILD, DATA, P)
4. ELSE CALL BSTSearch(ROOT->RCHILD, DATA, P)
5. RETURN
```

## 使用迭代方法从二叉搜索树搜索项的算法

```
Algorithm: BstSearch (ROOT, DATA, P)
1. P = ROOT
2. Repeat while P != NULL
3. If DATA = P->INFO then Return
4. Else If DATA < P->INFO then
5. P = P->LCHILD
6. Else P = P->RCHILD
[End of loop]
7. Return
```

假设二叉搜索树包含 n 个数据项。因此，n 个项有 n! 种排列。树中 n! 个数的平均深度约为 c log2 n，其中 c = 1.4。在包含 n 个元素的二叉搜索树中搜索一个项的平均运行时间 f(n) 与 log2 n 成正比，即 f(n) = O(log n)。

## 节点的中序后继

在二叉树中，节点的中序后继是二叉树中序遍历中的下一个节点。中序遍历中最后一个节点的中序后继为 NULL。在二叉搜索树中，键为 k 的节点的中序后继是属于该树且严格大于 k 的最小键值。查找给定节点 x 的后继的思路如下：

- i) 如果 x 有右子节点，则其中序后继将是 x 右子树中最左侧的元素（即 x 右子树中的最小值）。

- ii) 否则，如果 x 没有右子节点，则其中序后继将是其祖先之一，中序后继是从 x 出发仅沿右分支向后可到达的最远节点。

- iii) 否则，如果 x 是树中最右侧的节点，则其中序后继将为 NULL。

## 从二叉搜索树查找中序后继的算法

```
Algorithm: BST_SUCCESSOR(X)
1. If X -> RCHILD != NULL then
2. Y = X -> RCHILD
3. Repeat while Y->LCHILD != NULL
4. Y = Y -> LCHILD
5. [End of loop]
6. Return Y
7. Else
8. Y = X
9. Repeat while Parent(X) -> RCHILD = X
10. X = Parent(X)
[End of loop]
11. If Parent(X) != NULL then Return Parent(X)
12. Else Print: No successor
[End of If]
[End of If]
13. Return
```

## 示例：

![](img/723fa3ef35f5102eb67dc45b74bb823d_204_0.png)

1 的中序后继是 5  
7 的中序后继是 10  
15 的中序后继是 17

## 图 8.21：二叉搜索树

## 二叉搜索树中的删除

二叉搜索树中的删除操作需要考虑三种可能的情况。

**情况 1：** 当删除的节点没有子节点或为叶节点（即被删除节点是叶节点）时，只需从树中删除该节点，并将父节点的相应链接设置为 null。

**情况 2：** 当删除的节点只有一个子节点（左子节点或右子节点）（即被删除节点恰好有一个非空子树）时，只需用其唯一子节点替换该节点。

**情况 3：** 当删除节点（P）有两个子节点（即被删除节点恰好有两个子树）时，则选择其中序后继节点或其中序前驱节点（R）。将节点 R 的键值复制到节点 P，然后递归删除 R 节点，直到满足前两种情况之一。在二叉树中，节点的中序后继（R）仅是其右子树的最左侧子节点，因为右子树不为空（在当前情况下，节点有两个子节点）。现在中序后继可能没有子节点或只有一个右子节点，因此可以使用前两种情况之一将其删除。

## 从二叉搜索树删除项的算法

```
ALGORITHM: DELETE (ROOT, P, PARENT, DATA)
1. IF P-LCHILD=NULL AND P-RCHILD=NULL THEN
   i) IF PARENT-LCHILD=P THEN
      SET PARENT-LCHILD=NULL
   ii) ELSE SET PARENT-RCHILD=NULL
2. ELSE IF P-LCHILD!=NULL THEN
   i) IF PARENT-LCHILD=P THEN
      SET PARENT-LCHILD=P-RCHILD
   ii) ELSE SET PARENT-RCHILD=P-RCHILD
3. ELSE IF P-RCHILD!=NULL THEN
   i) IF PARENT-LCHILD=P THEN
      SET PARENT-LCHILD=P-LCHILD
   ii) ELSE SET PARENT-RCHILD=P-LCHILD
4. ELSE P-LCHILD!=NULL AND P-RCHILD!=NULL THEN
   i) SET PARENT = P
   ii) SET IN=P-RCHILD
```

