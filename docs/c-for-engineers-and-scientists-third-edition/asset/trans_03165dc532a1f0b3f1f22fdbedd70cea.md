

```cpp
const int MAXRECS = 3; // 最大记录数
```

```cpp
struct TeleType {
  char name;
  char phoneNo;
  TeleType *nextaddr;
};
```

```cpp
void populate(TeleType *); // main() 需要的函数原型
void display(TeleType *); // main() 需要的函数原型
```

```cpp
int main() {
  int i;
  TeleType *list, *current; // 指向 TeleType 类型  // 体的两个指针

  // 获取列表中第一个结构体的指针
  list = new TeleType;
  current = list;

  // 填充当前结构并创建剩余的  // 结构
  for(i = 0; i < MAXRECS - 1; i++) {
    populate(current);
    current->nextaddr = new TeleType;
    current = current->nextaddr;
  }

  populate(current); // 填充最后一个结构
  current->nextaddr = NULL; // 将最后一个地址设为 NULL 地址
  cout << "\n列表包含以下记录：\n";
  display(list); // 显示结构体

  return 0;
}
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_758_0.png)

```cpp
// 输入名字和电话号码
void populate(TeleType *record) // record 是指向 // 结构体的指针
{
    // TeleType 结构体

    cout << "输入名字：*";
    getline(cin,record->name);
    cout << "输入电话号码：*";
    getline(cin,record->phoneNumber);

    return;
}

void display(TeleType *contents) // contents 是指向 // 结构体的指针
{
    // TeleType 类型的结构体
    while (contents != NULL) // 显示到链表结束
    {
        cout << endl << setflags(ios::left)
        << setw(30) << contents->name
        << setw(20) << contents->phoneNo;
        contents = contents->nextaddr;
    }
    cout << endl;
}
```

在程序 13.11 中，第一次调用 `new` 时，它用于创建链表中的第一个结构体。因此，返回的地址存储在指针变量 `list` 中。`list` 中的地址被赋值给该指针变量。该指针变量用于指向当前结构体。由于当前结构体是创建的第一个，因此指针列表中的地址被赋值给当前指针。

在 `main()` 的 `for` 循环中，通过调用 `populate()` 并将当前结构体的地址传递给函数，填充新结构中的名字和电话号码成员。在返回时，当前结构体的指针成员被赋值为列表中下一个结构体的地址，该地址通过 `new` 获取。对 `new` 的调用创建了下一个结构并将其地址返回给当前结构体的指针成员。这次调用完成了当前成员的填充。`for` 循环的最后一条语句将当前指针中的地址重置为列表中下一个结构体的地址。

在创建最后一个结构体后，`main()` 中的最后语句填充该结构体，为指针成员分配一个 NULL 地址，并调用 `display()` 显示列表中的所有结构体。以下是程序 13.11 的运行示例：

输入名字：Acme, Sam
输入电话号码：(555) 898-2392
输入名字：Dolan, Edith
输入电话号码：(555) 682-2392

输入名字：Lanfrank, John
输入电话号码：(555) 718-4581
列表包含以下记录：
Acme, Sam (555) 898-2392
Dolan, Edith (555) 682-3104
Lanfrank, John (555) 718-4581

正如我们在运行时动态创建存储空间一样，`delete` 运算符在运行时将一个存储块还原给计算机。`delete` 唯一需要的参数是动态分配的存储块的起始地址。因此，返回的任何地址都可以顺序传递给 `delete`，将预留的内存恢复给计算机。`delete` 运算符不会更改传递给它的地址；它只是移除该地址引用的存储空间。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_760_0.png)

# 练习题 13.5

- 1. （修改）如表 13.1 所示，`new` 运算符返回分配的第一个新存储区域的地址，如果没有可用存储空间则返回 NULL。修改程序 13.11，在调用 `populate()` 之前检查是否返回了有效地址。如果可用存储不足，则显示适当的消息。
- 2. （程序）编写一个 C++ 函数 `remove()`，用于从程序 13 创建的结构体链表中移除现有的结构体。移除链式结构的算法应遵循第 13.4 节练习 4 中开发的移除结构体的序列。传递给 `remove()` 的参数应该是要被移除记录的前一个记录的结构体地址。在 `remove()` 函数中，确保被移除结构体中的指针值在移除之前替换为其前一个结构体的指针值。
- 3. （程序）编写一个新函数 `insert()`，用于向程序 13.11 创建的结构体链表中插入结构体。向链表插入的算法应遵循图 13.7 之前所示的插入记录的序列。传递给 `insert()` 的参数应该是要插入结构体的前一个结构体地址。插入的结构体应显示此当前结构体。`insert()` 函数应该动态创建一个新结构体，调用 `populate()` 并正确调整所有值。
- 5. （程序）编写一个 C++ 函数 `modify()`，用于修改程序 13.11 中创建的类型结构体的名字和电话号码成员。传递给 `modify()` 的参数应该是要修改结构体的地址。`modify()` 函数应先显示所选结构中的名字和电话号码，然后请求这些成员的数据。
- 6. （程序）a. 编写一个 C++ 程序，为用户提供选择菜单。菜单应包含以下选择：
  根据用户的选择，程序应执行相应的函数以满足请求。
  b. 为什么创建链表通常只由一个程序完成？

# 13.6 联合体 (Unions)

联合体是一种允许你在同一内存位置存储不同类型数据的数据类型。联合体的大小是其最大成员的大小。同一时间只能使用一个成员。定义联合体的语法与结构体相似，但使用 `union` 关键字代替 `struct`。

```cpp
union {
  char key;
  int num;
  double volts;
};
```

当你定义联合体时，编译器会分配足够的内存来容纳最大的成员。然而，所有成员共享相同的内存地址。当你给一个成员赋值时，它将覆盖任何其他成员的值。当你有一个变量可以持有几种类型中的一种，但在任何给定时间只有一种类型时这非常有用。

例如，以下声明

```cpp
union DateTime {
    int days;
    double time;
};
```

提供了一个不预留任何存储位置的联合体数据类型。这种数据类型可以定义任意数量的变量。例如，定义

DateTime first, second, *pt;

创建了一个名为 `first` 的联合体、一个名为 `second` 的联合体以及一个可以存储任何具有 DateTime 的联合体地址的指针。在声明联合体指针后，可以使用访问结构体成员相同的符号来访问联合体成员。例如，如果进行了赋值 `pt = &first;`，则 `pt->days` 指向联合体 `first` 的数据成员。

联合体可以是结构体或数组的成员，而结构体、数组和指针也可以联合体的成员。在每种情况下，用于访问成员的符号必须与所使用的嵌套保持一致。例如，在定义的结构体

```cpp
struct {
    char uType;
    union {
        char *text;
        float rate;
    } uTax;
    int flag;
} flag;
```

中变量 `rate` 的引用方式为

```cpp
flag.uTax.rate
```

同样，字符串地址的第一个字符存储在指针 `text` 中，引用方式如下：

```cpp
*flag.uTax.text
```

# 第13 章结构体

通常使用第二个变量来跟踪联合体中存储的当前类型。例如，可以使用以下代码选择合适的成员进行显示。`uType` 变量的值决定了当前存储的类型：

```cpp
switch (uType) {
    case 'c': cout << val.key;
        break;
    case 'i': cout << val.num;
        break;
    case 'd': cout << val.volts;
        break;
    default: cout << "uType 中的无效类型: " << uType;
}
```

