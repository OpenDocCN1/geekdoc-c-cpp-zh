

```cpp
cout<<"\\nAVLTREE Operations\\n1.Insert\\n2.Delete\\n3.Traverse\\n";
cout<<"4.Height Of Tree\\n5.Searching\\n6.Exit";
cout<<"\\n\\nEnter Your Option";
cin>>n;
switch(n)
{
 case 1:insert();break;
 case 2:
 if(root==NULL) {cout<<"Tree Is Empty";break;}
 cout<<"\\n1.Delete Leaf Node\\n2.Delete Single Child Node";
 cout<<"\\n\\nEnter Your Option";
 cin>>op;
 switch(op)
 {
 case 1:deleleaf();break;
 case 2:delone();break;
 case 3:goto x;
 default:cout<<"Invalid Choice";
 }
 break;
 case 3:cout<<"Tree Elements Are:";inorder(root);break;
 case 4:height=findheight(root);
 cout<<"Height Of The Tree:"<<height;break;
 case 5:if(root==NULL) {cout<<"Tree Is Empty";break;}
 s=k=0;cout<<"Which Item You Want To Search";
 cin>>item;
 s=searching(root,item);
 if(s==1)
 cout<<"Item"<<item<<"Is Found";
 else
 cout<<"Item"<<item<<"Is Not Found";
 break;
 case 6:exit(0);
 default:cout<<"Invalid Choice";
 }
}
```

## 输出

- AVLTREE 操作
- 1. 插入
- 2. 删除
- 3. 遍历
- 4. 树的高度
- 5. 搜索
- 6. 退出

```
Enter Your Option 1
Enter Item To Be Insert 35
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 20
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 40
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 10
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 22
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 37
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 15
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 25
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 1
Enter Item To Be Insert 36
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 3
Tree Elements Are:10 15 20 22 25 35 36 37 40
1.Delete Leaf Node
2.Delete Single Child Node
Enter Your Option 1
Which Item You Want To Delete 15
Element Is Successfully deleted
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 3
Tree Elements Are:10 20 22 25 35 36 37 40
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 2
1.Delete Leaf Node
2.Delete Single Child Node
Enter Your Option 2
Which Item You Want To Delete 22
Element Is Successfully deleted
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 3
Tree Elements Are:10 20 25 35 36 37 40
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 4
Height Of The Tree:3
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 5
Which Item You Want To Search 37
Item 37 Is Found
AVLTREE Operations
1.Insert
2.Delete
3.Traverse
4.Height Of Tree
5.Searching
6.Exit
Enter Your Option 6
```

## 12.6 应用

自平衡二叉搜索树有众多应用。其基本特征是保持元素有序。因此，它应用于所有需要元素顺序的环境中：

- 1. 优先队列
- 2. 基于元素顺序的关联数组（键值对按插入顺序排列）
- 3. 二叉树排序
- 4. 计算几何中的许多算法，如线段、交点问题和点定位问题
- 5. 互联网路由器

## 摘要

- • 非空二叉搜索树应满足以下属性：
  - 1. 所有元素必须有键，且键必须互不相同。
  - 2. 树左子树中的所有键（如果有）。
  - 3. 树右子树中的所有键（如果有）必须大于根元素。
  - 4. 树的左子树和右子树也必须是二叉搜索树。
- • 二叉搜索树的中序遍历会按升序生成给定元素的有序列表。
- • 二叉搜索树上的操作包括搜索、插入和删除。
- • BST 在顺序列表上执行所有操作时效率很高，时间复杂度为 O(log n)。
- • 二叉搜索树存在易退化为偏树的缺点。
- • 空二叉树是 AVL 树。非空二叉树 T 是 AVL 树，当且仅当：
  - 1. T 的左子树 TL 和右子树 TR 也是 AVL 树，且
  - 2. |h(TL) - h(TR)| <= 1，其中 h(TL) 和 h(TR) 分别是 T 左右子树的高度。
- • 节点 u 的平衡因子 bf(u) 可定义为 bf(u)=h(UL)-h(UR)，其中 h(UL) 是 u 左子树的高度，h(UR) 是 u 右子树的高度。
- • AVL 树和 AVL 搜索树的表示与使用链式表示的二叉树和二叉搜索树非常相似。
- • 搜索、插入和删除是 AVL 树上的常见操作。
- • AVL 树上的插入操作与 BST 类似，但会导致不平衡。LL、LR、RL、RR 旋转用于重新平衡树。
- • AVL 树上的删除操作也会执行一些旋转。

## 练习

### 填空题

- 1. 从根节点到外部节点的路径称为 _______。
- 2. 由表示键的内部节点和表示空指针的外部节点组成的二叉搜索树链式表示称为 _______。
- 3. 偏斜二叉搜索树的时间复杂度为 _______。
- 4. AVL 树删除操作中旋转的主要分类是 _______。
- 5. _______ 是向 AVL 树中插入元素时执行的旋转。

### 选择题

- 1. 在假设频繁插入和/或删除的平均情况下，_______ 的时间复杂度。
  - a. O(log n)
  - b. O(n)
  - c. O(n log n)
  - d. 无

- 2. 以下哪种遍历技术按升序列出二叉树的节点？
  - a. 后序遍历
  - b. 中序遍历
  - c. 前序遍历
  - d. 无

- 3. 考虑这棵二叉搜索树：

![](img/45784b9f0334626143002ec0d63692fd_419_0.png)

- 假设我们删除根节点，并用左子树中的某个节点替换它，新的根节点将是什么？
  - a. 1
  - b. 2
  - c. 4
  - d. 5
  - e. 16

- 4. 节点 u 的平衡因子 bf(u) 可定义为 _______。
  - a. bf(u_l)-h(u_r)
  - b. bf(u)-h(u_l)-h(u_r)
  - c. bf(u_l)+h(u_l)-h(u_r)
  - d. bf(u_l)+h(u_l)-h(u_r)

- 5. 以下哪项陈述是正确的？
  - a. AVL 搜索树在删除后可能需要一次旋转来重新平衡。
  - b. AVL 搜索树可能需要多次旋转，插入只需要单次旋转。
  - c. AVL 搜索树在删除后可能需要多次旋转来重新平衡。
  - d. 无。

### 简答题

- 1. 定义二叉搜索树。
- 2. 定义 AVL 树。
- 3. 假设我们想要创建一棵二叉搜索树，其中每个节点包含名为 Item 的某种数据类型的信息（该类型具有默认构造函数和正确的值语义），Item 数据类型还需要什么额外因素？
- 4. 假设二叉搜索树中包含数字 42 作为带有两个子节点的节点。用两三句清晰的话描述从树中删除 42 所需的过程。
- 5. 考虑以下 AVL 树：

![](img/45784b9f0334626143002ec0d63692fd_420_0.png)

在以下每种操作下显示修改后的树：
删除键 4
插入键 16。

### 论述题

- 1. 详细解释二叉搜索树及其操作。
- 2. 详细讨论 AVL 树。
- 3. 给出向 AVL 树中插入元素时涉及的各种旋转的表示。
- 4. 编写 AVL 树删除操作的算法。
- 5. 解释从 AVL 树中删除元素时涉及的各种旋转。

