

```cpp
LinkedList<T>& operator=(const LinkedList<T>& L);
//重载赋值运算符 "="
```

```cpp
int ListSize(void) const; //返回链表中元素的
//个数(size)
```

```cpp
int ListEmpty(void) const; //当 size 等于 0 时返回 TRUE，
//否则返回 FALSE
```

```cpp
void Reset(int pos = 0); //将指针 currPtr 移动到
//索引为 pos 的元素，prevPtr 根据
//相对位置变化并记录
//当前节点的索引
```

```cpp
void Next(void); //让 prevPtr 和 currPtr 移动到
//下一个节点
```

```cpp
int EndOfList(void) const; //当 currPtr 等于
//NULL 时返回 TRUE，否则返回 FALSE
```

```cpp
int CurrentPosition(void) const; //返回数据成员所在的位置
```

```cpp
void InsertFront(const T& item); //在链表头部插入节点
void InsertRear(const T& item); //在链表尾部插入节点
void InsertAt(const T& item); //在当前节点之前插入节点
void InsertAfter(const T& item); //在当前节点之后插入节点
```

```cpp
T DeleteFront(void); //删除链表头
void DeleteAt(void); //删除当前节点
```

```cpp
T& Data(void); //返回当前节点数据成员的
//引用（使数据成员能够被//访问或修改）
```

```cpp
//清空链表：释放每个节点的内存空间。
//将由析构函数和运算符 = 调用
void ClearList(void);
```

```cpp
#endif //LINKLIST_CLASS
```

# 3. 应用

示例 9.7：链表的应用。

该程序旨在执行以下操作：从键盘获取 10 个整数，
创建一个节点持有这些整数的链表，并按顺序输出这些数字。

然后从键盘获取另一个数字，删除所有包含该数字的节点并输出链表中的数据，最后在退出前清空链表。

```cpp
//9_7.cpp
#include <iostream>
#include "9_6.h"
#include "9_6.cpp"
namespace std;

int main()
{
    LinkedList<int> Link;
    int i, key, item;
    // 输入 10 个整数并将它们逐个插入链表头部
    for(i=0;i<10;i++)
    {
        cin>>item;
        Link.Insert(item);
    }
    // 输出链表
    cout << "List: ";
    Link.Reset();
    // 输出每个节点的数据，直到链表末尾
    while(!Link.EndOfList())
    {
        cout <<Link.Data() << " ";
        Link.Next();//让 currPtr 指向下一个节点
    }
    // 输入要删除的数字
    cout << "Please input the number to delete: ";
    cin >> key;

    // 查找并删除节点
    Link.Reset();
    while (!Link.EndOfList())
    {
        if(Link.Data() == key)
            Link.DeleteAt();
        Link.Next();
    }
}
```

```cpp
// 输出链表
cout << "List: ";
Link.Reset();
// 输出每个节点的数据，直到链表末尾
while(!Link.EndOfList()) {
    cout << Link.Data() << " ";
    Link.Next(); // 让 currPtr 指向下一个节点
}
cout << endl;
```

运行结果：

3 6 5 7 2 4 5 9 10
List: 10 9 5 4 2 7 5 6 3
nPlease input the number to delete: 5
List: 10 9 4 2 7 6 3

# 9.2.4 栈

如 9.2.1 节所述，栈是一种具有受限访问的特殊线性集合。可以通过数组或链表来实现栈。栈的访问模式是受限的，因此栈类需要定义栈的接口。

栈的状态包括：空、满。当栈达到最大容量时，它是满的。可以通过数组或链表来实现，提供了这些操作：

- 初始化栈
- 向栈推送数据
- 从栈弹出数据
- 清空栈
- 访问栈顶
- 检测栈是否为空
- 检测栈是否为满

示例展示了如何用数组实现栈。也可以用链表来实现栈，这被留作练习题。

