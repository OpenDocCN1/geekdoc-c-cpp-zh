
{
    if(a[i]==element)
    {
        flag=1;
        break;
    }
    i++;
}  //end of while
if(flag)
cout<<" item found";
else
cout<<"item not in the list";
}//end of function
int main()
{
clrscr();
int arr[]={2,3,4,5};
float farr[]={2.5,3.2,4.6,5.9};
char a[]={'a','c','e','g'};
cout<<"integer result"<<endl;
search(arr,14);
cout<<"character result"<<endl;
search(a,'c');
getch();
return 0;
}

为了避免重复编写相同的代码，可以使用函数模板。在接下来的程序中，我们在模板中**使用了两个参数，然而它们的类型相同。**

```
// Program to search the element using generic function
const int size=4;
template<class t>
void search(t a[size], t element)
{
```
int i=0;
int flag=0;
while(i<size)
{
if(a[i]==element)
{
flag=1;
break;
}
i++;
} //end of while
if(flag)
cout<<" item found";
else
cout<<"item not in the list";
}//end of function
int main()
{
clrscr();
int arr[]={2,3,4,5};
float farr[]={2.5,3.2,4.6,5.9};
char a[]={'a','c','e','g'};
cout<<"integer result"<<endl;
search(arr,14);
cout<<"character result"<<endl;
search(a,'c');
cout<<"Float result"<<endl;
search(farr,3.2);
getch();
return 0;
}
```

在上述例子中，我们将函数声明为泛型类型。因此，在调用整数类型时，即 search(arr,14)，它会被转换为整数类型。而在字符数组时，即 search(a,'c')，它会被转换为字符类型。因此，由于模板的创建，同一调用可以用于调用不同类型的数据。

# 使用两个参数的函数模板

与单参数类型的模板函数类似，我们可以创建双参数类型的模板函数。这样，它就能让我们传递两个不同数据类型的参数。

考虑这样一种情况：我们希望根据第二个参数的值（即第二个变量的值的出现次数）来打印第一个参数。第一个参数可以是任何数据类型。下面通过示例来说明这一点：

```
// Function template type, accepting two different types of arguments
template<class type1, class type2>
void display (type1 one, type2 two)
{
int i=0;
while (i<two) {
cout<<one<<"\t";
i++;
} //end of while
}//end of function
int main ()
{
clrscr ();
display ("jitendra", 5);
display (58, 3);
getch ();
return 0;
}
Output
jitendra    jitendra    jitendra    jitendra    jitendra
58    58    58
}
```

在上述程序中，我们首先传递字符串以及该字符串要打印的次数。因此，在调用函数 display ("jitendra", 5) 时，它将显示名字 'jitendra' 5次。在第二次调用中，我们通过 display (58, 3) 传递整数类型，因此，58会打印3次。

# 显著特点

数据结构是计算机科学中极其重要的学科。关于这一主题有许多书籍，它们基于各自的方法论充实着学生们。然而，本书的编写方式使读者可以仅借助本书来学习数据结构。本书的其他特点如下：

+   > 使用简单的语言进行编码。
+   > 主要关注链表、树、栈和队列。
+   > 特别强调递归。
+   > 在大多数情况下，对单个操作同时使用递归和非递归函数。
+   > 使用C++进行编程的面向对象方法。
+   > 每章目标在开头进行讨论。
+   > 代码配有大量图形和描述。
+   > 所有编写的代码均经过测试和执行。
+   > 对新手和专家同样有益。
+   > 每章后面附有案例研究。
+   > 章末包含练习，使读者能够进行自我评估。

Horowitz, E., Sahni, S., & Anderson-Freed, S. (1983). 数据结构基础 (No. 04; QA76. D35, H6.). 伦敦: Pitman.

Horowitz, E., Sahni, S., & Rajasckaran, S. (1996). 计算机算法：C++. WH Freeman & Co.

Kanetkar, Y. (2008). 通过C++学习数据结构.

Kanetkar, Y. P. (2016). 让我们学C. BPB publications.

Lafore, R. (1997). C++面向对象编程. Pearson Education.

Lafore, R. (1999). Sams 24小时自学数据结构和算法（附光盘）. Sams.

Manindra Agrawal, Neeraj Kayal, and Nitin Saxena. PRIMES属于P类问题. 数学年鉴, 160(2):781–793, 2004.

Mehta, D. P., & Sahni, S. (编). (2004). 数据结构与应用手册. CRC Press.

Ravindra K. Ahuja, Kurt Mehlhorn, James B. Orlin, and Robert E. Tarjan. 最短路径问题的更快速算法. ACM杂志, 37:213–223, 1990.

Ravindra K. Ahuja, Thomas L. Magnanti, and James B. Orlin. 网络流：理论,

Selim G. Akl. 并行算法的设计与分析. Prentice Hall, 1989.

Stroustrup, B. (1995). C++编程语言. Pearson Education India.

Structures, D. (1998). C++算法. Adam Drozdek, 4.

Vandevoorde, D., & Josuttis, N. M. (2002). C++模板. Addison-Wesley Longman Publishing Co., Inc.

West, D. B. (2001). 图论导论 (第2卷). Upper Saddle River: Prentice hall.

# 索引

# A

AVL树, 228
接受矩阵, 27
访问指针, 33
访问数组元素, 17
激活记录, 321
地址部分, 44
邻接, 303
邻接矩阵, 304
算法, 4
栈的应用, 142
数组, 15
数组初始化, 19
整数数组, 17
指针数组, 37
数组, 16
广度优先搜索方法, 315
蛮力法, 288
冒泡排序, 263
桶排序, 267

# B

B树, 247
B+树, 255
基本情况, 320
基本术语, 182
大(1), 8
大O, 7
二元递归, 325
二分查找, 261
二叉搜索树, 184
信息块, 321
边界折叠, 295
括号检查, 143

# C

基于双向链表的案例研究, 121
基于链表的案例研究, 87
基于队列的案例研究, 174
基于栈的案例研究, 147
字符元素, 22
循环双向链表, 106
循环链表, 77
循环链表遍历, 79
循环队列, 168
散列中的冲突处理技术, 296
完全平衡二叉树, 184
复杂度, 267
复杂度, 7
连接新节点, 79
构建树, 198
中缀转后缀, 146
复制, 25
计数排序, 268
计算节点数, 109
统计BST中的所有节点, 211
统计元素个数, 157
统计BST中的节点数, 209
统计左半部分节点, 209
统计元素个数, 130

# 参考资料与参考文献

统计节点数, 106
统计右半部分节点, 210
在有序链表中创建并插入节点, 57
创建链表, 44
创建链表, 43
双向链表的创建, 94
二叉搜索树的创建, 184
循环双向链表的创建, 107
根节点的创建, 189
循环双向链表的创建, 108
环, 303
出队, 162
迪杰斯特拉算法, 316
有向图, 301
显示节点, 45
队列的显示, 156
显示双向链表的节点, 95
分治法, 10
二维, 15
双向链表, 93
使用模板的双向链表, 113
动态数组, 36
动态数组, 36
动态栈, 127, 132
使用模板的动态栈, 139
D
数据部分, 44
数据结构, 1
数据结构分类, 181
声明数组, 16
声明指针, 34
声明指针, 32
节点的度, 183
图的度, 302
复制删除, 202
合并删除, 205
删除第一个节点, 53
删除第一个节点, 103
删除节点, 52, 54
从链表中删除节点, 54
从双向链表中删除节点, 102
B树中的删除, 251
节点的删除, 201
节点的删除, 201
深度优先搜索, 314
E
 在开头插入元素, 48
入队, 162
表达式求值, 143
外部排序, 263
提取法, 295
F
错误算法, 4
折叠法, 295
帧, 321
出栈函数, 129
G
图, 300

