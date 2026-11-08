
```cpp
u2=(l2+size-1<n)?l2+size-1:n-1;
for(i=l1,j=l2;i<=u1&&j<=u2;k++)
{
  if(x[i]<=x[j])
    aux[k]=x[i++];
  else
    aux[k]=x[j++];
}
for(;i<=u1;i++)
  aux[k++]=x[i];
for(;j<=u2;j++)
  aux[k++]=x[j];
l1=u2+1;
}
for(i=l1;k<n;i++)
  aux[k++]=x[i];
for(i=0;i<n;i++)
  x[i]=aux[i];
size=size*2;
}
printf("\n\t\tThe sorted elements are:");
for(i=0;i<n;i++)
  printf("%d ",x[i]);
}
getch();
}
```

清单 24.32 展示了使用 C++ 模板实现归并排序：

### 清单 24.32：展示使用 C++ 模板的归并排序代码

```cpp
#include <iostream.h>
#include <conio.h>
template <class T>
class msrt
{
  private:
    T a[50];
    int n;
  public:
    void getdata()
    {
      cout<<endl<<endl<<" Enter the total no. of elements: ";
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
        cout<<a[i]<<"  ";
      cout<<a[n-1]<<"  ";
    }
    void mergesort()
    {
        int h[12],u1,u2,size,i,j,k;
        int aux[50];
        size=1;
        while(size<n)
        {
            k=0;
            l1=0;
            while(l1+size<n)
            {
                l2=l1+size;
                u1=l2-1;
                u2=(l2+size-1<n)?(l2+size-1):(n-1);
                for(i=l1,j=l2;i<=u1 && j<=u2;k++)
                {
                    if(a[i]<a[j])
                        aux[k]=a[i++];
                    else
                        aux[k]=a[j++];
                }
                while(i<=u1)
                    aux[k++]=a[i++];
                while(j<=u2)
                    aux[k++]=a[j++];
                l1=u2+1;
            }
            for(i=0;i<k;i++)
                a[i]=aux[i];
            size=size*2;
        }
    };
void main(void)
{
    msrt<int> q;
    clrscr();
    q.getdata();
    cout<<endl<<endl<<" Your entered sequence: ";
    q.display();
    q.mergesort();
    cout<<endl<<endl<<" Sorted sequence: ";
    q.display();
    getch();
}
```

## 计数排序

计数排序基于元素范围位于 1 到 k 之间的假设。该技术统计具有相同值的元素数量，并通过保持其出现顺序来对它们排序。这是一种线性排序算法，它不执行任何比较；而是根据元素的出现次数对它们排序。计数排序的唯一限制是：如果列表元素的最大值很大，其开销会变得巨大。为了解释计数排序，让我们考虑以下待排序列表：

A = {1, 2, 1, 4, 3, 2, 1}

```text
for m <- 1 to k
begin
    C[m] <- C[m] + C[m-1]
end
//C[m] now contains the number of elements less than or equal to m.
for p <- n downto 1
begin
    B[C[A[p]]] <- A[p]
    C[A[p]] <- C[A[p]] - 1
end
end
```

现在，我们来分析计数排序算法。在该算法中，执行四个循环来使用计数排序对列表排序。第一个循环执行需要 O(k) 时间，第二个循环执行需要 O(i) 时间，第三个循环执行需要 O(p) 时间，第四个循环执行需要 O(m) 时间。因此，如果将所有循环执行的时间累加在一起，完成此操作所需的总时间为 O(k) + O(i) + O(p) + O(m)。该算法的复杂度为 n 阶，即 O(n)。由于计数排序不执行任何比较，最好和最坏情况的行为相同，即 O(n)。

### 清单 24.34：展示计数排序的代码

```c
#include <stdio.h>
#include <conio.h>
void main()
{
    clrscr();
    int i,j,m,a[20],b[20],c[20],max;
    printf("Enter no of elements in an array...\n");
    scanf("%d",&m);
    printf("Enter the array elements...");
    for(i=0;i<=m;i++)
    {
        scanf("%d",&a[i]);
    }
    max=a[1];
    for(i=0;i<=m;i++)
    {
        if(max<a[i])
        {
            max=a[i];
        }
    }
    for(i=0;i<=max;i++)
    {
        c[i]=0;
    }
    for(j=0;j<=m;j++)
    {
        c[a[j]]=c[a[j]]+1;
    }
    for(i=0;i<=max;i++)
    {
        c[i]=c[i]+c[i-1];
    }
    for(j=m;j>=1;j--)
    {
        b[c[a[j]]]=a[j];
        c[a[j]]=c[a[j]]-1;
    }
    printf("\n the sorted list is...\n");
    for(i=0;i<=m;i++)
    {
        printf("%d",b[i]);
    }
    getch();
}
```

## 基数排序

基数排序是最简单的排序技术之一，它根据数组元素的各个数字对元素排序。它实现了一种非比较技术来对列表排序。该技术的基本概念是：首先创建一个桶数组，其大小由用户定义；然后根据元素的各个数字（或根据元素的长度），将元素放入相应的桶中。此过程基于个位创建相关子列表；然后在第二步中创建另一个子列表，并根据元素的十位值将数组元素放入桶中。因此，如果列表元素的最高位数为 3，则此过程会持续到根据百位值对元素排序为止。

基数排序技术使用两个循环：外部循环和内部循环。外部循环执行的次数取决于数组元素的最大长度。另一方面，内部循环执行的次数取决于用户指定的桶值。

让我们用以下元素列表来理解基数排序：

{349, 810, 912, 520, 670, 163, 157, 295}

我们将桶值定义为 10；因此，将有十个桶，其索引从 0 开始。元素将根据数组元素的各个数字放入这些桶中。使用基数排序对元素排序的步骤如下：

- 1. 根据个位元素创建子列表，如下所示：

| 桶索引 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 值 | 810<br>520<br>670 |  | 912 | 163 |  | 295 |  | 157 |  | 349 |

此步骤得到以下子列表：

(810, 520, 670, 912, 163, 295, 157, 349)

- 2. 使用第一步得到的子列表，根据十位元素创建子列表，如下所示：

| 桶索引 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 值 |  | 810<br>912 | 520 |  | 349 | 157 | 163 | 670 |  | 295 |

此步骤得到以下子列表：

(810, 912, 520, 349, 157, 163, 670, 295)

- 3. 使用上一步的子列表，根据百位位置元素创建结果子列表，如下所示：

| 桶索引 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 值 |  | 157<br>163 | 295 | 349 |  | 520 | 670 |  | 810 | 912 |

此步骤得到排序后的数组，如下所示：

(157, 163, 295, 349, 520, 670, 810, 912)

清单 24.35 展示了基数排序的算法表示：

### 清单 24.35：展示基数排序的算法

```text
function Radix_Sort(A[n])
begin
    B[n] <- initialize output queue
    bin <- user defined value for the size of bin array
    length <- maximum length of the array element

    for i <- 0 to i <- length -1
    begin
        for j <- 0 to j <- bin -1
        begin
            radix <- GetRadixValue (A[j], i)
            B[radix].enqueue(A[j])
        end
        for k <- 0 to k <- B.Length
        begin
            while(B[k] is not null)
            begin
                A[pos] <- B[k].dequeue()
                pos++
            end
        end
    end
end
function GetRadixValue(num, position)
begin
    radixVal <- num / Powerof(10, position - 1) mod 10
    return radixVal
end
```

前面的算法实现了基数排序，其中不涉及比较。首先，我们声明桶值，然后声明数组元素的最大长度。该算法从每个数组元素的个位开始。根据个位的值，算法开头声明的 B 队列会以这样的方式填充：B 中第 i 个位置由数组 A 中个位与 i 匹配的元素占据。GetRadixValue() 函数用于获取元素的个位、十位或百位值。当 B 队列填充了输入数组 A 的所有元素后，A 会按正确顺序用 B 中的值重新填充。再次将此技术应用于 A，此时考虑十位。重复此过程，直到数组的每个元素都按正确顺序排序。

现在，我们来分析基数排序算法。在该算法中，外部循环执行 d 次，其中 d 是元素的长度；内部循环执行 n 次，其中 n 是用户提供的桶大小。因此，对列表排序所需的时间为 O(n)。在最坏和最好情况下，该算法的行为相同，因为不发生比较。因此，基数排序是最受推荐的排序算法。
