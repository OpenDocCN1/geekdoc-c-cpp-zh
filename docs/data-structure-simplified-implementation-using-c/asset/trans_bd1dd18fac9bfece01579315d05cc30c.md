

```cpp
}

    return flag;
}
```

在上面的程序中，我们声明了一个变量 `flag` 来表示要搜索条目的状态。我们将其初始化为 `'0'`，表示该条目不在列表中。如果在双向链表中找到了要搜索的条目，循环会借助 `break` 语句立即终止，并将 `flag` 的状态设置为新值 `1`，表示该条目位于链表中。最后，将 `flag` 的状态返回给调用者。

## 4.8 计算双向链表中的节点数

在许多情况下都需要计算双向链表中的节点数，例如，了解双向链表的长度、在插入节点时、在删除节点时等。因此，计算节点数是双向链表中的一个重要函数。计算双向链表中的所有节点并不复杂。这里，用户必须从第一个节点开始，一直到达最后一个节点。在遍历节点时需要计数。由于双向链表支持双向遍历，我们也可以从末尾开始遍历来计算节点数。在这种遍历过程中，我们可以使用 `previous` 指针到达第一个节点，同时可以计算双向链表中的节点数。然而，在我们的示例中，我们考虑的是从开始节点向末尾节点进行遍历。下面的程序对此进行了说明。

```cpp
// Program to count the number of nodes in a doubly link list
Solution:
int count()
{
    dnode *current = first;
    int cnt = 0;
    while (current != NULL)       // till the doubly link list is not exhausted
    {
        cnt++;                    // count the node
        current = current->next;  // move to the next node
    }
    return cnt;
}
```

## 4.9 循环双向链表

尽管双向链表允许双向遍历，但有时我们需要将最后一个节点连接到第一个节点。这种类型的双向链表被称为循环双向链表。双向链表具有以下优点。

-   没有任何空指针。
-   提高效率，特别是当需要从最后一个节点向第一个节点遍历时。
-   提高性能，如果要求从第一个节点向最后一个节点方向遍历的话。

循环双向链表如图 4.7 所示。

![](img/9b7c80a1312a664ae505ba138aa3306b_123_0.png)

### 4.9.1 创建循环链表

创建循环双向链表不同于创建普通的双向链表。一旦创建了第一个节点，与双向链表不同，我们不会将 `previous` 和 `next` 指针指向 `NULL`。相反，我们将它们连接到节点本身。这一点已在图 4.7(a) 中说明。一旦创建了第二个节点，它的前驱节点会连接到第一个节点。第一个节点的指针也需要调整，因为第一个（现有）节点的 `next` 指针将指向这个新节点，而这个新节点的 `next` 指针需要指向第一个节点。插入、删除和遍历等操作可以像普通链表一样执行。在循环双向链表上执行各种操作（函数）的类已在下面的程序中描述。

```cpp
#include <iostream.h>
#include <conio.h>

// class to define the structure of a node in a doubly link list
class dnode
{
public:
    int data;
    dnode *prev;
    dnode *next;
};

// Class for the doubly link list
class dblyList
{
    dnode *first;
    dnode *end;
public:
    dblyList()
    {
        first = NULL;
        end = NULL;
    }
    void create(int);
    void display();
    void insert(int, int);
    int count();
    void deletenode(int);
};
```

### 4.9.2 创建循环双向链表的函数

在创建循环双向链表时，我们假设有两个指针，即 `first` 和 `end`。这两个指针分别代表循环双向链表的第一个节点和最后一个节点。通过使用 `last` 的 `next`，我们可以到达循环双向链表的第一个节点。相应地，我们也可以通过 `first` 的 `previous` 到达最后一个节点。当创建第一个节点且双向链表只有一个节点时，在这种情况下，`first` 和 `last` 节点都将指向同一个节点。要插入其他节点，需要将 `last` 的指针和 `first` 节点的 `previous` 指针连接到新创建的 `newnode`。完整程序如下所示。

```cpp
// Prob: Write a program to create the first node or any other node

// To create the first node
void create(int element)
{
    if (first == NULL)
    {
        first = new dnode;
        first->data = element;
        first->next = first;
        first->prev = first;
        end = first;
        return;
    } // end of if statement

    dnode *newnode;            // to create any other node
    newnode = new dnode;
    newnode->data = element;
    newnode->next = end->next;
    newnode->prev = end;
    end->next = newnode;
    first->prev = newnode;
    end = newnode;
}
```

将节点插入循环双向链表后，我们需要查看循环双向链表中可用的数据。这个目标可以通过 `display` 函数来实现。在 `display` 函数中，需要格外小心，以避免无限循环。由于在循环双向链表中，最后一个节点连接到第一个节点，因此循环必须在 `end` 节点处终止；否则，将导致无限循环。

```cpp
void dblyList::display()
{
    dnode *current = first;
    while (current->next != first)
    {
        cout << current->data << "->";
        current = current->next;
    }
    // to display the data of the last node
    cout << current->data << "->";
}
```

### 4.9.3 计算循环双向链表中的节点数

要计算循环双向链表中的节点数，我们需要从前面或后面开始遍历。在循环双向链表中，由于第一个节点连接到最后一个节点，而最后一个节点指向第一个节点，因此，在遍历过程中需要格外小心，以防止循环。在我们的例子中，我们应用了条件，从而检查我们是否尚未到达开始遍历时的节点。实现此效果的函数如下所示：

```cpp
// To count the number of nodes in a doubly link list
int dblyList::count()
{
    // initialize the count to 0
    int c = 0;
    // store the address of first to the current node
    dnode *current = first;
    // run the loop till we are not reaching the first node
    while (current->next != first)
    {
        c++;       // increment the count
        // move the pointer to the next node
        current = current->next;
    }

    // One node was left due to current->next, count that node also;
    c = c + 1;
    return c;
}
```

变量 `c` 表示计数；最初，该值为零，因此已将其初始化为零。在访问每个节点期间，我们将此变量的值加一。由于我们在最后一个节点处终止，因此没有到达该节点。为了计算这个节点，我们将变量 `c` 的当前值加 1。最后，将 `c` 的值返回给调用者。

### 4.9.4 在给定位置插入节点

在循环链表中插入节点时，我们需要确保插入后循环属性不会丢失。这一点尤其适用于在第一个位置或最后一个位置插入节点的情况。当要插入的节点在中间时，循环双向链表与双向链表之间没有区别。在循环链表中插入节点的完整过程如下所述：

-   确定要插入新节点的位置是否有效（必须位于第一个节点和最后一个节点加一之间）。
-   如果要插入节点的位置是第一个，将 `newnode` 的前驱节点连接到现有 `first` 节点的前驱节点。将 `next` 指针连接到 `first` 节点。通过将 `first` 指针移动到这个 `newnode`，将此 `newnode` 命名为第一个节点。类似地，将 `last` 节点的 `next` 指针更改为此 `newnode`（即第一个节点）。
-   要在中间插入节点（第一个和最后一个节点除外），将 `newnode` 的 `next` 指针替换为当前节点（`newnode` 将插入其后的节点）的 `next` 指针。将 `newnode` 的前驱节点连接到当前节点。将当前节点的 `next` 指针连接到 `newnode`。
-   要在末尾位置插入，将此 `newnode` 的 `next` 指针替换为 `end` 节点现有的 `next` 指针（该指针指向第一个节点）。将现有 `end` 节点的 `next` 指针连接到 `newnode`（这将作为最后一个节点），将 `newnode` 的前驱节点连接到现有的最后一个节点。最后，将 `end` 节点移动到此 `newnode`。

演示整个操作的程序如下所示：

```cpp
// To insert the node at a given position
void dblyList::insert(int element, int pos)
{
    int n = count();
    dnode *current, *temp;
    temp = new dnode;
    temp->data = element;
    if (pos <= (n + 1))
    {
        if (pos == (n + 1))
        {    // insert at the end
            temp->prev = end;
            temp->next = end->next;
            end->next = temp;
            first->prev = temp;
            end = temp;
        }
        else
        {
            current = first;
            int i = 1;
            while (i < pos)
            {

```

