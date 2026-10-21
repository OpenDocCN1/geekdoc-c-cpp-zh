
```
        n2 = y;
    }
    PAR sum()
    {
        return(n1 + n2);
    }
};
```

**输出：**

```
Sum = 30
Sum = 6.9
```

**说明：** 类模板与函数模板类似，区别在于它用于类。这里编写了一个模板类`demo`，使用了泛型数据类型`PAR`。注意，模板声明与函数模板的写法相同。该类模板有两个数据成员`n1`和`n2`、一个构造函数以及一个`sum`函数，该函数计算两个数据成员之和并返回。

在main函数中，请注意我们是如何实例化类模板的。语句`demo<int>d1(10,20);`为`int`数据类型实例化了一个新的`demo`类。在类模板中，所有出现`PAR`的地方都被替换为`int`。首先写类名，然后在尖括号`<`和`>`中写入数据类型；`d1(10,20)`通过调用`demo`类的双参数构造函数创建对象`d1`。然后我们通过调用`sum`函数求两个数据成员的和。

该类在内存中将如下所示：

```
class demo
{
        int n1, n2;
    public:
                demo(int x, int y)
                {
                        n1 = x;
                        n2 = y;
                }
```

```
floatData
2.4      4.5
charData
P  T
char *Data
One      Two
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_647_0.png)

**图13.10.** 程序13.13的输出屏幕

**说明：** 这里，我们有一个类模板，类似于前面程序中创建的`demo`类模板，区别在于这个类只是接收并显示数据成员。在main函数中，当`demo<int>d1(10,20);`执行时，将为`int`数据类型创建一个新的`demo`类，所有出现`PAR`的地方都会被替换为`int`。`demo`类的构造函数将被调用，`n1`的值为10，`n2`的值为20。在构造函数中，我们调用了`show`函数，它显示`n1`和`n2`的数据类型及其值。其他语句也遵循同样的逻辑：

```
demo<float> d2(2.4f,4.5f);
demo<char> d3('P','T');
demo<char*> d4("One","Two");
```

## 程序13.14 使用类模板（版本2）显示不同类型的数据

```cpp
#include <iostream.h>
#include <typeinfo.h>
template <class T1,class T2>
class demo
{
    T1 n1;
    T2 n2;
public :
    demo(T1 x, T2 y)
    {
        n1 = x;
        n2 = y;
        show();
    }
    void show()
    {
        cout << n1 << " is of type" << typeid(T1).name() << endl;
        cout << n2 << " is of type" << typeid(T2).name() << endl;
    }
};

void main()
{
    demo<int,float> d1(10,20.54f);
    demo<float,char> d2(2.4f,'H');
    demo<char,char*> d3('M',"NMIMS");
    demo<char*,int> d4("MPSTME",24);
}
```

**输出：**

```
10 is of type int
20.54 is of type float
2.4 is of type float
H is of type char
M is of type char
NMIMS is of type char*
MPSTME is of type char*
24 is of type int
```

**说明：** 我们可以在类模板中拥有两种不同的泛型数据类型，类似于函数模板写为`template<class T1, class T2>`。在main函数中，当这4条语句全部执行时，会为4对不同参数创建4个不同的类。例如，当`demo<int,float>d1(10,20.54f);`执行时，将按照类模板`demo`的定义创建一个新的`demo`类，所有出现`T1`的位置都会被替换为`int`，所有出现`T2`的位置都会被替换为`float`。该类将如下所示：

```
class demo
{
    int n1;
    float n2;
public :
    demo(int x,float y)
    {
        n1 = x;
        n2 = y;
        show();
    }
    void show()
    {
        cout << n1 << " is of type " << typeid(int).name() << endl;
        cout << n2 << " is of type " << typeid(float).name() << endl;
    }
};
```

## 程序13.15 用于求数组元素之和的类模板

```cpp
#include <iostream.h>
#include <typeinfo.h>
#define S 5
template <class TARR>
class demo
{
    TARR arr[S];
public:
    demo()
    {
        int i;
        cout << "Enter " << S << " " << typeid(TARR).name() << " numbers\n";
        for(i=0;i<S;i++)
            cin >> arr[i];
    }
    TARR sum()
    {
        int i;
        TARR s=0;
        for(i=0;i<S;i++)
            s += arr[i];
        return s;
    }
};

void main()
{
    demo<int> d1;
    cout << "Sum = " << d1.sum() << endl;
    demo<float> d2;
    cout << "Sum = " << d2.sum() << endl;
    demo<long> d3;
    cout << "Sum = " << d3.sum() << endl;
}
```

**输出：**

```
Enter 5 int numbers
2 45 67 34 23
Sum = 169
Enter 5 float numbers
1.2 3.4 3.3 4.5 5.6
Sum = 18
Enter 5 long numbers
12345
234567
76543
34567
127865
Sum = 485815
```

**说明：** 这个类模板用于声明和定义不同类型的数组，并求其元素之和。当`demo<float>d2;`执行时，会实例化一个新版本的`demo`类模板，并提示用户输入5个元素。数字存储在数组中，然后通过使用对象`d2`调用`sum`函数显示总和。该类将如下所示：

```
class demo
{
    float arr[S];
public:
    demo()
    {
        int i;
        cout << "Enter " << S << " " << typeid(float).name()
             << " numbers\n";
        for(i=0;i<S;i++)
            cin >> arr[i];
    }
    float sum()
    {
        int i;
        float s=0;
        for(i=0;i<S;i++)
            s += arr[i];
        return s;
    }
};
```

## 程序13.16 类模板演示：成员函数在类外定义

```cpp
#include <iostream.h>
#include <conio.h>
template <class T>
class demo
{
    T num1,num2;
public:
    void input(T x, T y);
    void show()
    {
        cout << "num1 = " << num1 << "\t";
        cout << "num2 = " << num2 << "\t";
    }
};

template <class T>
void demo<T>::input(T x, T y)
{
    num1 = x;
    num2 = y;
}

void main()
{
    demo<int> d;
    clrscr();
    d.input(10,20);
    d.show();
    getch();
}
```

**输出：**

```
num1 = 10	num2 = 20
```

**说明：** 本程序的目的是演示如何在类外部定义类模板的函数。对于类模板中声明的每个函数，其定义的第一行必须如下：

```cpp
template<class T>
void demo<T>::input(T x, T y)
{
    num1 = x;
    num2 = y;
}
```

## 程序13.17 不使用模板的简单链表

```cpp
#include <iostream.h>
#include <typeinfo.h>
class Linklist
{
    struct node
    {
        int data;
        struct node*next;
    }*start,*save,*temp;
public:
    Linklist()
    {
        start = NULL;
    }
    void add(int d)
    {
        if(start == NULL)
        {
            start = new node;
            start->data = d;
            start->next = NULL;
        }
        else
        {
            temp = new node;
            temp->data = d;
            temp->next = NULL;
            save = start;
            while(save->next != NULL)
                save = save->next;
            save->next = temp;
        }
    }
    void show()
    {
        while(start != NULL)
        {
            cout << start->data << "->";
            start = start->next;
        }
    }
};

void main()
{
    Linklist L;
    L.add(10);
    L.add(20);
    L.add(30);
    L.add(40);
}
```

**输出：**

```
10->20->30->40
```

**说明：** 我们使用结构`node`为链表创建节点，该结构有一个`int`类型的数据成员，以及一个指向下一个节点的`struct node`类型指针，名为`next`。在结构`node`声明之后，我们又创建了三个指针`start`、`temp`和`save`。`start`指针用于跟踪链表的起始节点，`temp`和`save`用于临时目的。函数`add`向链表添加一个新节点。它检查`start`是否为NULL；如果是，则创建链表的第一个节点，并让`start`指向它。如果`start`不为NULL，则使用while循环和`save`指针移动到最后一个节点，并在那里添加一个新节点。注意，新节点是在前面创建的，并由`temp`指针指向。为了显示链表，我们有`show`函数，它显示每个节点的数据。

## 程序13.18 基于模板的链表

```cpp
#include <iostream.h>
#include <typeinfo.h>
template <class T>

class Linklist
{
    struct node
    {
        T data;
        struct node* next;
    }*start,*save,*temp;
public:
    Linklist()
    {
        start = NULL;
    }
    void add(T d)
    {
        if(start == NULL)
        {
            start = new node;
            start->data = d;
            start->next = NULL;
        }
        else
        {
            temp = new node;
            temp->data = d;
            temp->next = NULL;
            save = start;
            while(save->next != NULL)
                save = save->next;
            save->next = temp;
        }
    }
};
```
