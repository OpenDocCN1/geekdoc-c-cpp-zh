
# /*程序 4.16 为字符串分配内存*/

```
#include <iostream.h>
#include <conio.h>
void main()
{
    int n;
    clrscr();
    cout << "Enter the length of your name\n";
    cin >> n;
    char *str = new char[n + 1];
    cout << "Enter your name\n";
    cin >> str;
    cout << "Hello " << str << endl;
    delete str;
    getch();
}
```

# 输出：

输入你的名字的长度
8
输入你的名字
MADHURI
你好，MADHURI

说明：在程序 3.16 中，我们首先将用户输入的名字长度存入变量 n，这样就能确定需要动态分配多少内存。语句 `char *str = new char[n + 1];` 从堆中动态分配 n + 1 字节的内存（其中 1 字节用于空字符），并返回所分配内存首字节的地址，该地址被赋给 char 类型指针 str。然后从用户处读取字符串并显示。最后使用 delete 释放内存。

# /*程序 4.17 使用 new 和 delete 运算符为数组动态分配与释放内存*/

```
#include <iostream.h>
#include <conio.h>
#include <stdlib.h> //for exit ()
void main()
{
    int i,n;
    clrscr();
    cout << "How many elements you want in array\n";
    cin >> n;
    int* arr = new int[n];
    for(i = 0; i < n; i++)
    {
        cout << "\n Enter arr[" << i << "]" element :;
        cin >> arr[i];
    }
    int ele;
    cout << "Enter the element you want to search\n";
    cin >> ele;
    for(i = 0; i < n; i++)
    {
        if(arr[i] == ele)
        {
            cout << "Element found at" << "index " << i << endl;
            exit(0);
        }
    }
    delete arr;
    cout << "Element does not exist in array\n";
    getch( );
}
```

# 输出：

（第一次运行）
你想在数组中存放多少个元素？
10

输入 arr[0] 元素：10

输入 arr[1] 元素：20

输入 arr[2] 元素：30

输入 arr[3] 元素：40

输入 arr[4] 元素：40

输入 arr[5] 元素：50

循环检查数组中是否有任何元素与 ele 匹配。如果有，就显示该元素的位置。如果数组中不存在该元素，for 循环会正常结束，最后显示“数组中不存在该元素”。

```
/* PROG 4.18 DEMO OF ARRAY OF POINTERS AND NEW OPERATOR*/

#include <iostream.h>
#include <stdlib.h>

void main()
{
    int n,i;
    cout << "How many elements you want in array\n";
    cin >> n;
    int* arr = new int [n];
    int **ptr = new int*[n];
    for(i=0;i<n;i++)
    {
        cout << "\n Enter arr[" << i << "]element : ";
        cin >> arr[i];
        ptr[i] = &arr[i];
    }
    cout << "Element\t\t Address\n";
    for(i=0;i<n;i++)
    {
        cout << *ptr[i] << "\t\t" << ptr[i] << endl;
    }
    delete arr;
    delete [] ptr;
}
```

输出：
你想在数组中存放多少个元素？
5

输入 arr[0]元素：12

输入 arr[1]元素：13

输入 arr[2]元素：14

输入 arr[3]元素：15

输入 arr[4]元素：16

| 元素 | 地址 |
|---|---|
| 12 | 0x8fd20f00 |
| 13 | 0x8fd20f02 |
| 14 | 0x8fd20f04 |
| 15 | 0x8fd20f06 |
| 16 | 0x8fd20f08 |

说明：语句 `int*arr [] = new int [n];` 动态创建了一个大小为 n 的数组。为了存储数组元素的地址，可以通过 `int **ptr = new int *[n]` 创建一个指针数组。在 for 循环中，我们将数组 arr 各元素的地址赋给指针数组 ptr 的对应元素。现在，`ptr[0]` 与 `&ptr[0]` 相同；而 `arr[0]` 与 `*ptr[0]` 的值相同。借助 ptr 数组，我们可以显示数组 arr 的地址和元素。

```
/*PROG 4.19 DYNAMIC MEMORY ALLOCATION FOR 2-D ARRAY */

#include <iostream.h>
#include <conio.h>
void main()
{
    int **ptr;
    int i,j;
    int row,col;
    clrscr();
    cout<<"Enter the number of rows\n";
    cin>>row;
    cout<<"Enter the number of columns\n";
    cin>>col;
    ptr=new int *[row];
    for(i=0;i<row;i++)
        ptr[i]=new int [col];
    int *max= new int [row];
    for(i=0;i<row;i++)
        for(j=0;j<col;j++)
        {
            cout<<"\nEnter ptr["<<i<<"] element : ";
            cin>>(*(ptr+i)+j);
        }
    cout<<"\n\n Matrix is \n";
    for(i=0;i<row;i++)
    {
        for(j = 0; j < col; j++)
            cout << ptr[i][j] << " ";
        cout << endl;
    }
    for(i = 0; i < row; i++)
    {
        max[i] = ptr[i][0];
        for(j = 1; j < col; j++)
        {
            if(max[i] < ptr[i][j])
            max[i] = ptr[i][j];
        }
    }
    cout << "Max of each row is as follows\n ";
    for(i = 0; i < row; i++)
        cout << "Row" << i + 1 << "->" << max[i] << endl;
    delete [] ptr;
    delete max;
    getch();
}
```

# 输出：

输入行数
3
输入列数
3

输入 ptr[0] 元素：1

输入 ptr[0] 元素：2

输入 ptr[0] 元素：3
输入 ptr[1] 元素：4

输入 ptr[1] 元素：5

输入 ptr[1] 元素：6

输入 ptr[2] 元素：7

输入 ptr[2] 元素：8
输入 ptr[2] 元素：92

矩阵是
1 2 3
4 5 6
7 8 92

每一行的最大值如下
第1行->3
第2行->6
第3行->92

说明：要动态创建二维数组，需要使用双重指针。最初，指针 ptr 指向为 3 行分配的内存。语句 `ptr = new int *[row];` 创建了一个大小为 row 的指针数组。由于每一行都由一个有 3 个元素的一维数组组成，所以用 for 循环按行数（输出中为 3）为各列分配内存（此处为 3），代码如下：

for(i=0; i< row; i++)
ptr[i] = new int [col];

我们在这里有三行，因此 `ptr[0]` 指向第一个一维数组，`ptr[1]` 指向第二个一维数组，`ptr[2]` 指向第三个一维数组。现在，指针 ptr 可以看作一个二维数组（三个一维数组的组合）。要访问任意元素，可以写 `ptr[i][j]` 或 `*(*(ptr+i)+j)`。

为了找出每一行的最大值，我们创建了一个大小为 row 的动态数组 max。最初，每一行的第一个元素被视为最大值。然后对每一行运行 for 循环，找出该行元素的最大值。

要删除二维数组，我们写 `delete [] ptr;`。该语句首先释放每一行的内存，然后再删除指针本身。

```
/*PROG 4.20 DYNAMIC ARRAY OF STRINGS */
#include <iostream.h>
#include <conio.h>
void main( )
{
 int n,i;
 clrscr();
 cout << "Enter how many strings \n ";
 cin >> n;
 char **ptr = new char*[n];
 int *len=new int [n];
for(i=0;i<n;i++)
{
    cout << "\n Enter the length of string no." << i+1 << endl;
    cin >> len[i];
    cout << "\nEnter string no." << i+1 << endl;
    ptr[i] = new char [len[i]+1];
    cin >> ptr[i];
}
cout << "STRING \t\t LENGTH\n";
for(i=0;i<n;i++)
    cout << ptr[i] << "\t\t" << len[i] << endl;
delete len;
delete [] ptr;
getch();
}
```

# 输出：

输入有多少个字符串
3
输入第1个字符串的长度
6
输入第1个字符串
Hari
输入第2个字符串的长度
6
输入第2个字符串
Ranjana
输入第3个字符串的长度
7
输入第3个字符串
Manmohan
字符串        长度
Hari          6
Ranjana       6
Manmohan      7

# 说明：

语句 `char **ptr = new char*[n];` 创建了一个大小为 n 的 char 类型指针数组 ptr。`ptr[0]` 将指向第一个字符串，`ptr[1]` 指向第二个字符串，依此类推。在 for 循环中，我们首先依次询问每个字符串的长度。然后使用语句 `ptr[i] = new char [len[i]+1];` 为每个字符串动态分配内存。内存分配完成后，从用户处读取字符串并赋给 `ptr[i]`。最后，显示字符串及其长度。

# 4.6 malloc 与 new 的比较

两者之间有许多区别：

+   1. **malloc** 不能被重载，而 **new** 可以。
+   2. new 运算符可以用来创建对象。
+   3. malloc 的默认返回类型是 **void ***，而 new 返回适当的指针类型，*即*，int 对应于 int 指针，float 对应于 float 指针；在为对象或结构体分配内存时，返回指向用户自定义数据类型的指针。
+   4. **new** 运算符会根据数据类型自动计算对象的大小，无需使用 **sizeof** 运算符。

# 4.7 指向成员的指针运算符

有三个运算符用于指向成员或对象的指针。建议你先弄清楚类的概念，再阅读这一节。这三个运算符是：

+   1. `:: *` 称为指向成员的指针声明符。
+   2. `->*` 称为指向成员的指针解引用运算符（通过指针）。
+   3. `.*` 称为指向成员的指针解引用运算符（通过值）。

要创建指向类成员的指针，可使用 `:: *` 运算符。一般语法如下：

```
data_type class_name :: *ptr_name =&class_name :: member _name;
```

例如，对于类 demo，它有一个名为 data 的 int 数据成员，可以这样声明指针：

```
int demo :: * ptr = &demo :: data;
```

为了更清楚地理解它，回忆一下如何创建指向整数的指针并存储数据的地址。我们会这样写：

```
int * ptr = &data;
```

现在，在 = 运算符左侧的 int 和 *ptr 之间插入 demo ::，在 = 运算符右侧的 & 和 data 之间插入 demo ::。你会得到什么？

```
int demo :: * ptr = &demo :: data;
```

看，定义指向类成员的指针就是这么简单。

定义指针 ptr 后，可以这样使用：

```
demo d;

d.*ptr = 20; // assign value 20 to num of object d.
cout<<d.num<<endl; //display value 20.
```

一旦按照上述方式创建了指针，它就可以用于该类创建的所有对象。与为类的数据成员创建指针类似，我们也可以为对象创建指针。对于类 demo：

```
demo d;
demo *ptr = &d;
```
