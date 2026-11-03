
```
nodeptr temp;
if(stack == NULL)
printf("POP OPERATION IS NOT POSSIBLE");
else
{
temp=stack;
printf("THE POPPED ITEM IS %d\n",stack->info);
printf("press any key to continue");
getchar();
stack=stack->next;
}
free(temp);
return(stack);
}
```
/*
输入 / 输出
1 入栈
2 出栈
3 显示
4 退出
请输入您的选择    1
请输入要入栈的元素 34
1 入栈
2 出栈
3 显示
4 退出
请输入您的选择    3
栈顶 34->NULL
1 入栈
2 出栈
3 显示
4 退出
请输入您的选择    2
弹出的元素是 34
按任意键继续
1 入栈
2 出栈
3 显示
4 退出
请输入您的选择    4
退出。

## 8. (a) 什么是网络？
## (b) 什么是生成树？

## (c) 定义最小生成树。
## (d) 树中有哪些不同的遍历方式？
## (a) 什么是网络？

答：网络是指两个介质之间的连接/通信。

根据 C 语言，网络是指两个或多个节点之间的连接，或者从一个图到另一个图的通信。图节点与另一个节点相连，这种连接称为边。下图解释并展示了网络操作是如何执行的。

![](img/65953ea584e494f3d396b2252cb5ea53_537_0.png)

## (b) 什么是生成树？

答：生成树通常表示为图。因此，生成树是无向树，只包含足以将所有节点连接成一棵树的那些边。关于生成树有两个重要考虑。

- 1. 生成树中的每一对节点之间都应具有唯一路径。
- 2. 生成树中的边数比节点总数少一[如果一棵树由 n 个节点组成，则边数应为 (n-1)]。
- 3. 因此，任何成功满足上述考虑的树都可以称为生成树。下面是一些生成树的示例。

![](img/65953ea584e494f3d396b2252cb5ea53_537_1.png)

每个生成树都涉及三个主要概念。它们是

- 1. 深度优先搜索生成树
- 2. 广度优先搜索生成树
- 3. 生成树的代价

通过深度优先搜索机制得到的生成树称为深度优先搜索生成树。通过广度优先搜索机制得到的生成树称为广度优先搜索生成树。
当生成树中的每条边都关联一个代价时，生成树的代价就是生成树所有边的代价之和。
基于生成树的代价特性，它已成功应用于与电路相关的研究，以及确定网络批量路由中的最短路径等研究中。

## (c) 定义最小生成树。

答：

加权图的最小生成树（MST）是边权之和最小的生成树。最小生成树描述了连接给定顶点集合中所有顶点的最廉价网络。

用于最小生成树的 Kruskal 算法按代价递增的顺序插入边（将连接两个先前不相交分量的边加入树中）。

图的最小生成树（MST）定义了使图保持为一个连通分量的最廉价边子集。电话公司对最小生成树特别感兴趣，因为一组站点的最小生成树定义了使用尽可能少的线缆连接这些站点的布线方案。它是所有网络设计问题之母。

最小生成树之所以重要，有几个原因：

- - 它们可以快速、轻松地计算出来，并创建一个稀疏子图，该子图能反映原图的许多信息。
- - 它们提供了一种识别点集中簇的方法。从最小生成树中删除长边后，留下的连通分量定义了数据集中的自然簇。
- - 它们可用于为斯坦纳树和旅行商等困难问题给出近似解。
- - 作为一种教学工具，最小生成树算法提供了直观证据，表明贪心算法可以给出可证明的最优解。

## 最小生成树的示例

## 一个加权图 G

![](img/65953ea584e494f3d396b2252cb5ea53_538_0.png)

## 加权图 G 的最小生成树

![](img/65953ea584e494f3d396b2252cb5ea53_538_1.png)

使用 Kruskal 算法求该树的最小代价。

## MST 问题：

给定连通图 G=(V,E) 和权重函数 d:E->R+，求一棵最小生成树 T。

## Kruskal 算法

- 1. 令 i=1，并令 E0={}
- 2. 选择一条不在 Ei-1 中且值最小的边 ei，使得 Ti=<Ei-1 ∪ {ei}> 无环

并定义 Ei=Ei-1 ∪ {ei}。如果这样的边存在，则令 T=<Ei> 并停止。

3. 将 i 替换为 i+1。返回步骤 2。

Kruskal 算法所需时间为 O(|E|log|V|)。

## C.38 已解答试卷

(d) 树中有哪些不同的遍历方式？

答：

树的遍历有三种类型：

- 1. 中序遍历
- 2. 前序遍历
- 3. 后序遍历

中序遍历由以下步骤给出：

- 1. 遍历左子树
- 2. 处理根节点
- 3. 遍历右子树

因此，上图中二叉树的中序遍历为 C—B—A—E—F—D—G。

示例

![](img/65953ea584e494f3d396b2252cb5ea53_539_0.png)

前序遍历定义如下：

- 1. 处理根节点
- 2. 以前序遍历方式遍历左子树
- 3. 以前序遍历方式遍历右子树

前序遍历为 A B C D E F G

示例

![](img/65953ea584e494f3d396b2252cb5ea53_539_1.png)

后序遍历定义如下：

- 1. 遍历左子树
- 2. 遍历右子树
- 3. 处理根节点

步骤 1：通过检查根指针 R 判断树是否为空。如果 R=NULL，则打印树为空，然后打印“tree empty”

步骤 2：如果 leftptr(R)!=NULL，则调用 post-order(leftptr(R))

步骤 3：打印 data(R)。

步骤 4：如果 rightptr(R)!=NULL，则调用 post-order(rightptr(R))

步骤 5：返回

示例

![](img/65953ea584e494f3d396b2252cb5ea53_539_2.png)

## C 语言编程与数据结构 2008 年 5/6 月

1. C 语言中有哪些不同类型的控制语句？请举例说明。

答：控制语句也称为决策语句。它们包括：

- 1. if 语句
- 2. switch 和 break 语句
- 3. 条件运算符语句
- 4. goto 语句

下面我们结合示例详细讨论这些语句。

if 语句是一种强大的决策语句，用于控制语句的执行流程。它有不同实现形式。

一般形式：

```
if(expression)
{
	Statements ;
}
Statements;
```

![](img/65953ea584e494f3d396b2252cb5ea53_540_0.png)

if 表达式

## C.40 已解答试卷

```
Main ()
{
Int a,b,c,d;
float ratio;
printf("enter the values");
scanf("%d%d%d",&a,&b,&c);
if (c!=0)
{
Ratio=(float(a+b)/float(c-d));
Printf("ratio=%f",ratio);
}
}
```

一般形式：

```
If (expression)
{
True block
}
Else
{
False block
}
Statements;
```

![](img/65953ea584e494f3d396b2252cb5ea53_541_0.png)

```
If (c-d!=0)
{
Ratio=float(a+b)/float(c-d);
Printf("ratio=%f",ratio);
}
Else
Printf("c-d is zero");
}
```

## 嵌套 if else 语句

一般形式：

```
If(condition 1)
{
    If(condition 2)
    {
        Statement 1;
    }
    Else
    {
        Statement 2;
    }
}
Else
{
    Statement 3;
}
Statement x;
```

嵌套 if else 系列中涉及条件判断。它包含不止一个 if else 语句。

![](img/65953ea584e494f3d396b2252cb5ea53_542_0.png)

## 示例：

```
Main()
{
    Float a,b,c;
    Printf("enter the values");
    Scanf("%f%f%f",&a,&b,&c);
    Printf("largest value is");
    If(a>b)
    {
        If(a>c)
```

## C.42 已解答试卷

```
Printf("%f", a);
Else
Printf("%f", c);
}
Else
{
If(c>b)
Printf("%f", c);
Else
Printf("%f", b);
}
```

## else if 阶梯

一般形式：

```
If(condition 1)
Statement 1;
Else if(condition 2)
Statement 2;
Else if(condition 3)
Statement 3;
Else if(condition n)
Statement n;
Else
Default statement;
Statements
```

这里，条件从顶部向下依次求值。

```
Cond 1
|
v
Statement 1
|
v
Cond 2
|
v
Statement 2
|
v
Cond 3
|
v
Statement 3
|
v
Statements
|
v
Next Statement
```

示例：

```
Main()
{
 Int units, custno;
```
