

```
inline void item :: getdata(int a, float b) // definition
{
    number = a;
    cost = b;
}
```

## 5.7 成员函数的嵌套

我们刚刚讨论过，类的成员函数只能由该类的对象使用点运算符调用。但是对此有一个例外。成员函数可以在同一类的另一个成员函数内部通过其名称调用。这称为成员函数的嵌套。程序 5.2 说明了这一特性。

### 成员函数的嵌套

```
#include <iostream>

using namespace std;

class set
{
    int m, n;
public:
    void input(void);
    void display(void);
    int largest(void);
};

int set :: largest(void)
{
    if(m >= n)
        return(m);
    else
        return(n);
}

void set :: input(void)
{
    cout << "Input values of m and n" << "\n";
    cin >> m >> n;
}

void set :: display(void)
{
cout << "Largest value = "
    << largest() << "\n";      // calling member function
}

int main()
{
    set A;
    A.input();
    A.display();

    return 0;
}
```

程序 5.2 的输出为：

```
Input values of m and n
25 18
Largest value = 25
```

## 5.8 私有成员函数

虽然通常的做法是将所有数据项放在私有部分，将所有函数放在公有部分，但在某些情况下可能需要将某些函数隐藏起来（就像私有数据一样），不允许外部调用。例如删除客户文件中的账户，或为员工提供增量，这些都是后果严重的事件，因此处理此类任务的函数应具有受限的访问权限。我们可以将这些函数放在私有部分。

私有成员函数只能由其所属类的另一个函数调用。即使对象也不能使用点运算符调用私有函数。考虑如下定义的类：

```
class sample
{
    int m;
    void read(void);      // private member function
public:
    void update(void);
    void write(void);
};
```

如果 s1 是 sample 的对象，则

```
s1.read();    // won't work; objects cannot access
             // private members
```

是非法的。但是，函数 read() 可以被函数 update() 调用以更新 m 的值。

```
void sample :: update(void)
{
    read();    // simple call; no object used
}
```

## 5.9 类中的数组

数组可以用作类的成员变量。下面的类定义是有效的。

```
const int size=10;    // provides value for array size

class array
{
    int a[size];    // 'a' is int type array
public:
    void setval(void);
    void display(void);
};
```

作为类 array 的私有成员声明的数组变量 a[ ] 可以在成员函数中使用，就像任何其他数组变量一样。我们可以对其执行任何操作。例如，在上面的类定义中，成员函数 setval() 设置数组 a[ ] 元素的数值，而 display() 函数显示这些数值。同样，我们可以使用其他成员函数对数组值执行任何其他操作。

让我们考虑一份每月向经销商订购的商品清单。该清单包括每件商品的编号和价格等详细信息。我们希望执行诸如向清单中添加商品、从清单中删除商品以及打印订单总价值等操作。程序 5.3 展示了如何使用具有数组作为数据成员的类来实现这些操作。

```
PROCESSING SHOPPING LIST

#include <iostream>

using namespace std;

const m=50;

class ITEMS
{
    int itemCode[m];
    float itemPrice[m];
    int count;
public:
    void CNT(void){count = 0;}        // initializes count to 0
    void getitem(void);
    void displaySum(void);
    void remove(void);
    void displayItems(void);
};
//==================================================
void ITEMS :: getitem(void)          // assign values to data
                                   // members of item
{
    cout << "Enter item code :";
    cin >> itemCode[count];

    cout << "Enter item cost :";
    cin >> itemPrice[count];
    count++;
}
void ITEMS :: displaySum(void)       // display total value of
                                   // all items
{
    float sum = 0;
    for(int i=0; i<count; i++)
        sum = sum + itemPrice[i];

    cout << "\nTotal value :" << sum << "\n";
}
void ITEMS :: remove(void)           // delete a specified item
{
    int a;
    cout << "Enter item code :";
    cin >> a;

    for(int i=0; i<count; i++)
        if(itemCode[i] == a)
            itemPrice[i] = 0;
}

void ITEMS :: displayItems(void)     // displaying items
{
cout << "\nCode  Price\n";

for(int i=0; i<count; i++)
{
    cout <<"\n" << itemCode[i];
    cout <<"   " << itemPrice[i];
}
cout << "\n";
}
//============================================

int main()
{
    ITEMS order;
    order.CNT();
    int x;
    do            // do....while loop
    {
        cout << "\nYou can do the following:"
             << "Enter appropriate number \n";
        cout << "\n1 : Add an item ";
        cout << "\n2 : Display total value";
        cout << "\n3 : Delete an item";
        cout << "\n4 : Display all items";
        cout << "\n5 : Quit";
        cout << "\n\nWhat is your option?";

        cin >> x;

        switch(x)
        {
            case 1 : order.getItem(); break;
            case 2 : order.displaySum(); break;
            case 3 : order.remove(); break;
            case 4 : order.displayItems(); break;
            case 5 : break;
            default : cout << "Error in input; try again\n";
        }
    } while(x != 5);            // do...while ends

    return 0;
}
```

程序 5.3 的输出为：

```
You can do the following; Enter appropriate number
1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option?1
Enter item code :111
Enter item cost :100

You can do the following; Enter appropriate number
1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option?1
Enter item code :222
Enter item cost :200

You can do the following; Enter appropriate number
1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option?1
Enter item code :333
Enter item cost :300

You can do the following; Enter appropriate number
1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option?2
Total value :600
```

You can do the following; Enter appropriate number
1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option?3
Enter item code :222

You can do the following; Enter appropriate number
1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option?4

| Code | Price |
|------|-------|
| 111  | 100   |
| 222  | 0     |
| 333  | 300   |

You can do the following; Enter appropriate number
1 : Add an item
2 : Display total value
3 : Delete an item
4 : Display all items
5 : Quit

What is your option?5

### note

该程序使用两个数组，即 itemCode[] 用于保存商品的编号，itemPrice[] 用于保存价格。第三个数据成员 count 用于记录清单中的商品数量。程序使用总共四个函数来实现对清单执行的操作。语句

```
const int m = 50;
```

定义了数组成员的大小。

第一个函数 CNT() 只是将变量 count 设置为零。第二个函数 getitem() 交互式地获取商品代码和商品价格，并将它们分配给数组成员 itemCode[count] 和 itemPrice[count]。请注意，在此函数内部，count 在赋值操作完成后递增。函数 **displaySum( )** 首先计算订单的总价值，然后打印该值。第四个函数 **remove( )** 从清单中删除给定商品。它使用商品代码在清单中定位该商品，并将价格设置为零，表示该商品在清单中不“活跃”。最后，函数 **displayItems( )** 显示清单中的所有商品。

该程序使用基于菜单的用户界面实现了所有任务。

## 5.10 对象的内存分配

我们已经指出，对象的内存空间在声明时分配，而不是在指定类时分配。这一说法只有部分正确。实际上，成员函数在作为类规范的一部分定义时创建并放置在内存空间中，仅创建一次。由于属于该类的所有对象都使用相同的成员函数，因此在创建对象时不会为成员函数分配单独的空间。只有为每个对象单独分配成员变量的空间。对象需要单独的内存位置，因为成员变量将为不同对象保存不同的数据值。这在图 5.3 中显示。

![](img/58ab8f034e2127e80560390a921c2523_127_0.png)

图 5.3 ⇨ 对象的内存

