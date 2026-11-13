

![](img/45784b9f0334626143002ec0d63692fd_174_0.png)

## 算法 5.15: DL_DELETION_SP

- 将 PTR 指向第一个节点
- 检查列表是否为空，如果是则写入 "删除不可能"
- 循环移动到所需节点
- 检查 VALUE
- 将 PTR 设置为 PTR 的 RLINK
- 结束循环
- 当 PTR 的 DATA 等于 VALUE 时
- 将 PPTR 设置为 PTR 的 LLINK
- 将 NPTR 设置为 PTR 的 RLINK
- 将 PPTR 的 RLINK 设置为 NPTR
- 检查被删除节点是否为最后一个节点，如果是
- 将 NPTR 的 LLINK 设置为 NULL
- Return(PTR)
- 结束。

## 程序 5.2

```cpp
#include<iostream.h>
#include<conio.h>
#include<stdio.h>
#include<alloc.h>
template<class t>
class llist
{
struct node
{
t data;
node *flink, *blink;
}*next, *head, *temp, *temp1;
public:
llist();
void insertf();
void inserta();
void inserta();
void deletef();
void deletee();
void fdisplay();
void bdisplay();
};
template<class t>
llist<t>::llist()
{
head->flink=NULL;
head->blink=NULL;
}
template<class t>
void llist<t>::insertf()
{
t ele;
cout<<"enter the element\n";
cin>>ele;
temp=(struct node*) malloc(sizeof(struct node));
if(temp==NULL)
{
cout<<"memory allocation error\n";
return;
}
if(head->flink==NULL)
{
temp->data=ele;
head->flink=temp;
temp->flink=NULL;
temp->blink=head;
}
else
{
temp->flink=head->flink;
temp->blink=head;
head->flink=temp;
temp1=head->flink;
temp1->blink=temp;
}
}
template<class t>
void llist<t>::inserte()
{
t ele;
cout<<"enter the element\n";
cin>>ele;
temp=(struct node*) malloc(sizeof(struct node));
if(temp==NULL)
{
    cout<<"memory allocation error\n";
    return;
}
if(head->flink==NULL)
{
    temp->data=ele;
    head->blink=head;
    head->flink=temp;
    temp->flink=NULL;
}
else
{
    for(temp1=head->flink;temp1->flink!=NULL;temp1=temp1->flink)
    {
        temp1->flink=temp;
        temp->data=ele;
        temp->flink=NULL;
        temp->blink=temp1;
    }
}
template<class t>
void llist<t>::inserta()
{
    t ele;
    int pos,i;
    cout<<"enter the element\n";
    cin>>ele;
    cout<<"enter the position\n";
    cin>>pos;
    temp=(struct node*)malloc(sizeof(struct node));
    if(temp==NULL)
    {
        cout<<"memory allocation error\n";
        return;
    }
    if(head->flink==NULL)
    {
        temp->data=ele;
        head->flink=temp;
        head->blink=head;
        temp->flink=NULL;
    }
    else
    {
        for(temp1=head,i=1;i<pos;i++)
        {
            temp1=temp1->flink;
        }
    }
    temp->flink=temp1->flink;
    temp1->flink=temp;
    temp->data=ele;
    temp->blink=temp1;
    temp1->blink=temp;
}
template<class t>
void llist<t>::deletef()
{
	t ele;
if(head->flink==NULL)
{
	cout<<"linked list is empty\n";
	return;
}
temp=head->flink;
temp1=temp->flink;
head->flink=temp1;
temp1->blink=head;
ele=temp->data;
free(temp);
cout<<"the deleted element is"<<ele<<endl;
}
template<class t>
void llist<t>::deletee()
{
	t ele;
if(head->flink==NULL)
{
	cout<<"linked list is empty\n";
	return;
}
for(temp1=head; temp1->flink!=NULL; temp1=temp1->flink)
{
	temp=temp1;
}
temp->flink=NULL;
ele=temp1->data;
free(temp1);
cout<<"the deleted element is"<<ele<<endl;
}
template<class t>
void llist<t>::deletea()
{
	t ele;
int pos,i;
if(head->flink==NULL)
{
cout<<"linked list is empty\n";
return;
}
cout<<"enter the position\n";
cin>>pos;
for(temp1=head, i=0; i<pos; i++, temp1=temp1->flink)
{
temp=temp1;
}
temp->flink=temp1->flink;
temp=temp1->flink;
temp->blink=temp1->blink;
ele=temp1->data;
cout<<"the deleted element is"<<ele<<endl;
free(temp1);
}
template<class t>
void llist<t>::fdisplay()
{
if(head->flink==NULL)
{
cout<<"linked list is empty\n";
return;
}
for(temp=head->flink; temp!=NULL; temp=temp->flink)
{
cout<<temp->data<<" ";
}
}
template<class t>
void llist<t>::bdisplay()
{
if(head->flink==NULL)
{
cout<<"linked list is empty\n";
return;
}
for(temp=head; temp->flink!=NULL; temp=temp->flink)
{
//cout<<temp->data<<" ";
}
for(temp1=temp; temp1->blink!=NULL; temp1=temp1->blink)
{
cout<<temp1->data<<" ";
}
}
}
void main()
{
 int ch;
 llist<char> l;
 clrscr();
 while(1)
 {
 cout<<"\n\n\n\n";
 cout<<"1.insertion at front\n";
 cout<<"2.insertion at end\n";
 cout<<"3.insertion at any position\n";
 cout<<"4.deletion at front\n";
 cout<<"5.deletion at end\n";
 cout<<"6.deletion at any position\n";
 cout<<"7.fdisplay\n";
 cout<<"8.bdisplay\n";
 cout<<"9.exit\n";
 cout<<"enter your choice\n";
 cin>>ch;
 switch(ch)
 {
 case 1:
 l.insertf();
 break;
 case 2:
 l.inserte();
 break;
 case 3:
 l.inserta();
 break;
 case 4:
 l.deletef();
 break;
 case 5:
 l.deletee();
 break;
 case 6:
 l.deletea();
 break;
 case 7:
 l.fdisplay();
 break;
 case 8:
 l.bdisplay();
 break;
 case 9:
 exit(0);
 }
}
break;
}
}
}
```

## 输出

菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
1
请输入元素
2
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
1
请输入元素
3
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
7
3 2
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
2
请输入元素
5
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
2
请输入元素
6
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
8
6 5 2 3
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
请输入元素
请输入位置
2
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
7
8 2 5 6
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
4
被删除的元素是 3
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
7
8 2 5 6
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
5
被删除的元素是 6
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
7
8 2 5
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择
6
请输入位置
2
被删除的元素是 2
菜单
1.前端插入
2.尾部插入
3.任意位置插入
4.前端删除
5.尾部删除
6.任意位置删除
7.fdisplay
8.bdisplay
9.退出
请输入您的选择

## 5.6 各种链表的比较

本节讨论各种类型链表的比较。

### 5.6.1 链表与数组

链表相对于数组具有多种优势。在列表特定位置插入元素是常数时间操作，而在数组中插入需要将一半或更多元素向下移动。虽然从数组中删除元素只需将其槽标记为“空闲”即可在常数时间内完成，但遍历元素的算法可能需要跳过大量空闲槽。

此外，链表可以插入任意数量的元素，仅受可用总内存限制，而数组最终会填满，然后需要调整大小——这是一项昂贵的操作，如果内存碎片化，甚至可能无法进行。同样，从中删除许多元素的数组可能需要调整大小，以避免浪费太多空间。

另一方面，数组允许随机访问，而链表只允许顺序访问元素。事实上，单链表只能单向遍历。这使得链表不适合需要按索引快速查找元素的应用，例如堆排序。数组上的顺序访问也比链表快，因为它们具有更好的引用局部性，因此能更多地从处理器缓存中受益。

链表的另一个缺点是需要额外的存储空间来保存引用，尤其是对于字符或布尔值等小数据项的列表。为每个新元素单独分配内存也可能很慢，并且使用朴素的分配器时会很浪费，这个问题通常通过使用内存池来解决。

一些混合解决方案试图结合两种表示的优点。展开链表在每个列表节点中存储多个元素，提高缓存性能的同时降低引用的内存开销。

一个突出数组与链表使用优劣的好例子是实现一个解决约瑟夫问题的程序。约瑟夫问题是一种选举方法，其工作原理是让一群人站成一个圆圈。从预定的人开始，绕圈计数 n 次。一旦到达第 m 个人，就将其移出圆圈，并让成员们闭合圆圈。然后再次绕圈计数相同的 n 次，重复此过程，直到只剩下一个人。该人赢得选举。这展示了链表相对于数组的优势和劣势，因为人们处于一个循环链表中；它展示了链表删除节点有多容易，因为它只需重新排列到不同节点的链接。然而，链表在查找下一个要移除的人方面表现不佳，需要遍历列表直到找到那个人。另一方面，数组在删除节点（或元素）方面表现不佳，因为它不能在不将列表中所有元素逐个向上移动一位的情况下删除一个节点。然而，通过直接按其在数组中的位置引用，在圆圈中找到第 n 个人非常容易。

列表排名问题涉及将链表表示高效转换为数组。虽然对于传统计算机来说这很平凡，但使用并行算法解决此问题很复杂。

