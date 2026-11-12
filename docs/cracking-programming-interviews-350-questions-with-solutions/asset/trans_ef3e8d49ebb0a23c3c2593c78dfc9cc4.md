
```cpp
while(u != v)
{
    u = tree.parent(u);
    v = tree.parent(v);
}

return u;
}

int main()
{
    tree<std::string> st;
    tree<std::string>::iterator itra
        = st.insert(st.begin(), "a");
    tree<std::string>::iterator itrb
        = st.append(itra, "b");
    tree<std::string>::iterator itrc
        = st.append(itra, "c");

    tree<std::string>::iterator itrd, itre;
    itrd = st.append(itrb, "d");
    itre = st.append(itrb, "e");
    st.append(itre, "h");

    tree<std::string>::iterator itri
        = st.append(itre, "i");
    tree<std::string>::iterator itrm
        = st.append(itri, "m");
    tree<std::string>::iterator itrn
        = st.append(itri, "n");
    tree<std::string>::iterator itro
        = st.append(itri, "o");

    tree<std::string>::iterator itrf
        = st.append(itrd, "f");
    tree<std::string>::iterator itrg
        = st.append(itrd, "g");
    tree<std::string>::iterator itrj
        = st.append(itrf, "j");
    tree<std::string>::iterator itrk
        = st.append(itrf, "k");
    tree<std::string>::iterator itrl
        = st.append(itrf, "l");


    std::cout << "levels of nodes:\n";
    std::cout << "a: " << st.level(itra)
              << "\nb: " << st.level(itrb)
              << "\nc: " << st.level(itrc)
              << "\nd: " << st.level(itrd)
              << "\ne: " << st.level(itre)
              << "\nf: " << st.level(itrf)
              << "\nh" << std::endl;

    tree<std::string>::iterator pi, pe, pb;
    pi = tree<std::string>::parent( itri );
    pe = tree<std::string>::parent( itri );
    pb = tree<std::string>::parent( pe );

    std::cout << "lca_of_b_and_c:"
    << *lca( st, itrb, itrc ) << std::endl;
    std::cout << "lca_of_d_and_e:"
    << *lca( st, itrd, itre ) << std::endl;
    std::cout << "lca_of_f_and_e:"
    << *lca( st, itrf, itre ) << std::endl;
    std::cout << "lca_of_f_and_i:"
    << *lca( st, itrf, itri ) << std::endl;
    std::cout << "lca_of_f_and_g:"
    << *lca( st, itrf, itrg ) << std::endl;
    std::cout << "lca_of_j_and_l:"
    << *lca( st, itrj, itrl ) << std::endl;
    std::cout << "lca_of_l_and_o:"
    << *lca( st, itrl, itro ) << std::endl;
    std::cout << "lca_of_b_and_o:"
    << *lca( st, itrb, itro ) << std::endl;
    std::cout << "lca_of_a_and_a:"
    << *lca( st, itra, itra ) << std::endl;
    std::cout << "lca_of_j_and_c:"
    << *lca( st, itrj, itrc ) << std::endl;
    std::cout << "lca_of_d_and_c:"
    << *lca( st, itrd, itrc ) << std::endl;

}
```

输出为：

```text
levels of nodes:
a: 0
b: 1
d: 2
e: 2
i: 3
f: 3

lca of b and c : a
lca of d and e : b
lca of f and e : b
lca of f and i : b
lca of f and g : d
lca of j and l : f
lca of l and o: b
lca of b and o : b
lca of a and a : a
lca of j and c : a
lca of d and c : a
```

### 常数时间 LCA

于是，*LCA* 问题是：给定一棵用于预处理的带根树 *T*，以某种方式预处理它，使得 *T* 中任意两个给定节点的 *LCA* 可以在常数时间内取得。下面我们给出一种预处理算法，其时间和空间复杂度均不超过线性。

我们对计算机器模型作以下两个假设。令 *n* 表示一元表示下输入规模：

- 1. 对二进制表示不超过 log n 位的数进行的所有算术、比较和逻辑运算都可以在 *常数时间* 内完成。
- 2. 我们假设，查找一个大小为 log n 的数的最高位（最左位）或最低位（最右位）可以在 *常数时间* 内完成。

### 完全二叉树

我们的讨论从 *LCA* 问题的一个特别简单的实例开始，即完全二叉树上的 *LCA* 查询。我们将利用在完全二叉树上求解 *LCA* 问题的知识，并在之后将其扩展，以求解任意带根树 *T* 上的 *LCA* 问题。

令 *B* 表示一棵有 *n* 个节点的完全二叉树。这里的关键是在节点自身中编码从根到该节点的唯一路径。我们为每个节点分配一个 *路径编号*，它是一个 *log n* 位的数，用于编码从根到该节点的唯一路径。

**路径编号** 对于 *B* 中的每个节点 *v*，我们按以下方式编码一个 *路径编号*：

- 从最左位开始计数，*v* 的路径编号的第 i 位对应于从根到 *v* 的路径上的第 i 条边。
- 从左数第 i 位为 0 表示路径上的第 i 条边通向一个左孩子，为 1 表示通向一个右孩子。
- 令 *k* 表示从根到 *v* 的路径上的边数，那么我们将路径编号的第 *k+1* 位（高度位）标记为 1，并将其余的 *log n - k - 1* 位标记为 0。

![](img/78e1bff64796dccbf49e7c84b8201fb2_214_0.png)

- 节点 i 的路径编号为 `0101`
- 节点 j 的路径编号为 `1010`

请注意，高度位用**粗体**标记，填充位用*斜体*标记。

路径编号可以很容易地通过对 $B$ 进行简单的 $O(n)$ 中序遍历来分配。

![](img/78e1bff64796dccbf49e7c84b8201fb2_214_1.png)

### 完全二叉树中的 LCA 查询

现在假设 $u$ 和 $v$ 是 $B$ 中的两个节点，且 $path(u)$ 和 $path(v)$ 是它们相应的路径编号。

我们将 $u$ 和 $v$ 的最近公共祖先记为 $lca(u,v)$。

## 3.1. 最近公共祖先（LCA）问题

我们将路径编号中对应于从根出发的路径上的边的前缀位称为路径编号的 *路径位*。

- 1. 首先我们计算 `path(u) XOR path(v)`，并找到最左侧等于 1 的位。
- 2. 如果不存在这样的位，那么 `path(u) = path(v)`，从而 `u = v`，因此假设结果的第 *k* 位为 1。
- 3. 如果 `path(u)` 中的第 *k* 位和 `path(v)` 中的第 *k* 位都是路径位，那么这意味着 `u` 和 `v` 在它们从根出发的路径上的 *k-1* 条边上一致，也就是说每个节点路径编号的前 *k-1* 位前缀编码了从根到 `lca(u,v)` 的路径。

![](img/78e1bff64796dccbf49e7c84b8201fb2_215_0.png)

**path(u) XOR path(v) =**

```text
  0010
XOR 0111
  ----
  0101
```

因此，

`path(lca(u,v)) = 0100`

其中第一位是高度位，其余位是填充位。

![](img/78e1bff64796dccbf49e7c84b8201fb2_216_0.png)

![](img/78e1bff64796dccbf49e7c84b8201fb2_216_1.png)

由此可以得出结论：如果我们取 *path(u) XOR path(v)* 结果的前 *k − 1* 位，将第 *k* 位设为 1，并在末尾填充 log *n − k* 个 0 后缀位，就得到 *path(lca(u,v))*。

如果 *path(u)* 中的第 *k* 位或 *path(v)* 中的第 *k* 位（或两者）不是路径位，那么一个节点是另一个节点的祖先，并且可以通过比较 *path(u)* 和 *path(v)* 的高度位轻松得到 *lca(u,v)*。

### 通用 LCA 算法

对于任意树 T，通用 LCA 算法包括以下两个阶段：

- 1. 首先，我们将 *LCA* 问题归约为 *受限范围最小值* 问题。*受限范围最小值* 问题是在一个固定数字列表的某个区间中寻找最小数的问题，其中列表中两个相邻数字的差恰好为一。
- 2. 其次，我们求解 *受限范围最小值* 问题，从而求解 *LCA* 问题。

更多细节请参见 [?]。

## 3.2 间谍活动

### 问题描述

罗布·罗尔对他在总统选举中的失败耿耿于怀，决定雇一名声名狼藉的摄影师跟踪威尔·克林特伍德。（姓名已更改，以保护有罪者。摄影师偷偷地拍摄克林特伍德，并在每张照片上标记拍摄时间 *t*。罗尔告诉摄影师，在每张特别有丑闻的照片上标记一个大大的红色 X，因为这些照片将用于未来的负面广告。罗尔需要一个包含克林特伍德照片的数据结构，并支持以下操作：

- **INSERT(x):** 将照片 *x* 插入数据结构。照片 *x* 有一个整数字段 `time[x]` 和一个布尔字段 `scandalous[x]`。
- **DELETE(x):** 从数据结构中删除照片 *x*。
- **NEXT-PICTURE(x):** 返回在照片 *x* 之后立即拍摄的照片。
- **SCANDALOUS(t):** 返回在时间 *t* 之后拍摄的第一张丑闻照片。

描述该数据结构的一种高效实现。说明如何执行这些操作，并分析它们的运行时间。请简洁。

### 解法

为了让我们能够高效地实现这些操作，我们将使用 *红黑树* 表示，以时间为键来组织照片，并为每个节点 *x* 增加以下额外字段：

- `scandalous?[x]`
- `max − scand − time[x]`

字段 *max − scand − time[x]* 存储以 *x* 为根的子树中最近的丑闻照片拍摄时间。它要么包含一个整数时间，要么在子树中没有丑闻照片时包含 NIL。我们在此数据结构上实现这些操作（均在 *O(log n)* 运行时间内），如下所示：

- **INSERT(x):** 将 *x* 放入树中，以 `time[x]` 为键，就像在普通红黑树中一样。如有必要，在旋转后更新 `max − scand − time` 字段。这可以在 *O(1)* 时间内完成。
- **DELETE(x):** 与 INSERT(x) 类似；执行红黑树中通常所做的操作，并注意在删除节点 *x* 后修正 `max − scand − time` 字段。当遇到一个节点满足 `max − scand − time[n] = time[x]` 且 `scandalous?[x] = TRUE` 时，查看该节点的孩子，并设置 `max − scand − time[n] ← max(max − scand − time[right[n]], max − scand − time[left[n]])`。
- **NEXT-PICTURE(x):** 与红黑树中的 SUCCESSOR(x) 类似。

