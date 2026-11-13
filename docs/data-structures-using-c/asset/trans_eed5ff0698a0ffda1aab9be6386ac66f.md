

![](img/a99ec79093c067f0bed8f1086197950e_227_0.png)

### 步骤 1

此步骤在图 6.16 中有所示。

```
NewNode->link = Head;
```

![](img/a99ec79093c067f0bed8f1086197950e_227_1.png)

### 步骤 2

此步骤在图 6.17 中有所示。

```
Head = NewNode;
```

![](img/a99ec79093c067f0bed8f1086197950e_227_2.png)

### 在末尾插入节点

在列表中间插入节点的步骤也适用于在列表末尾插入节点。由于要在最后一个节点之后插入该节点，Prev 是指向最后一个节点的指针。设要插入的节点为 NewNode，如图 6.18 所示。

![](img/a99ec79093c067f0bed8f1086197950e_227_3.png)

- 1. NewNode->link = Prev->link

由于 Prev 是最后一个节点，Prev->link = Null。因此，如果已知 Prev 是最后一个节点（如图 6.19 所示），此步骤可替换为语句 NewNode->link = Null。

![](img/a99ec79093c067f0bed8f1086197950e_228_0.png)

图 6.19 在列表末尾插入节点（步骤 1）

- 2. Prev->link = NewNode;

这将使节点 NewNode 成为 Prev 的后继节点。如图 6.20 所示。

![](img/a99ec79093c067f0bed8f1086197950e_228_1.png)

图 6.20 在列表末尾插入节点（步骤 2）

这将把节点 NewNode 插入到最后一个位置，即使节点 NewNode 成为列表的最后一个节点。

### 通用插入例程

让我们编写一个单一的插入例程，用于在列表中任何随机位置插入一个节点。假设已知要插入节点的位置 i。我们遍历列表直到第 (i – 1) 个节点，以便在第 i 个位置插入新节点。现在，设第 (i – 1) 个节点为由指针 Prev 引用的前驱节点。当已知要插入新节点的前一个或后一个节点（而不是位置）时，该函数可以相应地进行修改。在这种情况下，可以先搜索合适的位置，然后插入节点。程序代码 6.4 对此进行了说明。

```
PROGRAM CODE 6.4
void List :: Insert_at_Pos (Node *NewNode, int position)
{
    Node *temp = Head;
    int count = 1, flag = 1;
    if(position == 1) // inserting at first position
    {
        NewNode->link = temp;
        Head = NewNode; // update head
    }
    else
    {
        while(count != position - 1)
        {
            temp = temp->link;
            if(temp == Null)
            {
                flag = 0; break;
            }
            count++;
        }
        if(flag == 1)
        {
            NewNode->link = temp->link;
            temp->link = NewNode;
        }
        else
            cout << "Position not found" << endl;
    }
}
void main()
{
    int pos;
    Node *NewNode;
    List L1; // L1 is object of list.
    L1.Create();
    L1.Display();
    NewNode = L1.GetNode();
    cout << "Enter position where node is to be inserted"
    << endl;
    cin >> pos;
    L1.Insert_at_Pos(NewNode, pos);
    L1.Display();
}
```

程序代码 6.4 演示了在链表中指定位置插入节点所涉及的步骤。可以编写类似的函数，在指定节点之前或之后插入节点。

## 6.5.3 链表遍历

链表遍历是基本操作，其中列表中的所有元素被依次逐个处理。处理可能涉及检索、搜索、排序、计算长度等等。链表遍历需要一个循环算法（算法 6.1）。要遍历链表，必须从第一个节点开始。我们可以通过指针变量 Head 访问第一个节点。一旦访问了第一个节点，通过其链接字段，可以访问第二个节点；通过第二个节点的链接字段，可以访问第三个节点，依此类推，因为每个节点都指向其后继节点，直到最后一个节点。

- 算法 6.1
- 1. 获取第一个节点的地址，将其称为 current；current = Head.
- 2. 如果 current 为 Null，转到步骤 6。
- 3. 处理当前节点（current 指向的节点）的数据字段。这里，处理可能包括打印数据、更新等等
- 4. 移动到下一个节点-current = current->link（现在 current 应该指向下一个节点。下一个节点的地址在 current 的链接字段中。因此，将 current 设置为 current 的链接字段）
- 5. 转到步骤 2
- 6. 停止

### 非递归方法

链表遍历的非递归函数如程序代码 6.5 所示。

```
PROGRAM CODE 6.5
void Llist :: Traverse()
{ // just displaying the list members
Node *temp = Head;
if(temp == Null)
cout << "Empty List";
else
{
while(temp != Null)
{
cout << temp->data << "\t";
temp = temp->link;
}
}
cout << endl;
}
```

该函数可以被任何函数调用。通过添加几条语句，同一函数也可用于打印、搜索、更新和计算长度。

这里，数据元素不一定只有一个。节点可能包含多个数据元素。让我们以图形方式查看列表 L 的输出。

L = {21, 22, 23}

- 1. Current = Head

![](img/a99ec79093c067f0bed8f1086197950e_231_0.png)

- 2. 执行语句 1 后

![](img/a99ec79093c067f0bed8f1086197950e_231_1.png)

- 3. 由于 current != Null，执行语句 3、4 和 5。

![](img/a99ec79093c067f0bed8f1086197950e_231_2.png)

- 4.

![](img/a99ec79093c067f0bed8f1086197950e_231_3.png)

- 5.

![](img/a99ec79093c067f0bed8f1086197950e_231_4.png)

现在 Current = Null 为真，while 循环条件为假；因此停止。

| 输出 |
|---|
| 21 |
| 21 22 |
| 21 22 23 |

### 递归遍历方法

程序代码 6.6 是遍历链表的递归代码。

```
PROGRAM CODE 6.6
class List
{
private:
    Node *Head, *Tail;
    void Recursive_Traverse(Node *tmp)
    {
        //Recursive traversal code
        if(tmp == Null)
            return;
        cout << tmp->data << " \t";
        Recursive_Traverse(tmp->link);
    }
public:
    void Create();
    void Display();
    void R_Traverse()
    {
        Recursive_Traverse(Head);
        //call to recursive traversal
        cout << endl;
    }
};
void main()
{
    List L1;
    L1.Create();
    L1.R_Traverse();
}
Output:
21 22 23
```

让我们更改程序代码 6.6 中递归遍历函数最后两条语句的顺序。

```
void List :: Recursive_Traverse(Node *tmp)
{
    if(tmp == Null)
        return;
    Recursive_Traverse(tmp->link);
    cout << tmp->data << " \t";
}
```

现在输出会是什么？会是 21 22 23 还是 23 22 21？请自行验证。

## 6.5.4 删除节点

列表中可能存在需要删除的节点。线性列表经常需要插入和删除节点。链表是为此目的最合适的数据结构。我们讨论了如何在列表中插入节点。让我们学习如何从列表中删除节点。

假设要删除的节点包含数据 x。我们需要以下步骤来删除它。设 x = 13，并由指针 Curr 指向它。要删除此节点，所需的链接操作如图 6.21 用虚线所示。

![](img/a99ec79093c067f0bed8f1086197950e_233_0.png)

图 6.21 删除节点的链接操作

要删除节点 Curr，我们需要修改 Curr 与其前驱节点之间的链接，以及 Curr 与其后继节点之间的链接。

我们需要按图 6.21 所示修改它们。Prev 当前指向 Curr 作为其后继节点。由于 Curr 将被删除，应修改 Prev 的链接，使其指向 Curr 的后继节点。这使得 Curr 的后继节点成为 Prev 的后继节点。这样就从链表中删除了节点 Curr。

请注意，我们需要既知道要删除节点的地址，也知道其前驱节点，以便修改链接从而删除该节点。

这可以通过算法 6.2 所示的以下步骤实现。

### 算法 6.2

- 1. 将 Curr 和 Prev 都设置为 Head。
- 2. 遍历列表并搜索要删除的节点。
- 3. 使 Curr 指向要删除的节点，Prev 为其前驱节点。
- 4. 修改 Prev 的链接字段，使其跳过 Curr 并指向其下一个节点。Prev->link = Curr->link
- 5. 释放为节点 Curr 分配的内存。
- 6. 停止

要删除的节点可以位于任何位置。它可能是第一个、中间或最后一个节点。

### 删除第一个节点

删除第一个节点也称为删除头节点。如果要删除第一个位置的节点，则需要修改指向第一个节点的指针（也称为头指针），即 Head。

