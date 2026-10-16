

## 5.11 静态数据成员

类的一个数据成员可以被限定为 static。静态成员变量的特性与 C 静态变量相似。静态成员变量具有某些特殊特性。这些特性如下：

- 它在该类的第一个对象创建时初始化为零。不允许其他初始化。
- 对于整个类只创建一个该成员的副本，并且无论创建了多少个对象，该副本都被该类的所有对象共享。
- 它仅在类内部可见，但其生命周期贯穿整个程序。

静态变量通常用于维护整个类共有的值。例如，静态数据成员可以用作计数器，记录所有对象的出现次数。程序 5.4 说明了静态数据成员的使用。

### 静态类成员

```
#include <iostream>

using namespace std;

class item
{
    static int count;
    int number;
public:
    void getdata(int a)
    {
        number = a;
        count ++;
    }
    void getcount(void)
    {
        cout << "count: ";
        cout << count << "\n";
    }
};

int item :: count;

int main()
{
item a, b, c;        // count is initialized to zero
a.getcount();        // display count
b.getcount();
c.getcount();

a.getdata(100);      // getting data into object a
b.getdata(200);      // getting data into object b
c.getdata(300);      // getting data into object c

cout << "After reading data" << "\n";

a.getcount();        // display count
b.getcount();
c.getcount();
return 0;
}
```

PROGRAM 5.4

程序 5.4 的输出为：

```
count: 0
count: 0
count: 0
After reading data
count: 3
count: 3
count: 3
```

### note

注意程序中的以下语句：

```
int item :: count;      // definition of static data member
```

请注意，每个静态成员变量的类型和作用域必须在类定义之外进行定义。这是因为静态数据成员是单独存储的，而不是作为对象的一部分。由于它们与类本身相关联而不是与任何类对象相关联，因此它们也被称为类变量。

静态变量 count 在对象创建时初始化为零。每当数据读入一个对象时，count 就会递增。由于数据被读入了三个对象三次，因此变量 count 被递增了三次。因为 count 只有一个副本被所有三个对象共享，所以所有三个输出语句都会显示值 3。图 5.4 显示了对象如何使用静态变量。

![](img/58ab8f034e2127e80560390a921c2523_130_0.png)

### Fig. 5.4 ↔ Sharing of a static data member

静态变量类似于非内联成员函数，因为它们在类声明中声明并在源文件中定义。在定义静态变量时，也可以为变量分配一些初始值。例如，以下定义将 count 的初始值设为 10。

```
int item :: count = 10;
```

## 5.12 静态成员函数

与静态成员变量类似，我们也可以拥有静态成员函数。声明为 static 的成员函数具有以下特性：

- 静态函数只能访问在同一类中声明的其他静态成员（函数或变量）。
- 静态成员函数可以使用类名（而不是其对象）按如下方式调用：

```
class-name :: function-name;
```

程序 5.5 说明了这些特性的实现。静态函数 showcount() 显示到目前为止创建的对象数量。对象数量的计数由静态变量 count 维护。

函数 showcode() 显示每个对象的代码号。

### 静态成员函数

```cpp
#include <iostream>

using namespace std;

class test
{
        int code;
        static int count;        // static member variable
public:
        void setcode(void)
        {
                code = ++count;
        }
        void showcode(void)
        {
                cout << "Object number: " << code << "\n";
        }
        static void showcount(void)        // static member function
        {
                cout << "Count: " << count << "\n";
        }
};

int test::count;
int main()
{
        test t1, t2;

        t1.setcode();
        t2.setcode();

        test::showcount();       // accessing static function

        test t3;
        t3.setcode();

        test::showcount();

        t1.showcode();
        t2.showcode();
        t3.showcode();

        return 0;
}
```

### Output of Program 5.5:

```
count: 2
count: 3
object number: 1
object number: 2
object number: 3
```

### note

请注意语句

```
code = ++count;
```

在每次调用 setcode( ) 函数时执行，并将 count 的当前值赋给 code。由于每个对象都有自己的一份 code 副本，因此 code 中包含的值代表其对象的唯一编号。

记住，以下函数定义将不起作用：

```
static void showcount()
{
    cout << code;    // code is not static
}
```

## 5.13 对象数组

我们知道数组可以是任何数据类型，包括 struct。同样，我们也可以拥有变量数组，其类型为类。这样的变量称为对象数组。考虑以下类定义：

```
class employee
{
    char name[30];
    float age;
public:
    void getdata(void);
    void putdata(void);
};
```

标识符 employee 是一个用户定义的数据类型，可用于创建与不同类别员工相关的对象。示例：

```
employee manager[3];        // array of manager
employee foreman[15];       // array of foreman
employee worker[75];        // array of worker
```

数组 **manager** 包含三个对象（经理），即 **manager[0]**、**manager[1]** 和 **manager[2]**，类型为 **employee** 类。同样，**foreman** 数组包含 15 个对象（工头），而 **worker** 数组包含 75 个对象（工人）。

由于对象数组的行为与任何其他数组一样，我们可以使用通常的数组访问方法来访问各个元素，然后使用点成员运算符来访问成员函数。例如，语句

```
manager[i].putdata();
```

将显示数组 **manager** 的第 i 个元素的数据。也就是说，该语句要求对象 **manager[i]** 调用成员函数 **putdata()**。

对象数组在内存中以与多维数组相同的方式存储。数组 manager 在图 5.5 中表示。请注意，只为对象的數據项创建了空间。成员函数是单独存储的，将被所有对象使用。

![](img/58ab8f034e2127e80560390a921c2523_133_0.png)

Fig. 5.5 ⇔ Storage of data items of an object array

程序 5.6 说明了对象数组的使用。

### 对象数组

```
#include <iostream>

using namespace std;

class employee
{
    char name[30];      // string as class member
    float age;
    public:
        void getdata(void);
        void putdata(void);
};
void employee :: getdata(void)
{
    cout << "Enter name: ";
    cin >> name;
    cout << "Enter age:  ";
    cin >> age;
}
void employee :: putdata(void)
{
    cout << "Name:  " << name << "\n";
    cout << "Age:   " << age  << "\n";
}
const int size=3;
int main()
{
    employee manager[size];
    for(int i=0; i<size; i++)
    {
        cout << "\nDetails of manager" << i+1 << "\n";
        manager[i].getdata();
    }
    cout << "\n";
    for(i=0; i<size; i++)
    {
        cout << "\nManager" << i+1 << "\n";
        manager[i].putdata();
    }
    return 0;
}
```

PROGRAM 5.6

这是一个交互式程序，输入数据和程序输出如下所示：

### Interactive input

Details of manager1
Enter name: xxx
Enter age: 45

