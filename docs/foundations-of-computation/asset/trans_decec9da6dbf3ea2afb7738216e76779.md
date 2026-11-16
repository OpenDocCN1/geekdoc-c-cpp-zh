

节点包含一个整数。二叉树可以为空，也可以由一个节点（称为树的根）和两个更小的二叉树（称为树的左子树和右子树）组成。你已经可以看到递归结构：一棵树可以包含更小的树。在 Java 中，树的节点可以由属于类的对象表示

```
class BinaryTreeNode {
    int item; // An integer value stored in the node.
    BinaryTreeNode left; // Pointer to left subtree.
    BinaryTreeNode right; // Pointer to right subtree.
}
```

空树由具有特殊值 null 的指针表示。如果 root 是指向树根节点的指针，那么 root.left 是指向左子树的指针，root.right 是指向右子树的指针。当然，如果相应的子树为空，root.left 和 root.right 都可以为 null。同样，root.item 是根节点中整数的名称。

假设我们想要一个函数，用于查找二叉树中所有节点的所有整数之和。我们可以用一个简单的递归函数来做到这一点。递归的基本情况是空树。由于空树中没有整数，空树中整数之和为零。对于非空树，我们可以使用递归来查找左子树和右子树中整数的和，然后将这些和加到树根节点的整数上。在 Java 中，这可以表示如下：

```
int TreeSum( BinaryTreeNode root ) {
    // Find the sum of all the integers
    // in the tree that has the given root.
    int answer;
    if ( root == null ) { // The tree is empty.
        answer = 0;
    }
    else {
        answer = TreeSum( root.left );
        answer = answer + TreeSum( root.right );
        answer = answer + root.item;
    }
    return answer;
}
```

我们可以使用数学归纳法的第二种形式来证明这个函数是正确的。

## 1.9. 应用：递归与归纳

### 定理 1.16.

上面定义的函数 TreeSum 正确地计算了二叉树中所有整数的和。

### 证明.

我们对树中的节点数进行归纳。设 P(n) 为陈述“TreeSum 正确地计算了任何恰好包含 n 个节点的二叉树中节点的和”。我们证明对于每个自然数 n，P(n) 都成立。

考虑 n = 0 的情况。零个节点的树是空的，空树由 null 指针表示。在这种情况下，TreeSum 定义中的 if 语句将值 0 赋给 answer，这是空树的正确和。所以，P(0) 为真。

设 k 为任意大于 0 的自然数。假设我们已经知道对于每个满足 0 ≤ x < k 的自然数 x，P(x) 都成立。也就是说，TreeSum 正确地计算了任何节点数少于 k 的树中所有整数的和。我们必须证明由此可得出 P(k) 为真，也就是说，TreeSum 对于有 k 个节点的树也有效。假设 root 是指向总共有 k 个节点的树的根节点的指针。由于根节点算作一个节点，剩下 k − 1 个节点分配给左子树和右子树，因此每个子树必须包含少于 k 个节点。根据归纳假设，我们知道 TreeSum(root.left) 正确地计算了左子树中所有整数的和，TreeSum(root.right) 正确地计算了右子树中所有整数的和。树中所有整数的和是 root.item 加上子树中整数的和，这正是 TreeSum 计算出的值。所以，TreeSum 对于有 k 个节点的树确实有效。这完成了归纳。

请注意归纳证明的结构与递归函数的结构是多么接近。特别是，数学归纳法的第二种形式在这里非常自然，因为子树的大小可能是从 0 到完整树大小减 1 的任何值。在关于二叉树的证明中使用数学归纳法的第一种形式将非常困难。

### 练习

- 1. 本节给出的 Hanoi 子程序不仅解决了汉诺塔问题。它使用最少可能的移动次数来解决问题。使用归纳法证明这一事实。

- 2. 使用归纳法证明 Hanoi 子程序使用 2^n − 1 次移动来解决 n 个盘子的汉诺塔问题。（有一个与汉诺塔问题相关的故事。据说在世界创造之日，一组河内的僧侣被指派解决 64 个盘子的问题。他们每天只能移动一个盘子。在问题解决的那一天，世界将终结。然而，我们不必太担心，因为 2^24 - 1 天是一段非常漫长的时间——大约 5 亿亿年。）

- 3. 考虑以下递归函数：

```
int power(int x, int n) {
    // Compute x raised to the power n.
    // Assume that n >= 0.
    int answer;
    if ( n == 0 ) {
        answer = 1;
    }
    else if ( n % 2 == 0 ) {
        answer = power( x * x, n / 2 );
    }
    else {
        answer = x * power( x * x, (n-1) / 2 );
    }
    return answer;
}
```

证明对于任何整数 x 和任何非负整数 n，函数 power(x, n) 正确地计算 x^n 的值。（假设 int 数据类型可以表示任意大的整数。）请注意，测试 "if (n % 2 == 0)" 检查 n 是否能被 2 整除。也就是说，如果 n 是偶数，则测试为真。（这个函数实际上是计算 x^n 的一种非常高效的方法。）

- 4. 二叉树中的叶节点是指其左子树和右子树都为空的节点。证明以下递归函数正确地计算了二叉树中叶节点的数量：

```
int LeafCount( BinaryTreeNode root ) {
    // Counts the number of leaf nodes in
    // the tree with the specified root.
    int count;
    if ( root == null ) {
        count = 0;
    }
    else if ( root.left == null && root.right == null ) {
        count = 1;
    }
    else {
        count = LeafCount( root.left );
        count = count + LeafCount( root.right );
    }
    return count;
}
```

- 5. 二叉排序树满足以下属性：如果 node 是指向树中任意节点的指针，那么 node 左子树中的所有整数都小于 node.item，而 node 右子树中的所有整数都大于或等于 node.item。证明以下递归子程序以非递减顺序打印二叉排序树中的所有整数：

```
void SortPrint( BinaryTreeNode root ) {
    // Assume that root is a pointer to the
    // root node of a binary sort tree.  This
    // subroutine prints the integers in the
    // tree in non-decreasing order.
    if ( root == null ) {
        // There is nothing to print.
    }
    else {
        SortPrint( root.left );
        System.out.println( root.item );
        SortPrint( root.right );
    }
}
```

## 1.10 递归定义

当子程序（至少部分地）以自身来定义时，编程中就会出现递归。但递归也发生在编程之外。**递归定义**是指包含对正在定义的术语的引用的定义。递归定义至少部分地以自身来定义某物。与递归子程序的情况一样，数学归纳法通常可以用来证明关于递归定义的事物的事实。

如前所述，对于 n ∈ N，n! 有一个递归定义。我们可以定义 0! = 1，并且对于 n > 0，n! = n · (n − 1)!。其他数字序列也可以递归定义。例如，著名的 **斐波那契数列** 是数字序列 f0, f1, f2, ...，由以下递归定义：

f0 = 0
f1 = 1
fn = fn-1 + fn-2   for n > 1

使用此定义，我们计算得出

```
f2 = f1 + f0 = 0 + 1 = 1
f3 = f2 + f1 = 1 + 1 = 2
f4 = f3 + f2 = 2 + 1 = 3
f5 = f4 + f3 = 3 + 2 = 5
f6 = f5 + f4 = 5 + 3 = 8
f7 = f6 + f5 = 8 + 5 = 13
```

等等，等等。根据此定义，我们可以使用归纳法来证明关于斐波那契数列的事实。例如，我们可以证明 fn 随 n 指数增长，即使不找到 fn 的精确公式。

### 定理 1.17.

斐波那契数列 f0, f1, f2, ... 满足 fn > (3/2)^(n-1)，对于 n >= 6。

### 证明.

我们对 n 进行归纳证明。对于 n = 6，我们有 fn = 8，而 1.5^(n-1) = 1.5^5，约为 7.6。所以对于 n = 6，fn > 1.5^(n-1)。同样，对于 n = 7，我们有 fn = 13，而 1.5^(n-1) = 1.5^6，约为 11.4。所以对于 n = 7，fn > 1.5^(n-1)。

现在假设 k 是大于 7 的任意整数。假设我们已经知道对于 n = k - 1 和 n = k - 2，fn > 1.5^(n-1) 成立。我们想要证明不等式对于 n = k 也成立。但是

```
fk = fk-1 + fk-2
> 1.5^(k-1-1) + 1.5^((k-2)-1) (by the induction hypothesis)
= 1.5^(k-2) + 1.5^(k-3)
= (1.5) * (1.5^(k-3) + 1.5^(k-3))
= (2.5) * (1.5^(k-3))
> (1.5^2) * (1.5^(k-3)) (since 1.5^2 = 2.25)
= 1.5^(k-1)
```

这一串等式和不等式表明 fk > 1.5^(k-1)。这完成了归纳并证明了定理。

### 练习

- 1. 证明斐波那契数列 f0, f1, f2, ... 对于所有自然数 n 满足 fn < 2^n。

