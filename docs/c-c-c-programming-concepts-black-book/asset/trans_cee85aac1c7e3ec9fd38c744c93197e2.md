

```
num1 <= num2
num2 <= temp
end
```

前面的算法按升序对元素列表进行排序。首先，它计算列表的最小和最大索引。之后，调用 Partition_List 函数，根据选定的基准值将列表划分为两部分。左侧分区包含值小于基准值的元素，右侧分区包含值大于基准值的元素。然后，对这两个分区递归应用快速排序技术。最终，列表中的所有元素都按升序排序。

在 Partition_List 函数中，列表的第一个元素被选作基准。比较基于该基准值进行。在此函数中，两个变量 i 和 j 分别保存列表的最小和最大索引。如果基准值大于列表中的第 i 个元素，则 i 的值递增。此外，如果基准值小于列表中的第 j 个元素，则 j 的值递减。如果在任意时刻这两个条件之一不满足，则第 i 个和第 j 个元素交换位置，因为第 j 个元素小于第 i 个元素。这两个过程持续进行，直到 i 小于 j。如果在任意时刻 i 的值大于 j，则第 i 个元素与基准值交换，因为第 i 个元素的值大于基准值。该过程根据基准值对列表进行分区。

现在，让我们分析快速排序算法。在分析快速排序算法时，我们先关注其最佳情况行为。快速排序的行为取决于基准的选择。在最佳情况下，基准的选择使得每次分区都产生长度相同的子列表。因此，所需的递归调用次数为 log n。在对列表进行分区时，该操作会遍历数组元素，其复杂度为 O(n)。因此，在最佳情况下，快速排序花费 O(n log n) 时间。快速排序的平均情况行为也与最佳情况行为相同，均为 O(n log n)。

在最坏情况下，基准的选择使得分区产生长度分别为 1 和 n-1 的两个子列表。因此，其行为将与冒泡排序相同。在这种情况下，第 i 个元素在 O(n-i) 时间内完成排序。执行顺序可计算如下：

1 + 2 + 3 + ... + (n - 1) + n = n(n - 1)/2 = O(n^2)

代码清单 24.28 展示了 C 语言中快速排序的实现：

### 代码清单 24.28：展示 C 语言快速排序的代码

```c
#include<stdio.h>
#include<conio.h>
void quick();
struct node
{
int low;
int up;
};
struct node stack[20];
int a[20],i,m,n,j,l,r,beg,end,temp;
void main()
{
int top=0;
clrscr();
printf("\n\n\t\tenter the number of elements that is to be sorted:=>");
scanf("%d",&n);
for(i=0;i<n;i++)
{
printf("\n\n\t\tenter the a[%d]th element:=>",i);
scanf("%d",&a[i]);
}
if(n>1)
{
top=top+1;
stack[top].low=0 ;
stack[top].up=n-1;
}
while(top!=0)
{
beg=stack[top].low;
end=stack[top].up;
top=top-1;
quick();
if(beg<m-1)
{
top=top+1;
stack[top].low=beg;
stack[top].up=m-1;
}
if(m+1<end)
{
top=top+1;
stack[top].low=m+1;
stack[top].up=end;
}
}
for(i=0;i<n;i++)
{
printf("%d",a[i]);
}
getch();
}
void quick()
{
l=0;
r=n-1;
i=1;
j=r+1;
m=1;
if(l<r)
{
do
{
i=i+1;
}while(a[i]<a[m]);
do
{
j=j-1;
}while(a[j]>a[m]) ;
if(i<j)
{temp=a[i];
a[i]=a[j];
a[j]=temp;
}
else
{temp=a[m];
a[m]=a[j];
a[j]=temp;
m=j;
}
}
}
```

代码清单 24.29 展示了使用 C++ 模板的快速排序实现：

### 代码清单 24.29：展示使用 C++ 模板的快速排序代码

```cpp
#include<iostream.h>
#include<conio.h>
template<class T>
class qsrt
{
    private:
        T a[50];
        int n;
    public:
        void getdata()
        {
            cout<<endl<<endl<<" Enter the total no. of terms: ";
            cin>>n;
            for(int i=0;i<n;i++)
            {
                cout<<endl<<" Enter element no. "<<i+1<<" : ";
                cin>>a[i];
            }
        }
        void display()
        {
            for(int i=0;i<n-1;i++)
            cout<<a[i]<<" , ";
            cout<<a[n-1]<<" .";
        }
        void quicksort()
        {
            int l[50],u[50],top=-1,i,pos,beg,end;
            top=0;
            l[top]=0;
            u[top]=n-1;
            while(top!=-1)
            {
                beg=l[top];
                end=u[top];
                top=top-1;
                pos=quick(beg,end);
                if(pos>(beg+1))
                {
                    top++;
                    l[top]=beg;
                    u[top]=pos-1;
                }
                if(pos<(end-1))
                {
                    top++;
                    l[top]=pos+1;
                    u[top]=end;
                }
            }
        }
        int quick(int left,int right)
        {
            T t;
            int pos;
            pos=left;
            while(left<=right)
            {
                while(a[pos]<=a[right] && pos!=right)
                    right=right-1;
                if(pos==right)
                    return pos;
                t=a[pos];
                a[pos]=a[right];
                a[right]=t;
                pos=right;
                while(a[pos]>=a[left]&&pos!=left)
                    left++;
                if(pos==left)
                    return pos;
                t=a[pos];
                a[pos]=a[left];
                a[left]=t;
                pos=left;
            }
        }
};
void main(void)
{
    qsrt<int> q;
    clrscr();
    q.getdata();
    cout<<endl<<endl<<" Your entered sequence:-> ";
    q.display();
    q.quicksort();
    cout<<endl<<endl<<" Sorted sequence:-> ";
    q.display();
    getch();
}
```

## 归并排序

归并排序是另一种基于分治策略的排序技术。在划分步骤中，它将数组分成大小相同的两半。在解决步骤中，通过对两个子数组递归应用排序技术来处理它们。在该过程结束时，将已排序的子数组合并，直到恢复为初始数组的原始大小。通过这种方式，得到排序后的数组。

由于归并排序遵循分治范式的三个步骤，我们可以将归并排序技术表示如下：

- 1. 将数组 A[n] 分成两半。
- 2. 继续划分，直到只剩下一个元素，该元素自身即视为已排序。
- 3. 将已排序的子数组合并为一个，并继续合并，直到达到数组的实际长度。该过程将得到排序后的数组。

```
L <- L.InsertLast(L2.Remove(L2.First()))
end
while(L1 != null)
begin
  L <- L.InsertLast(L1.Remove(L1.First()))
end
while(L2 != null)
begin
  L <- L.InsertLast(L2.Remove(L2.First()))
end
return L
end
```

在前面的算法中，首先对列表进行划分，使得划分结束时得到的多个分区数量等于列表元素的数量。通过递归调用 MergeSort_Partition() 函数，对列表进行划分。当列表被划分为单个元素后，执行 Merge() 函数。在此函数中，我们从 L1 和 L2 中取出较小的元素，并将它们紧接在结果数组中前一个元素的右侧放置。如果此移除操作使一个列表变空，则将另一个列表中的剩余元素追加到结果列表中。重复此过程，直到整个列表排序完成。

现在，让我们分析归并排序算法。在分治排序技术家族中，归并排序是最高效的排序算法，因为即使在其最坏情况下，复杂度也是 O(n log n)。其原因在于，如果列表按逆序排序，那么

- O(log n) 时间用于划分列表
- O(n) 时间用于合并两个分区

因此，该算法的总复杂度为 O(n log n)。在最佳情况下，由于无论元素顺序如何都会进行划分和合并，因此复杂度为 O(n log n)。因此，可以说归并排序很有用，因为无论元素顺序如何它都很快，并且易于理解和实现。

代码清单 24.31 展示了 C 语言中归并排序的实现：

### 代码清单 24.31：展示归并排序的代码

```c
#include<stdio.h>
#include<conio.h>
void main()
{
 int size=1,l1,l2,k,aux[20],x[20],u1,u2,n,i,j;
 clrscr();
 printf("\n\t\tEnter the number of elements that is to be sorted");
 scanf("%d",&n);
 for(i=0;i<n;i++)
 {
  printf("\n\t\tEnter the a[%d]th element",i);
  scanf("%d",&x[i]);
 }
 while(size<n)
 {
  l1=0;
  k=0;
  while(l1+size<n)
  {
   l2=l1+size;
   u1=l2-1;
```

