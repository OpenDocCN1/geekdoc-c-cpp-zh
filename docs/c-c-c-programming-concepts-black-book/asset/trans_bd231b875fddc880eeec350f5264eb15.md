
```text
B[parentIndex] <- B[childIndex]
B[childIndex] <- temp
else
    do nothing
end
end
end
return B[0...k]
end
```

在前述算法中，首先定义了 Heap_Sort 函数，其中使用 Form_Heap 函数为给定数组 A[n] 构建堆。获得初始堆后，将根元素存储在数组 A[n] 中，该数组用于保存已排序元素。然后，树的根元素被堆 H[n] 的最后一个元素替换。执行该函数后，递归调用 Form_Heap 函数以重建堆。此函数持续执行，直到所有元素都已排序。另一方面，Form_Heap 函数遍历二叉树，比较父节点和子节点的键值。如果任一子节点的键值大于其父节点，则用其子节点的最大键值替换父节点键值。这样便形成了堆。

现在，让我们分析堆排序算法。在堆排序中，复杂度分析基于两个过程：

- 1. 每次从最后位置移除元素后重新构建堆
- 2. 执行初始 for 循环，通过移除根元素并将最后一个元素放到根位置来对数组排序

前者需要 O(log n) 时间，后者需要 O(n) 时间执行。因此，最佳情况和最坏情况的复杂度相同，即 O(n log n)。堆排序算法比归并排序算法更高效，因为它只需要内存来存储堆。然而，堆排序算法仍然存在稳定性问题，因为相等元素的顺序在其执行期间可能改变。这被视为堆排序的缺点之一，同时初学者会觉得这种排序技术有些难以理解。不过，由于它实现了堆和完全树的概念，因此学习它对于理解数据结构概念非常有效且必要。

### 清单 24.38：堆排序代码展示

```c
#include<stdio.h>
#include<conio.h>
#include<alloc.h>

void main()
{
    int *x,i,n;
    int temp;
    void heap(int *,int);
    clrscr();
    fflush(stdin);
    printf("Enter the numbers of array element. . . \n");
    scanf("%d",&n);
    x = (int *)malloc(n * sizeof(int));
    for(i=0;i<n;i++)
    {
        fflush(stdin);
        scanf("%d",&x[i]);
    }

    heap(x,n);
    for(i=n-1;i>=1;i--)
    {
        temp = x[i];
        x[i] = x[0];
        x[0] = temp;
        heap(x,i-1);
    }

    printf("The sorted array is... \n");
    for(i=0;i<n;i++)
    {
        printf("%d\t\t",x[i]);
    }
    free(x);
    getch();
}

void heap(int *a,int n)
{
    int i,temp;
    for(i=n/2;i>=0;i--)
    {
        if(a[(2*i)+1] < a[(2*i)+2] && (2*i+1)<=n && (2*i+2)<=n)
        {
            temp = a[(2*i)+1];
            a[(2*i)+1] = a[(2*i)+2];
            a[(2*i)+2] = temp;
        }
        if(a[(2*i)+1] > a[i] && (2*i+1)<=n && i<=n)
        {
            temp = a[i];
            a[(2*i)+1] = a[i];
            a[i] = temp;
        }
    }
}
```

清单 24.39 展示了使用 C++ 模板实现堆排序：

### 清单 24.39：使用 C++ 模板的堆排序代码展示

```cpp
#include<iostream.h>
#include<conio.h>
template<class T>
class hsort
{
    private:
        T a[50];
    public:
        void insertheap(int n,int item)
        {
            int ptr,par;
            n=n+1;
            a[n-1]=item;
            ptr=n;
            while(ptr!=1)
            {
                par=ptr/2;
                if(a[par]<a[item])
                {
                    a[ptr]=a[par];
                    ptr=par;
                }
                else
                    break;
            }
            a[ptr]=item;
        }
        void display(int n)
        {
            for(int i=1;i<n;i++)
                cout<<a[i]<<" ";
            cout<<a[i]<<" ";
        }
        int deleteheap(int n)
        {
            T t;
            int ptr,l,r;
            if(!(a[1]>a[n] && n==2))
            {
                t=a[1];
                a[1]=a[n];
                a[n]=t;
                n=n-1;
                ptr=1;
                l=2*ptr;
                r=l+1;
                while(l<=n)
                {
                    if(a[l]>a[ptr]||a[r]>a[ptr])
                    {
                        if(a[l]>a[r])
                        {
                            t=a[ptr];
                            a[ptr]=a[l];
                            a[l]=t;
                            ptr=l;
                        }
                        else
                        {
                            t=a[ptr];
                            a[ptr]=a[r];
                            a[r]=t;
                            ptr=r;
                        }
                    }
                    else
                        break;
                    l=2*ptr;
                    r=l+1;
                }
            }
        }
};
```

让我们考虑下图，以理解拓扑排序过程：

![](img/43c5f409f9b17790a628c4b4df854b61_903_0.png)

现在，对图中的每个节点应用这三个步骤，如下所示：

- 1. 计算图中每个节点的入度。计数如下：

    V1 = 0  
    V2 = 3  
    V3 = 1  
    V4 = 2  
    V5 = 1  
    V6 = 2

    由于 V1 的入度为 0，我们从图中删除该节点并将其放入一个单独的数组中。此外，所有出边（{V1, V2}、{V1, V3}、{V1, V4}）都从图中移除。因此，结果图如下所示：

![](img/43c5f409f9b17790a628c4b4df854b61_903_1.png)

- 2. 现在，计算剩余节点的入度，如下所示：

    V2 = 2  
    V3 = 0  
    V4 = 1  
    V5 = 1  
    V6 = 2

    在这种情况下，节点 V3 的入度为 0。因此，我们删除该节点及其出边 {V3, V4}。因此，结果图如下所示：

![](img/43c5f409f9b17790a628c4b4df854b61_903_2.png)

- 3. 再次计算剩余节点的入度，如下所示：

    - V₂ = 2
    - V₄ = 0
    - V₅ = 1
    - V₆ = 2

    在这种情况下，V₄ 的入度为 0。因此，从图中删除 V₄ 及其所有出边 {V₄, V₂}、{V₄, V₅}。此过程之后，结果图如下所示：

![](img/43c5f409f9b17790a628c4b4df854b61_904_0.png)

- 4. 计算剩余图节点的入度，如下所示：

    - V₂ = 1
    - V₅ = 0
    - V₆ = 2

    在这种情况下，V₅ 的入度为 0。因此，从图中删除 V₅ 及其所有出边 {V₅, V₂}、{V₅, V₆}。此过程之后，结果图如下所示：

![](img/43c5f409f9b17790a628c4b4df854b61_904_1.png)

- 5. 在此步骤中，剩余图节点的入度如下：

    - V₂ = 0
    - V₆ = 1

    在这种情况下，V₂ 的入度为 0。因此，从图中删除 V₂ 及其出边 {V₂, V₆}。此过程之后，结果图将只剩下一个节点，如下所示：

![](img/43c5f409f9b17790a628c4b4df854b61_904_2.png)

- 6. 在最后一步中，由于 V₆ 的入度为 0，我们删除该节点。此步骤结束时，节点的线性次序如下：

    {V₁, V₃, V₄, V₅, V₂, V₆}

## 第24章

此外，从源节点 V₁ 到目标节点 V₆ 的遍历如下所示：

![](img/43c5f409f9b17790a628c4b4df854b61_905_0.png)

清单 24.40 展示了图排序的算法表示：

### 清单 24.40：图排序算法展示

```text
function Topological_Sort(Graph G with n nodes)
begin
    Q <- Initialize the array to null to store the
         output topological ordering
    n <- Count of nodes in graph
    inDegree[n] <- Initialize this array to null to
                   store the in-degree of the node
    v <- Initialize an integer that holds the intermediate node.
    H <- G

    while H is not empty do
    begin
        //Step 1
        inDegree[n] <- Store the indegree count of the particular node
        //Step 2
        if(inDegree[n] == 0)
        begin
            //Step 3
            v <- nodes[n]
            n <- n - 1
            remove v and all its outgoing edges from H
            Insert v to Q
        end
    end
end
```

前述算法基于入度计数实现图排序。在算法开始时，声明一个数组 inDegree[] 来保存图中每个节点的入度值。数组 Q 充当输出数组，数组 H 保存图 G，图 G 由数组 nodes[] 组成。对于图中的每个节点，首先计算节点的入度值，然后将其存储在数组 inDegree[] 中。如果任一节点的入度值为零，则从图 H 中删除该节点及其出边，然后将该图节点插入输出数组 Q。此过程将图的节点数减 1，并重复执行，直到图 H 为空。此过程结束时，Q 以排序顺序保存图节点，这些节点形成一条从源点到目标点并经过每个节点的路径。

该算法的复杂度取决于图中包含的节点数和边数。对于具有 N 个节点和 E 条边的图，图排序的复杂度计算为 O(E + V)。因此，对于这种排序技术，最佳情况、最坏情况和平均情况复杂度相同。
