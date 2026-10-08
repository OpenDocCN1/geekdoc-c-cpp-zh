
```c
            case 4: bk[4]=list[i]; break;

            case 5: bk[5]=list[i]; break;

            case 6: bk[6]=list[i]; break;

            case 7: bk[7]=list[i]; break;

            case 8: bk[8]=list[i]; break;

            case 9: bk[9]=list[i]; break;

        }

    }

    printf("\nThe elements in table are:-");

    printf("\n\tElements\n");

    for(j=0;j<10;j++) {

        printf("\n %d:-",j);

        for(i=0;i<5;i++) {

            if (bk[j]>0) {

                printf("%3d",bk[j]);

                slist[p++]=bk[j];

            }

        }

    }

    printf("\n-------------------");

    printf("\nThe sorted numbers:-");

    for(i=0;i<5;i++)

        printf("%d",slist[i]);

}
```

OUTPUT
Enter one digit: 1 6 8 3 6
The elements in table are:
Bucket 0:-
Bucket 1:-
Bucket 2:-
Bucket 3:- 3
Bucket 4:-
Bucket 5:-
Bucket 6:- 6 6
Bucket 7:-
Bucket 8:- 8
Bucket 9:-
sorted numbers:- 1 6 8 3 6

# Example 11.11 写一个程序使用基数排序对给定的两位数字

```c
#include <stdio.h>
#include <conio.h>
int l[5],flag=0;
void place();
void main() {
    int i,j;
    clrscr();
    printf("\nEnter five elements with two digits:-");
    for(i=0;i<5;i++)
        scanf("%d",&l[i]);
    printf("\nThe first sorted table is:-");
    place();
    printf("\nFirst sorted list :-");
    for(i=0;i<5;i++)
        printf("%3d",l[i]);
    flag=2;
    getch();
    printf("\nThe final sorted table is\n");
    place();
    printf("\nFinal sorted list :-\n");
    for(i=0;i<5;i++)
        printf("%3d",l[i]);
    getch();
}
void place() {
    int k0,k1,k2,k3,k4,k5,k6,k7,k8,k9;
    int a,b,q,r,n,b[10][5]={0};
    k0=k1=k2=k3=k4=k5=k6=k7=k8=k9=a=0;
    while(a<5) {
        if(flag==2)
            n=l[a]/10;
        else
            n=l[a]%10;
        switch(n) {
            case 0: b[0][k0++]=l[a]; break;
            case 1: b[1][k1++]=l[a]; break;
            case 2: b[2][k2++]=l[a]; break;
            case 3: b[3][k3++]=l[a]; break;
            case 4: b[4][k4++]=l[a]; break;
            case 5: b[5][k5++]=l[a]; break;
            case 6: b[6][k6++]=l[a]; break;
            case 7: b[7][k7++]=l[a]; break;
            case 8: b[8][k8++]=l[a]; break;
            case 9: b[9][k9++]=l[a]; break;
        }
        a++;
    }
    r=0;
    for(p=0;p<10;p++) {
        if(b[p][0]!=0) {
            printf("\nBucket %d:-",p);
            for(q=0;q<5;q++) {
                if(b[p][q]!=0) {
                    printf("%3d",b[p][q]);
                    l[r++]=b[p][q];
                }
            }
        }
    }
}
```

OUTPUT
Enter five elements with two digits:-99 12 38 48 10
The first sorted table is:-
Bucket 0:- 10
Bucket 1:- 12
Bucket 3:- 38
Bucket 4:- 48
Bucket 9:- 99
First sorted list :- 10 12 38 48 99
The final sorted table is
Bucket 0:- 10
Bucket 1:- 12
Bucket 3:- 38
Bucket 4:- 48
Bucket 9:- 99
Final sorted list :- 10 12 38 48 99

# 11.28 C 语言数据结构

## 11.11 分区排序

分区排序是一种将元素列表分为两个部分的排序技巧。使用列表中的基准值形成子集。左部分称为左子列表，右部分称为右子列表。对两部分执行快速排序，并将准备好的两个部分合并。例如，考虑以下列表：

+   24, 30, 27, 32, 11, 21, 19。

| 初始列表 | 24 | 30 | 27 | 32 | 11 | 21 | 19 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 选择 24 为基准 | 24 | 30 | 27 | 32 | 11 | 21 | 19 |
| 基准划分为两部分 | 11 | 21 | 19 | 24 | 30 | 27 | 32 |
| 排序后的最终排序列表 | 11 | 19 | 21 | 24 | 27 | 30 | 32 |

图 11.8 显示了分区排序。

# 排序

## 11.29

排序后的左右部分：

11, 19, 21
27, 30, 32

使用主元键（pivot key）合并两个部分后，排序后的列表变为：

11, 19, 21, 24, 27, 30, 32。

下出的程序基于相同的概念。

![](img/c2f6b24e88575cdba9137937a75b3615_436_0.png)

```c
#include <stdio.h>
#include <conio.h>
int q_sort(int items[], int lower, int upper);
void main()
{
    int arr[7],tree[7],rtree[7];
    int i=0,j,pivot,lcount=0,rcount=0;
    clrscr();
    printf("\nEnter the 7 elements:\
```

# 11.30 使用C语言的数据结构

```c
{
  while(items[key]<=items[r] && key!=r)
    r--;
  if( key==r )
    key_placed=1;
  if( items[key] > items[r] )
    {
      temp=items[key];
      items[key]=items[r];
      items[r]=temp;
      key=r;
    }
  while (items[key]>=items[l] && l!=key)
    l++;
    if(key==l)
      key_placed=1;
      if( items[key] < items[l] )
        {
          temp=items[key];
          items[key]=items[l];
          items[l]=temp;
          key=l;
        }
  q_sort(items,lower,key-1);
  q_sort(items,key+1,upper);
  return 0;
}
```

输出
输入 7 个元素:- 24 30 27 32 11 21 19
主元元素:- 24
11 19 24 27 30 32

# 解析：

在此程序中，输入了七个元素并排序到 `arr[]` 中。在选择主元键后，值小于主元的元素被放入 `ltree[]` 中，否则放入 `rtree[]`。然后对该主元键的左侧和右侧元素调用 `q_sort`。在 `q_sort()` 函数中，会检查下界和上界的值。如果下界的值大于上界，则函数终止；剩余元素将进行排序。执行这些操作后，即可获得 `ltree[]` 和 `rtree[]` 的排序列表。

# 总结

- 1. 排序是一个按升序或降序顺序排列记录的过程。
- 2. 本章介绍了各种排序方法的信息；每种方法都通过合适的示例进行了说明。
- 3. 插入排序：在插入排序中，元素被插入到合适的位置。这里可以引用打牌牌的真实例子。牌片按增大顺序排列。值最小的牌片放在最左侧，最大的放在另一侧。在此基础上，其他牌片按升序插入。
- 4. 选择排序：选择列表与交换排序几乎相同。通过应用选择排序，将第一个元素与剩余的 (n-1) 个元素比较。将最小的放在第一个位置。再次将第二个元素与剩余的 (n-2) 个元素比较。如果找到的项目小于剩余的 n-2 个元素中的比较元素，则执行交换操作。在此类排序中，会检查每个数组以找到最小元素并进行交换。
- 5. 泡泡排序：泡泡排序是一种常用的排序算法。在该方法中，比较相邻元素，如果第一个元素大于第二个元素，则进行交换。元素按升序排序。
- 6. 快速排序：它也被称为分区交换排序。这种方法也采用了分而治的技术。元素的主列表被分为两个子列表。列表中的任何元素在快速排序中都可以被标记为主元键。现在，主元将主列表分为两部分。并不要求所选元素必须位于中间。列表中的任何元素都可以充当键元素。中间元素可以获得最佳性能。快速排序的时间消耗取决于键在列表中的位置。
- 7. 树排序：中序排序和堆排序方法在树排序下进行了详细阐述。中序排序方法涉及根据规则排列元素。在该方法中，选择树的第一个元素，然后是节点和右节点。堆的规则规定每个父节点应该更大的值。
- 8. 堆排序：在堆排序中，使用了二叉树，其中节点按照特定的预设顺序排列。规则规定每个节点的值应比其子节点大。可以按照本章给出的图示和示例进行堆排序过程。
- 9. 数位排序：数位排序基于数字的位置。根据数字的位置进行排序。
- 10. 分区交换排序：分区交换排序将元素分为两个子部分。在元素中选择一个主元。值小于主元的元素移向主元的左侧。右部分包含值大于主元的元素。

# 11.32 使用C语言的数据结构 练习题

A. 回答以下：
- 1. 什么是排序？
- 2. 描述各种方法。
- 3. 选择排序和交换排序。
- 4. 解释堆排序。
- 5. 合并排序是如何工作的？
- 6. 数位排序是如何工作的？
- 7. 解释分区排序。
- 8. 解释插入排序。
- 9. 选择排序和插入排序。
- 10. 快速排序是如何工作的？
- 11. 描述树排序。

B. 编写程序：
- 1. 对数字进行选择排序。
- 2. 使用合并排序对名称。
- 3. 对名称进行快速排序并按字母顺序排序。
- 4. 降序选择排序。
- 5. 对数字进行中序排序并按升序排列。
- 6. 使用堆排序数字。
- 7. 对十二个数字进行分区排序。
- 8. 使用数位排序数字。
- 9. 使用泡泡排序指针。
- 10. 对五个数字使用选择方法。
- 11. 使用泡泡排序15个元素。
- 12. 使用插入排序对 32,45,5,78,4,56,10,23 进行降序排序。
- 13. 对元素列表进行排序。
- 14. 使用数位排序数字。
- 15. 使用选择排序对以下数字进行升序排序。

# 排序 11.33

C. 为每项选择合适的选项：

- 1. 按顺序排列记录的过程是
(a) 排序 (c) 索引
(b) 搜索 (d) 以上都不是

- 2. 在插入排序中，数字的移动是：
(a) 将较大的放在数组末尾和开头
(b) 将较大的数字放在右侧
(c) 将较小的放在中间和开头
(d) 以上都不是

- 3. 这种类型的排序将列表分为两个子列表：
(a) 快速排序 (c) 合并排序
(b) 交换排序 (d) 以上都不是

- 4. 交换排序也被称为：
(a) 泡泡排序 (c) 壳排序
(b) 合并排序 (d) 以上都不是

- 5. 在泡泡排序中，排序是通过比较：
(a) 相邻元素 (c) 最后一个和中间元素
(b) 第一个和最后一个元素 (d) 以上都不是

- 6. 在树中，元素通过通过排序：
(a) 中序遍历 (c) 后序遍历
(b) 前序遍历 (d) 以上都不是

- 7. 数位排序方法基于：
(a) 数字的位置 (c) 数字的平方
(b) 数字的立方 (d) 以上都不是

- 8. 使用分区排序元素元素时使用哪种方法？
(a) 泡泡排序 (c) 堆排序
(b) 快速排序 (d) 以上都不是

- 9. 在堆排序中，数字最初排列为：
(a) 升序 (c) 二叉树
(b) 降序 (d) 以上都不是

- 10. 使用合并排序可以排序的列表数量是：
(a) 一个列表 (c) 以上都不是
(b) 多个列表

# 使用 C 语言的数据结构

## D. 以下程序的输出分别是什么？

- 1.
```c
int ns[5],p=0,q=1,temp;
clrscr();
printf("\nEnter 5 elements:-\n");
while(p<5) {
    scanf("%d", &ns[p++]);
    for(q=1;q<p;q++) {
        temp=ns[q];
        for(p=q-1;p>=0&&temp<ns[p];p--)
            ns[p+1]=ns[p];
        ns[q]=temp;
    }
}
printf("\nSorted elements are:-\n");
for(p=0; p<5; p++)
    printf("%d ",ns[p]);
```

- 3.
```c
#include <stdio.h>
#include <conio.h>
void main() {
    int p=0,q,r,num,t,small;
    int arr[5]={12,23,12,321,1,4,2};
    clrscr();
    for(p=0; p<4;p++) {
        small = p;
        for(r=p+1; r<5;r++)
            if(arr[small] > arr[r]) small = r;
        if (p != small) {
            t = arr[p];
            arr[p] = arr[small];
            arr[small] = t;
        }
    }
    printf("\nSorted elements are:-\n");
    for(p=0;p<5;p++)
    printf("%d ",arr[p]);
```

- 2.
```c
#include <stdio.h>
#include <conio.h>
void main() {
    int arr[5]={12,23,122,321,1},i,j,t;
    clrscr();
    for(i=0;i<5;i++)
    for(j=i;j<4;j++)
```

- 4.
![](img/c2f6b24e88575cdba9137937a75b3615_441_0.png)

# 排序

```c
if (arr1[i]>arr1[j+1])
{
    t=arr1[i];
    arr1[i]=arr1[j+1];
    arr1[j+1]=t;
}
for (i=0;i<5;i++)
    printf(" %d",arr1[i]);
} for (n=0;n<5;n++)
{
    sum=sum+12[n];
    p=n-m=0;
    m=m-sum;
    while (m<sum)
{
        for (n=0;n<5;n++)
        {
            if (m==11[n] || m==12[n])
