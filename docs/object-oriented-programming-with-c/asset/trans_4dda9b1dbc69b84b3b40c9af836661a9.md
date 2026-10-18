
由此产生的后果是，处理这类任务的函数应具有受限的访问权限。我们可以将这些函数放在私有区。

私有成员函数只能被其所属类的另一个成员函数调用。即使是对象也不能使用点运算符调用私有函数。考虑如下定义的类：

```cpp
class sample
{
    int m;
    void read(void);  // 私有成员函数
public:
    void update(void);
    void write(void);
};
```

如果 **s1** 是 **sample** 的一个对象，那么

```cpp
s1.read();  // 不可行；对象不能访问
            // 私有成员
```

是非法的。但是，函数 **read()** 可以被函数 **update()** 调用来更新 **m** 的值。

```cpp
void sample :: update(void)
{
    read();  // 简单调用；未使用对象
}
```

## 5.9 类中的数组

数组可以作为成员变量在类中使用。以下类定义是有效的。

```cpp
const int size = 10; // 为数组大小提供值
class array
{
    int a[size];    // 'a' 是 int 类型的数组
public:
    void setval(void);
    void display(void);
};
```

数组变量 **a[ ]** 被声明为类 **array** 的私有成员，它可以像任何其他数组变量一样在成员函数中使用。我们可以对其执行任何操作。例如，在上述类定义中，成员函数 **setval()** 设置数组 **a[ ]** 的元素值，**display()** 函数显示这些值。类似地，我们可以使用其他成员函数对数组值执行任何其他操作。

让我们考虑一个购物清单，我们每月向经销商下订单。清单包括每件商品的代码和价格等详细信息。我们希望执行诸如向清单添加商品、从清单删除商品以及打印订单总价值等操作。程序 5.3 展示了如何使用以数组作为数据成员的类来实现这些操作。

### 程序 5.3 处理购物清单

```cpp
#include <iostream.h>
using namespace std;
const int m = 50;

class ITEMS
{
    int itemCode[m];
    float itemPrice[m];
    int count;
public:
    void CNT(void) {count = 0;}  // 将 count 初始化为 0
    void getitem(void);
    void displaySum(void);
    void remove(void);
    void displayItems(void);
};
// ==============================================
void ITEMS :: getitem(void)  // 为 item 的
                             // 数据成员赋值
{
    cout << "Enter item code :";
    cin >> itemCode[count];
    cout << "Enter item cost :";
    cin >> itemPrice[count];
    count++;
}
void ITEMS :: displaySum(void)  // 显示所有
                                 // 商品的总值
{
    float sum = 0;
    for(int i = 0; i < count; i++)
        sum = sum + itemPrice[i];
    cout << "\nTotal value :" << sum << "\n";
}
void ITEMS :: remove(void)  // 删除指定商品
{
    int a;
    cout << "Enter item code :";
    cin >> a;
    for(int i = 0; i < count; i++)
        if(itemCode[i] == a)
            itemPrice[i] = 0;
}
void ITEMS :: displayItems(void)  // 显示商品
{
    cout << "\nCode Price\n";
    for(int i = 0; i < count; i++)
    {
        cout << "\n" << itemCode[i];
        cout << " " << itemPrice[i];
    }
    cout << "\n";
}
// ================================
int main()
{
    ITEMS order;
    order.CNT();
    int x;
    do  // do...while 循环
    {
        cout << "\nYou can do the following;";
        cout << " Enter appropriate number \n";
        cout << "\n1 : Add an item ";
        cout << "\n2 : Display total value";
        cout << "\n3 : Delete an item";
        cout << "\n4 : Display all items";
        cout << "\n5 : Quit";
        cout << "\n\nWhat is your option?";
        cin >> x;
        switch(x)
        {
            case 1 : order.getitem(); break;
            case 2 : order.displaySum(); break;
            case 3 : order.remove(); break;
            case 4 : order.displayItems(); break;
            case 5 : break;
            default : cout << "Error in input; try again\n";
        }
    } while(x != 5);  // do...while 结束
```

```text
Enter item cost :300

You can do the following; Enter appropriate number

1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option? 2

Total value :600

You can do the following; Enter appropriate number

1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option? 3

Enter item code :222

You can do the following; Enter appropriate number

1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option? 4
```

| 代码 | 价格 |
|------|-------|
| 111  | 100   |
| 222  | 0     |
| 333  | 300   |

```text
You can do the following; Enter appropriate number

1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option? 5
```

**注意：** 该程序使用了两个数组，即 **itemCode[]** 用于存放商品的代码号，**itemPrice[]** 用于存放价格。第三个数据成员 count 用于记录清单中的商品数量。程序共使用四个函数来实现要对清单执行的操作。语句 `const int m = 50;` 定义了数组成员的大小。

第一个函数 **CNT()** 简单地将变量 **count** 设置为零。第二个函数 **getitem()** 以交互方式获取商品代码和商品价格，并将它们赋给数组成员 **itemCode[count]** 和 **itemPrice[count]**。注意，在此函数内部，赋值操作完成后 **count** 会递增。函数 **displaySum()** 首先计算订单的总值，然后打印该值。第四个函数 **remove()** 从清单中删除指定商品。它使用商品代码在清单中定位该商品，并将价格设置为零，表示该商品在清单中不再“有效”。最后，函数 **displayItems()** 显示清单中的所有商品。

该程序使用基于菜单的用户界面来实现所有任务。

## 5.10 对象的内存分配

我们曾指出，对象的内存空间是在声明它们时分配的，而不是在指定类时分配的。这一说法只部分正确。实际上，成员函数在作为类规范的一部分被定义时，只创建并放入内存空间一次。由于属于该类的所有对象使用相同的成员函数，因此在创建对象时不会为成员函数分配单独的空间。只有成员变量的空间是为每个对象单独分配的。对象必须具有独立的内存位置，因为不同对象的成员变量将保存不同的数据值。如图 5.3 所示。

![](img/62b7c32e48e4f960a8dc2825a7119fb2_195_0.png)

图 5.3 *对象的内存*

## 5.11 静态数据成员

类的数据成员可以被限定为 static。**static** 成员变量的属性与 C 语言中的 static 变量类似。静态成员变量具有某些特殊特性，如下：

- 当创建其类的第一个对象时，它被初始化为零。不允许其他初始化。
- 无论创建多少个对象，只为整个类创建该成员的一个副本，并由该类的所有对象共享。
- 它仅在类内可见，但其生命周期是整个程序。

静态变量通常用于维护整个类共有的值。例如，静态数据成员可以用作记录所有对象出现次数的计数器。程序 5.4 演示了静态数据成员的用法。

### 程序 5.4 静态类成员

```cpp
#include <iostream.h>
using namespace std;

class item
{
    static int count;
    int number;
public:
    void getdata(int a)
    {
        number = a;
        count++;
    }
    void getcount(void)
    {
        cout << "count:";
        cout << count << '\n';
    }
};
```

