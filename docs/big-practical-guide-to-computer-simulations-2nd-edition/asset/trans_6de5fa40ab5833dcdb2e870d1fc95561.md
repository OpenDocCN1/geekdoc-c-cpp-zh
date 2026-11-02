

对于一个分量，不再启动进一步的分量识别过程。最终遇到节点 5。它是一个新分量（ID 1）的种子。由于它没有邻居，即代码第 23 行的条件立即为 FALSE，因此不会有其他节点加入该分量。此时，主循环终止，完整的分量识别过程完成。

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_230_0.png)

图 6.29 随机图最大分量的平均大小 S，按节点数 n 归一化，作为平均连通度 c 的函数。这里 n = 10000。对于每个 c 值，平均值是在 1000 个独立随机图实例上取得的。线条仅供参考。

作为如何将分量确定与图模型结合使用的一个示例应用，我们研究 Erdős–Rényi（ER）随机图。这些图在此具有 n 个节点和 m 条边，边随机且独立地连接所选节点对。因此，

## 练习

（解答：可从 http://www.worldscientific.com/r/9010-supp 下载）

### （1）排列

| 解决方案源代码 |
| --- |
| 目录：algorithms |
| 文件： |
| permutation.c |

设计、实现并测试一个递归函数 permutation()，用于原地获取并打印整数数组 a[] 的所有排列，即不需要额外的数组。

函数原型如下：

```c
/********************** permutation() **********************/
/** Obtains all permutations of positions 0..n-1 of a       **/
/** given array 'a' of numbers and prints them,            **/
/** including the higher index entries (from 0..n_max-1).  **/
/**                                                         **/
/** Parameters: (*) = return parameter                      **/
/**       n: current range                                   **/
/**       n_max: size of array                              **/
/**       a: array                                          **/
/** Returns:                                                **/
/**       (nothing)                                         **/
/*************************************************************/
void permutation(int n, int n_max, int *a)
```

### （2）数的幂

| 解决方案源代码 |
| --- |
| 目录：algorithms |
| 文件： |
| power.c |

设计、实现并测试函数 fast_power()，用于计算幂 a^n（n 为整数）。采用分治方法，当 n > 2 时将 a^n 的计算转化为 a^{n/2} 的计算。这使得运行时间为 O(log n)，而朴素方法为 O(n)。

函数原型如下：

```c
/************ fast_power() ************/
/** Calculates the a^n (n being a natural number) using **/
/** a divide-and-conquer approach. **/
/**
/** Parameters: (*) = return parameter **/
/**            a: base **/
/**            n: power **/
/** Returns **/
/**            a^n **/
/***************************************/
double fast_power(double a, int n)
```

提示：首先为 n ≥ 0 设计你的函数，然后将 n < 0 的情况归约为 n > 0 的情况。

### （3）数值划分

解决方案源代码
目录：algorithms
文件：partition.c

数值划分问题（NPP）定义如下：给定一个包含 n 个非负整数的集合 A = {a[0]...a[n-1]}，我们希望将其划分为两个子集 A1 ⊂ A 和 A2 ⊂ A，使得差值 d = |∑_{a∈A1} a - ∑_{a∈A2} a| 最小。例如，{2,3,4,10} 可以被划分为两个子集 A1 = {2,3,4} 和 A2 = {10}，其中 d = 1。使用动态规划方法解决此问题，即找到最小差值。设计、实现并测试所得程序。

提示：引入二维数组 part[][]，其中如果 {a[0]...a[i]} 的某个子集的和为 s，则 part[i][s]=1（其中 i=0,...,n-1，s=0,...,∑_{a∈A} a）。可以使用 part[i][s]=1（如果 part[i-1][s]==1 或 part[i-1][s-a[i]]==1）来计算数组 part（需对 part[0][s] 进行适当初始化）。然后，利用 |∑_{a∈A1} a - ∑_{a∈A2} a| = |2∑_{a∈A1} a - ∑_{a∈A} a|，可以从 part[n-1][s]（s=0,...,∑_{a∈A} a）得到最小差值。注意，此方法不直接给出两个子集，仅给出最小差值。

技术提示：将整数作为参数传递给程序。

### （4）骑士的巡游

解决方案源代码
目录：algorithms
文件：knight.c

在国际象棋棋盘上，马可以从当前位置移动到其邻域中最多八个可能位置之一。马的可能走法如图 6.30（左）所示。

骑士巡游问题是为一个 n × n 的棋盘寻找一条巡游路径，从棋盘的左上角开始，使得每个方格恰好被访问一次。一个 8 × 8 棋盘的可行解如图 6.30（右）所示。

编写一个使用回溯方法解决此问题的 C 程序。

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_234_0.png)

图 6.30 （左）马的 8 种可能走法。（右）骑士巡游问题在 8 × 8 棋盘上的一个可行解。

设计、实现并测试所得程序。提示：使用数组 visit[x][y]，其中初始时到处 visit[x][y]=0，visit[x][y]>0 表示该方格在巡游的第几步被访问。此外，使用数组 dx[] 和 dy[] 存储可能的移动，例如（见图 6.30 左）dx[0]=−2，dy[0]=−1。最后，你可以使用一个函数，它放置一个骑士，并调用自身来放置下一个骑士。函数原型可以如下：

```c
/********************* move_knight() *********************/
/** Calculates recursively via backtracking a tour for **/
/** the knight, such that all squares with visit[x][y]=0 **/
/** are visited once. **/
/** **/
/** Parameters: (*) = return parameter **/
/** n: size of board **/
/** step: how many sites already visited? **/
/** x,y: current position of knight **/
/** visit: states whether and when square was visited **/
/** dx,dy: possible move directions **/
/** Returns: **/
/** (nothing) **/
/********************************************************** */
void move_knight(int n, int step, int x, int y,
 short int **visit, int *dx, int *dy)
```

### （5）从链表中移除元素

设计、实现并测试用于从链表中移除元素的函数 remove_node()，如第 181 页所述。函数原型如下：

解决方案源代码
目录：algorithms
文件：list_rm_e.c

```c
/**************** remove_element() ****************/
/** Remove element from list                       **/
/** PARAMETERS: (*)= return-parameter               **/
/**               list: first element of list       **/
/**               elem: to be removed               **/
/** RETURNS:                                        **/
/**  (new) pointer to beginning of the list         **/
/*****************************************************/
elem_t *remove_node(elem_t *list, elem_t *elem)
```

### 6. 链表的归并排序

设计、实现并测试一个使用归并排序算法（见第 6.3 节）对给定链表进行排序的函数。主要方法如下：首先，将给定链表拆分为两个大小约为一半的链表。然后，对这两个链表分别递归调用该函数。最后，通过合并两个已排序链表来构建结果链表。（练习指针运算的好题目！！）函数原型如下：

| 解决方案源代码 |
|---|
| 目录：algorithms |
| 文件：list_mergesort.c |

```c
/**************** mergesort_list() ****************/
/** Sorts list using mergesort algorithm            **/
/** PARAMETERS: (*)= return-parameter               **/
/**               list: first element of list       **/
/** RETURNS:                                        **/
/**  (new) pointer to beginning of the list         **/
/*****************************************************/
elem_t *mergesort_list(elem_t *list)
```

### 7. 在树中查找值

设计、实现并测试一个函数，用于测试树中是否包含给定键值。函数原型如下：

| 解决方案源代码 |
|---|
| 目录：algorithms |
| 文件：tree_find.c |

```c
/**************** find_node() ****************/
/** Locates a node with a given 'key' in a tree.   **/
/** If the 'key' is not contained in the tree,     **/
/** NULL is returned                               **/
/** PARAMETERS: (*)= return-parameter               **/
/**               tree: pointer to root of tree     **/
/**               key: to be located                **/
/** RETURNS:                                        **/
/**  pointer to node (NULL if key is not existing)  **/
/*****************************************************/
node_t *find_node(node_t *tree, int key)
```

