

Template<class T>
void MinHeap<T>::insertEle(const T& x)
{
    if (full())
        throw Overflow();
    // Move up
    int newnode = ++cSize;
    int temp;
    for (; newnode > 1 && array[newnode] < array[newnode / 2]; newnode /= 2)
    {
        temp = array[newnode];
        array[newnode] = array[newnode / 2];
        array[newnode / 2] = temp;
    }
    // Ultimately element x is reached to array index of array[newnode].
}

(b) 使用交换操作将元素插入最小堆的方法

**图 11.12 插入元素的方法**

插入元素本可使用交换操作实现。最初，元素应插入新节点，并在元素与其父节点之间进行交换，直到满足最小属性，但一次交换需要三条赋值语句。如果元素上移 m 层，交换所执行的赋值次数将为 3m。上述方法（不使用交换）使用 m + 1 次赋值。使用交换的修改方法如图 11.12(b) 所示。

**使用交换的修改函数：** 将元素 x 插入优先队列，保持堆序。

**使用交换将元素插入最小堆：** 将待插入元素移至其适当位置使用交换操作。最初，通过创建新节点放置待插入元素，使树成为完全二叉树。插入后，如果树是最小堆，则元素不上移。否则，它通过与父节点交换上移，直到满足最小堆属性。

![](img/45784b9f0334626143002ec0d63692fd_345_0.png)

(a) 寻找插入 16 的位置，将 16 暂时插入新节点

![](img/45784b9f0334626143002ec0d63692fd_346_0.png)

(b) 通过交换 33 和 16，元素 16 上移一层

![](img/45784b9f0334626143002ec0d63692fd_346_1.png)

(c) 通过交换 23 和 16，元素 16 上移一层

**图 11.13** 使用交换进行插入

要插入元素 16，在下一个可用的堆位置创建一个新节点（图 11.13(a)）。将 16 插入新节点。该位置的元素 16 将违反最小堆属性。因此，通过与父节点交换将 16 上移。由于新节点的父节点 33 大于 16，交换 33 和 16；16 上移，并用虚线指示：图 11.13(b)。此时（图 11.13(b)），堆不满足最小堆属性。因此，16 需要继续上移。由于 16 的父节点 23 更大，交换 23 和 16（图 11.13(c)），如虚线所示。在图 11.13(c) 中，不需要进一步交换，因为已满足最小堆属性。如果元素一直移动到根节点，将元素插入优先队列的时间最多可能为 O(log N)。

## 11.3.3 最小堆–删除

当删除最小元素时，根节点会创建一个空节点。由于堆树现在比之前的节点数少一个节点，堆中的最后一个元素必须移动到堆中的某个位置。

![](img/45784b9f0334626143002ec0d63692fd_347_0.png)

(a) 删除最小元素 15

![](img/45784b9f0334626143002ec0d63692fd_347_1.png)

(b) 删除最小元素 15 创建了一个空节点

![](img/45784b9f0334626143002ec0d63692fd_347_2.png)

(c) 空节点下移一层

**图 11.14** 删除元素

![](img/45784b9f0334626143002ec0d63692fd_348_0.png)

(d) 空节点再下移一层

![](img/45784b9f0334626143002ec0d63692fd_348_1.png)

元素 33 的位置

(e) 找到插入最后一个元素 33 的位置

![](img/45784b9f0334626143002ec0d63692fd_348_2.png)

(f) 最后一个元素 33 放置在其位置

**图 11.14**（续）

如图 11.14(b) 所示，删除最小元素创建了一个空节点。树中的最后一个元素 33 应该移动到树中的某个位置。将 33 移动到树中的适当位置意味着在将元素 33 放置在其适当位置后确保最小堆属性。

假设最后一个元素 33 放置在空节点中。现在将 33 与其子节点 16 和 18 进行比较（图 11.14(d)）。如果两个子节点都大于或等于其父节点，则下移停止。否则，将空节点向较小的子节点移动。在此例中，它向左移动。因此，16 上移一层（图 11.14(c)。

假设元素 33 放置在空节点中（图 11.14(c)）。在此位置，它不维护最小堆属性。现在将 33 与其子节点 22 和 34 进行比较（图 11.14(c)）。空节点向左移动，用虚线表示（图 11.14(d)）。

假设元素 33 放置在空节点中（图 11.14(e)）。在此位置，它确实维护了最小堆属性。因此，将元素放置在此空节点中（图 11.14(f)）。

从堆中删除具有最小优先级的元素的方法的 C++ 实现如图 11.15 所示。

从优先队列中删除最小元素并重新建堆。

```cpp
Template<class T>
void MinHeap<T>::deleteMin(T& minEle)
{
   if (empty())
      throw Underflow();
   minEle = array[1];
   array[1] = array[cSize--];
   moveDownHeap(1);
}
// Method to move down the heap
// emptynode is the index at which moving down begins
Template<class T>
void MinHeap<T>::moveDownHeap(int emptynode)
{
   int child;
   T temp = array[emptynode];
   for (; emptynode * 2 <= cSize; emptynode = child)
   {
      child = emptynode * 2;
      if (child != cSize && array[child + 1] < array[child])
         child++;
      if (array[child] < temp)
      {
         array[emptynode] = array[child];
      }
      else
         break;
      }
      array[emptynode] = temp;
   }
}
```

**图 11.15**（续）

通过连续插入 N 个元素，可以构建一个最小堆。定义了一个 buildMinHeap() 方法来构建 N 个元素的堆；该方法如图 11.16 所示。

```cpp
explicit MinHeap(const vector<T>& items)
: array(items.size() + 1), cSize(items.size())
{
   for (int i = 0; i < items.size(); i++)
      array[i + 1] = items[i];
   buildMinHeap();
}
Template<class T>
void MinHeap<T>::buildMinHeap()
{
   for (int i = cSize / 2; i >= 0; i--)
      moveDownHeap(i);
}
```

**图 11.16** 从 N 个元素构建最小堆的方法

## 程序 11.1

```cpp
#include<iostream.h>
#include<process.h>
#include<conio.h>
int n, front = 0, rear = 0, i = 0;
class minheap
{
   int a[50], b[50], item, p;
public:
   void minheapinsert();
   void minheapdelete();
   void minheapdisplay();
};
void minheap::minheapinsert()
{
   if (front == ((rear % n) + 1))
   {
      cout << "queue is overflow";
      return;
   }
   cout << "enter element & priority";
   cin >> item >> p;
   if (front == 0)
      front = rear = 1;
   else
      rear = (rear % n) + 1;
   a[rear] = item;
   b[++i] = p;
   for (int j = i - 1; j > 1; j--)
   {
      for (int k = 1; k <= j; k++)
      {
         if (b[k] > b[k + 1])
         {
            b[k] = (b[k] + b[k + 1]) - (b[k + 1] = b[k]);
            a[k] = (a[k] + a[k + 1]) - (a[k + 1] = a[k]);
         }
      }
   }
   cout << "\nelement is inserted successfully.";
}
void minheap::minheapdelete()
{
   if (front == 0)
   {
      cout << "queue is empty";
      return;
   }
   else
   {
      cout << endl << a[front] << " successfully deleted";
      if (front == rear)
         front = rear = 0;
      else
         front = (front % n) + 1;
   }
}
void minheap::minheapdisplay()
{
   int j;
   if (front == 0)
   {
      cout << endl << "queue is underflow";
      return;
   }
   cout << endl << "elements";
   if (front <= rear)
   {
      for (j = front; j <= rear; j++)
         cout << a[j] << " ";
   }
   else
   {
      for (j = front; j <= n; j++)
         cout << a[j] << " ";
      for (j = 1; j <= rear; j++)
         cout << a[j] << " ";
   }
}
```

```cpp
void main()
{
   int op;
   clrscr();
   minheap ob;
   cout << "enter queue size";
   cin >> n;
   while (1)
   {
      cout << "menu\n1.insert\n2.delete\n3.display\n4.exit\n";
      cout << "enter option";
      cin >> op;
      switch (op)
      {
         case 1:
            ob.minheapinsert();
            break;
         case 2:
            ob.minheapdelete();
            break;
         case 3:
            ob.minheapdisplay(); break;
         case 4:
            exit(0); break;
         default:
            cout << "you are entered invalid choice";
      }
   }
}
```

## 输出

```
enter queue size5
menu
1 insert
2 delete
3 display
4 .exit
enter option1
enter element & priority 12
5
:element is inserted successfully:
menu
1.insert
2.delete
3.display
4.exit
enter option1
enter element & priority 11
8
:element is inserted successfully:
menu
1.insert
2.delete
3.display
4.exit
enter option1
enter element & priority 30
2
:element is inserted successfully:
menu
1.insert
2.delete
3.display
4.exit
enter option3
elements 30 12 10
menu
1.insert
2.delete
3.display
4.exit
enter option2
30 successfully deleted
menu
1.insert
2.delete
3.display
4.exit
enter option3
elements 12 10
menu
1.insert
2.delete
3.display
4.exit
enter option4
```

