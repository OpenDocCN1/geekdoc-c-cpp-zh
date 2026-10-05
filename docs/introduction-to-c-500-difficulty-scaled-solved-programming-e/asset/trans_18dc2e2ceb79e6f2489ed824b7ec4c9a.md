

# C++ 简介

```cpp
int main()
{
    Book *books_ptr;
    char str[100];
    int i, num, len;

    cout << "Enter number of books: ";
    cin >> num;
    cin.get();

    books_ptr = new Book[num];
    for(i = 0; i < num; i++) {
        cout << "\nTitle: ";
        cin.getline(str, sizeof(str));
        len = strlen(str);
        books_ptr[i].title = new char[len+1];
        strcpy(books_ptr[i].title, str);

        cout << "Authors: ";
        cin.getline(str, sizeof(str));
        len = strlen(str);
        books_ptr[i].auth = new char[len+1];
        strcpy(books_ptr[i].auth, str);

        cout << "Code: ";
        cin.getline(str, sizeof(str));
        len = strlen(str);
        books_ptr[i].code = new char[len+1];
        strcpy(books_ptr[i].code, str);

        cout << "Price: ";
        cin >> books_ptr[i].prc;
        cin.get();
        // 分配出版社的内存。
        books_ptr[i].pub_ptr = new Publisher;

        cout << "Name: ";
        cin.getline(str, sizeof(str));
        len = strlen(str);
        (books_ptr[i].pub_ptr)->name = new char[len+1];
        strcpy((books_ptr[i].pub_ptr)->name, str);

        cout << "Address: ";
        cin.getline(str, sizeof(str));
        len = strlen(str);
        (books_ptr[i].pub_ptr)->addr = new char[len+1];
        strcpy((books_ptr[i].pub_ptr)->addr, str);

        cout << "Phone: ";
        cin.getline(str, sizeof(str));
        len = strlen(str);
        (books_ptr[i].pub_ptr)->phone = new char[len+1];
        strcpy((books_ptr[i].pub_ptr)->phone, str);
    }
    cout << "\nEnter code to search: ";
    cin.getline(str, sizeof(str));
```

# 14 内存管理与数据结构

```cpp
for(i = 0; i < num; i++)
{
    if(strcmp(books_ptr[i].code, str) == 0)
    {
        cout << "\nTitle:\" << books_ptr[i].title << "\tPublisher:" <<
    << (books_ptr[i].pub_ptr)->name << '\t\n';
        break;
    }
}
if(i == num)
    cout << "\nCode isn't registered\n";

for(i = 0; i < num; i++)
{
    delete books_ptr[i].pub_ptr->name;
    delete books_ptr[i].pub_ptr->addr;
    delete books_ptr[i].pub_ptr->phone;

    delete books_ptr[i].title;
    delete books_ptr[i].auth;
    delete books_ptr[i].code;
    delete books_ptr[i].pub_ptr;
}
delete[] books_ptr;
return 0;
```

# 动态数据结构

到目前为止我们遇到的数据结构是为了以简单快速的方式进行数据存储和处理。例如，数组是数据结构，用于存储相同类型的数据。结构体（Structures）和联合体（unions）也是数据结构，可以用于存储任何类型的数据。这些数据结构是静态的，因为分配的内存是固定的，在程序执行期间无法进行修改。然而，在许多应用程序中，使用动态数据结构更高效，动态数据结构的大小可以根据需要增长或缩小。

接下来的章节将向你介绍一些动态数据结构的形式。标准库提供了许多此类结构（例如 `list`），我们可以在程序中使用它们。然而，为了更熟悉如何管理动态内存，我们不会使用这些开箱即用的工具，而是将尝试从头实现一些简单的数据结构，以感受背后的运行机制。

# 链表

链表由一系列连接的元素组成，称为节点（nodes）。每个节点通常由一个结构体表示，包含其数据以及指向链中下一个节点的指针，如下图所示：

![](img/25e0e40b08b8016a58f1aab13ac2e81_439_0.png)

# C++ 简介

第一个节点是链表的头节点（head），最后一个是尾节点（tail）。最后一个节点的值为 `nullptr` 表示链表的结束。

与固定的数组不同，链表更加灵活，因为它的大小可以根据需要调整。我们可以轻松地在链表的任何位置插入和删除节点。另一方面，访问数组元素必须从头开始，这是很慢的。

# 插入节点

新节点可以插入到链表的任何位置。为了插入节点，我们检查以下情况：

1. 如果列表为空，将其插入头部并成为新的头节点。
2. 如果列表不为空，检查以下子情况：
    a. 插入到头部，成为新的头节点。
    b. 插入到尾部，成为新的尾节点。
    c. 插入到节点之间，成为中间节点。该操作如图所示：

![](img/25e0e40b08b8016a58f1aab13ac2e81_440_0.png)

# 删除节点

从列表中删除节点并释放内存，我们检查以下情况：

1. 如果是头节点，检查以下情况：
    a. 有下一个节点，成为新的头节点。
    b. 没有下一个节点，列表为空。
2. 如果是尾节点，成为新的尾节点。
3. 如果是中间节点，该节点被删除。如图所示：

![](img/25e0e40b08b8016a58f1aab13ac2e81_441_0.png)

# 实现示例

在创建链表之前，我们将实现两种特殊列表：栈和队列。注意，实现这些数据结构的方法，我尝试用简单易懂的方式来实现。在以下示例中，每个节点都是 `Node` 类型。如果你需要开发类似的结构，大部分代码可以复用：

正如我们所说，STL 提供了许多实现数据结构的类。例如，`stack` 类实现了 LIFO（后进先出）栈。我们将在第26 章简要介绍。在这里，我们将尝试实现这些类的一些功能，以便你获得更多管理内存的经验。

# 实现栈

在本节中，我们将创建一个 LIFO 栈，正如名称所示，最后插入的节点第一个被提取。它是链表的一种特殊情况，具有以下限制：

a. 新节点只能插入到栈的头部并成为其新的头节点。
b. 只能删除头节点。

这种栈类似于一堆脏盘子。每个新盘子都放在栈顶，它是我们第一个清洗的盘子。

# 练习题

C.14.8 定义结构类型 `Node`，成员为 `code`、`name`、`grade` 以及一个指向 `Node` 结构的指针。创建一个节点类型类型的栈。编写一个程序，显示菜单以执行以下操作：

- 1. 插入学生。程序应读取学生数据并将其存储在节点中，该节点成为栈的头部。
- 2. 显示存储的数据。
- 3. 显示最后插入的学生的数据。
- 4. 删除最后插入的学生。
- 5. 显示存储的学生总数。
- 6. 程序终止。
