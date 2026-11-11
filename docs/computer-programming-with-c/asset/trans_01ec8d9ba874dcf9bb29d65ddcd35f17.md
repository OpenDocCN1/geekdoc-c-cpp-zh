
```cpp
/*pointer p and q point to dynamically allocated objects of
        Employee*/
p= new Employee;
q= new Employee;
/*Input the members of the Employee object pointed by the pointer
        p*/
cout<<"Enter the value of id , name and salary for object pointed by p"<<endl;
p->input();
/*Input the members of the Employee object pointed by the pointer
        q*/
cout<<"Enter the value of id , name and salary for object pointed by q"<<endl;
q->input();
/*Print the members of the Employee object pointed by the pointers
        p and q*/
cout<<"Employee Details are:"<<endl;
p->output();
q->output();
}
```

## **输出**

```
Enter the value of id, name and salary for object pointed by p
10 John 5000
Enter the value of id, name and salary for object pointed by q
20 Jack 3000
Employee Details are:
10   John   5000
20   Jack   3000
```

## 11.21  用于维护员工数据的链表

我们在第 10 章中利用结构体对象的动态内存分配，实现了一个可以存储整数数据的链表。我们也在第 10 章中说明了链表相较于数组的优势。既然现在已经理解了类对象的动态内存分配，我们将升级第 11.12 节中通过创建 Employee 对象数组来存储员工数据的代码，改为创建一个能够存储员工数据的链表，而不是创建对象数组。通过创建链表来存储员工数据的完整源代码中，类 Node 提供了以下函数：

```
void insert(Employee x)
```

该函数用于将 Employee 对象 x 插入链表。

```
void traverse()
```

该函数用于通过遍历链表，打印链表中所有员工的数据。

```
void remove(int id)
```

该函数用于从链表中删除 id 与传给该函数的整数参数相匹配的 Employee 节点。

这些函数的实现逻辑与第 10 章所述类似，唯一区别在于链表中的数据类型是 Employee，而不是 int。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_616_0.png)

## 存储整数值的列表——第 10 章实现

![](img/57c0d966bb33c67a5a188e6bf39e4e02_616_1.png)

## 存储 Employee 数据的链表

![](img/57c0d966bb33c67a5a188e6bf39e4e02_616_2.png)

**图 11.43：** 整数链表与 Employee 对象链表的比较

回顾第 10 章，结构体 Node 有两个成员 data 和 next，如图 11.43 所示。成员 data 的数据类型是整数，因为第 10 章实现的链表需要存储整数。在本节中，我们创建了一个包含两个成员 data 和 next 的类 Node。这一次，data 的数据类型是 Employee，因为我们打算在链表中存储 Employee 对象，而不仅仅是整数，如图 11.43 所示。

由于 Employee 是用户定义类型，我们创建了一个类 Employee，其中包含私有成员 id、name 和 salary，以及公有成员函数 input()、output() 和 getId()。函数 input() 用于从用户处读取成员 id、name 和 salary 的值作为输入，而函数 output() 用于在计算机屏幕上打印所有成员的值。函数 getId() 仅将成员 id 的值返回给调用者，我们很快会讨论该函数的意义。

正如从第 10 章给出的实现中所了解的，创建链表需要创建一个可在整个代码中访问的全局指针 head。为保持一致，我们将在给定程序中使用以下语句创建类似的全局指针 head：

```
Node *head;
```

然而，类 Node 是在程序中稍后定义的（在 head 指针的声明语句之后），因此我们必须使用以下语句对类 Node 进行原型声明：

```
class Node;
```

该语句使编译器知道名为 Node 的类将在程序中稍后定义，从而允许在定义类 Node 之前声明 Node 类型的指针 head。你可能会认为，避免对类 Node 进行原型声明的一种选择，是在创建 Node 类型指针 head 之前移动类 Node 的完整定义。这会引发其他问题，因为类 Node 中有 insert()、traverse() 和 remove() 等函数会使用指针 head。因此，指针 head 必须在类 Node 定义之前声明，因为 C++ 不支持变量的前向引用。这意味着程序中使用的每个变量都必须在使用之前声明。这解释了为什么程序中在定义类 Node 之前声明了指针 head，但复杂之处在于指针 head 也是 Node 类型。因此，编译器必须知道 Node 是程序中稍后定义的类，才能允许声明指针 head。因此，在这个程序中对类 Node 进行原型声明绝对必要。如果你查看类 Node，它有一个成员 data，其类型为 Employee。因此，我们在类 Node 之前定义了类 Employee，以避免对类 Employee 进行原型声明。因此，我们编写程序的顺序如下：

- 1. **步骤 1：** 包含头文件 `iostream.h`
- 2. **步骤 2：** 对类 Node 进行原型声明
- 3. **步骤 3：** 声明一个 Node 类型的指针 head
- 4. **步骤 4：** 定义类 Employee
- 5. **步骤 5：** 定义类 Node
- 6. **步骤 6：** 定义运行程序的 `main()` 函数

现在我们已经理解了程序的布局，接下来将重点说明：与第 10 章中定义的用于存储整数值的链表相比，在存储 Employee 对象的链表实现中有某些不同之处。

```
void insert(Employee x)
```

这是类 Node 的成员函数，用于将数据插入链表。注意，该函数的参数类型为 Employee，因为它需要将对象 x 作为其插入链表中的节点的数据。insert 函数的其余实现与第 10 章给出的内容完全相同。如果要插入的节点是第一个节点，则 if 块中的以下语句

```
head->data=x;
```

会将对象 x 的所有成员复制到 head 所指向的 Node 中包含的对象 data 中。这是可行的，因为我们知道，当 C++ 的赋值运算符用于对象时，它会把赋值运算符右侧对象的成员值复制到左侧对象。换句话说，对象 data 将成为对象 x 的精确副本，因此这等同于将对象 x 存储为 head 所指向的数据节点。同样，如果要插入的节点不是第一个节点，则 else 块中突出显示的语句会将临时节点 d 的数据正确设置为 x 的成员

```
Node *d = new Node;
d->data=x;
d->next=NULL;
```

因此，当节点 d 链接到链表时，员工 x 的数据就会被插入链表中。

```
void traverse()
```

该函数用于通过遍历链表，打印链表中所有 Employee 对象的数据。该函数的实现与第 10 章中的实现类似，区别在于，当我们打印每个节点中的数据时，我们使用以下语句

```
temp->data.output();
```

这是因为 temp 是一个遍历链表每个节点的指针。节点的数据实际上是类 Employee 的对象，而不是基本类型。因此，无论链表指针 temp 指向哪个节点，temp->data 始终是一个 Employee 对象。因此，你可以使用 temp->data 调用类 Employee 的任何公有成员函数。所以，我们调用 output() 成员函数来打印对象 temp->data 的成员 id、name 和 salary，如图 11.44 所示。由于指针 temp 会遍历链表中的所有对象，函数 traverse() 将打印所有对象的成员 id、name 和 salary。

