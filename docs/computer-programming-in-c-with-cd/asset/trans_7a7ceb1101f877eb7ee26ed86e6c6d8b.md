

```text
Enter second number 6
Greatest common divisor of 8 and 6 is 2
Lowest common multiple of 8 and 6 is 24
```

> 借助合适的程序和函数，解释按引用传递参数和按值传递参数（孟买大学，2007 年 12 月）

除了将值作为函数参数传递外，还可以将数组作为函数参数传递。下面一节我们将讨论如何将数组传递给函数。

## 将数组传递给函数

你可以通过将数组名和数组大小作为参数传递给函数，从而将数组传递给函数。使用数组调用函数时，只需传递数组名（不需要传递数组大小）。而在声明或定义函数时，需要将数组名及其大小作为方法参数传递。代码清单 16 展示了如何将数组传递给函数（可在随书光盘的 code/chapter3 文件夹中找到 Func11.cpp 文件）：

### 代码清单 16：将数组传递给函数

```cpp
#include <iostream.h>

int main()
{
    void display(int array[20], int size);
    int array[20], size, i;
    cout<<"Enter size of array : ";
    cin>>size;
    for(i=0;i<size;i++)
    {
        cout<<"Enter element of array["<<i<<"]: ";
        cin>>array[i];
    }
    cout<<endl;
    display(array, size);
    return 0;
}
void display(int array[20], int n)
{
    int i;
    cout<<"The element of array are : "<<endl;
    for(i=0;i<n;i++)
    {
        cout<<array[i]<<endl;
    }
}
```

**输出：**

```text
Enter size of array : 6
Enter element of array[0]: 2
Enter element of array[1]: 3
Enter element of array[2]: 8
Enter element of array[3]: 4
Enter element of array[4]: 6
Enter element of array[5]: 0

The element of array are :
2
3
8
4
6
0
```

在代码清单 16 中，定义了 display() 函数，它接受一个包含二十个元素的数组和一个整型变量作为参数。在 display() 函数中，使用 for 循环向用户显示数组（作为参数传递）的元素。使用 main() 函数从用户处接受数组元素，然后调用 display() 函数，后者进而向用户显示数组元素。

![](img/8a6886c00caa6a1651a6c0e62bff341f_192_0.png)

> 我们将在第 04 章讨论函数如何使用指针返回数组和字符串。

## 测试你的知识

### Q9. 编写一个程序来对矩阵进行转置。

答：

```cpp
#include<iostream.h>
#include<iomanip.h>
void transpose(int row, int col, int a[10][10])
{
    for(int i=0;i<col;i++)
    {
        for(int j=0;j<row;j++)
        {
            cout<<a[j][i]<<setw(5);
        }
        cout<<setw(0);
        cout<<endl;
    }
}
void display(int row, int col, int a[10][10])
{
    for(int i=0;i<row;i++)
    {
        for(int j=0;j<col;j++)
        {
            cout<<a[i][j]<<setw(5);
        }
        cout<<setw(0);
        cout<<endl;
    }
}
void main()
{
    int i, j, x[10][10];
    int row, col;
    cout<<"Enter row of Matrix x ";
    cin>>row;
    cout<<endl;
    cout<<"Enter col of Matrix x ";
    cin>>col;
    cout<<endl;
    cout<<"Enter element of matrix x now"<<endl;
    for(i=0;i<row;i++)
    {
        for(j=0;j<col;j++)
        {
            cout<<"Enter element of x["<<i<<"]["<<j<<"]:";
            cin>>x[i][j];
        }
    }
    cout<<"Element of matrix x is:"<<endl;
    display(row, col, x);
    cout<<"Transpose of matrix x is:"<<endl;
    transpose(row, col, x);
}
```

**输出：**

```text
Enter row of Matrix x 3
Enter col of Matrix x 2
Enter element of matrix x now
Enter element of x[0][0]:1
Enter element of x[0][1]:2
Enter element of x[1][0]:3
Enter element of x[1][1]:4
Enter element of x[2][0]:5
Enter element of x[2][1]:6
Element of matrix x is:
1    2
3       4
5       6
Transpose of matrix x is:
1       3       5
2       4       6
```

### Q10. 编写一个程序对数组元素进行排序。

答：

```cpp
#include <iostream.h>
void display(int array[], int n)
{
        int i;
        for(i=0;i<n;i++)
        {
                cout<<array[i]<<endl;
        }
}
void sort(int array[], int n)
{
        int temp = 0;
        for (int i=0; i<n; i++)
        {
                for(int j=0; j<=i; j++)
                {
                        if(array[i] < array[j])
                        {
                                temp = array[i];
                                array[i] = array[j];
                                array[j] = temp;
                        }
                }
        }
        display(array, n);
}
int main()
{
        int array[20], size, i;
        cout<<"Enter size of array : ";
        cin>>size;
        for(i=0;i<size;i++)
        {
                cout<<"Enter element of array["<<i<<"] : ";
                cin>>array[i];
        }
        cout<<"Before sorting elements of array[] are : "<<endl;
        display(array, size);
        cout<<"After sorting elements of array[] are : "<<endl;
        sort(array, size);
        return 0;
}
```

**输出：**

```text
Enter size of array : 8
Enter element of array[0]: 3
Enter element of array[1]: 4
Enter element of array[2]: 6
Enter element of array[3]: 8
Enter element of array[4]: 2
Enter element of array[5]: 9
Enter element of array[6]: 5
Enter element of array[7]: 1
Before sorting elements of array[] are :
3
4
6
8
2
9
5
1
After sorting elements of array[] are:
1
2
3
4
5
6
8
9
```

让我们学习如何将常量作为函数参数传递。

## 将函数参数作为 const 传递

声明 const 变量意味着不能在程序中更改其值。你可以将参数传递给函数，以在函数体内执行特定任务。还可以在函数体内更改参数的值。当将 const 变量作为参数传递给函数时，不能在函数体内修改该 const 变量的原始数据。编译器会产生错误消息 *无法修改 const 对象*。代码清单 17 展示了当你在 adder() 函数体内修改 const 参数时，编译器如何产生错误消息（可在随书光盘的 code/chapter3 文件夹中找到 Func12.cpp 文件）：

### 代码清单 17：将 const 参数传递给函数

```cpp
#include <iostream.h>
#include <stdio.h>
int adder(const int array[], int num);
int main()
{
    int data[] = {1, 2, 3, 4};
    int total = adder(data, 4);
    cout<<"The total is : "<<total<<endl;
    return 0;
}
int adder(const int array[], int num)
{
    int sum = 0, temp;
    for(int i=0; i<num; i++)
    {
        array[i] = array[i]+i;
        sum += array[i];
    }
    return sum;
}
```

在代码清单 17 中，创建了 adder() 函数，它接受一个常量整型数组和一个整数作为参数。adder() 函数有一个 for 循环，用于为数组元素赋值。此外，还定义了 main() 函数，其中包含一个存有四个值的整型数组（data）。从 main() 函数调用 adder() 函数，以显示数组元素之和。

编译该程序时，它会在第 16 条语句（array[i] = array[i]+i;）处产生错误消息 *无法修改 const 对象*。这意味着不能在 adder() 函数体内更改 const 参数。

## 将字符串传递给函数

将字符串值作为参数传递给函数，被视为将字符串传递给函数。此过程类似于将整数值传递给函数。作为参数传递给函数的字符串可以在函数体内使用和更改。代码清单 18 展示了如何将字符串值作为参数传递给 display() 函数。可在随书光盘的 code/chapter3 文件夹中找到 Func13.cpp 文件：

### 代码清单 18：将字符串传递给函数

```cpp
#include <iostream.h>
#include <stdio.h>
int main()
{
    void display(char array[20]);
    char name[20];
    int size, i;
    cout<<"Enter name : ";
    gets(name);
    cout<<endl;
    display(name);
    return 0;
}
void display(char array[20])
{
    cout<<"Welcome ";
    cout<<array;
}
```

**输出：**

```text
Enter name : Mahtab Alam
Welcome Mahtab Alam
```

在代码清单 18 中，名为 name 的字符串通过 `void display(name);` 作为参数传递给 display() 函数。然后，`main()` 函数通过将字符串变量 name 作为实际参数传递来调用 `display()` 函数。随后使用该函数打印 name 字符串变量的值。

让我们学习 C++ 中递归的使用。

## 使用递归

有时，你会在函数中编写一段重复执行以完成任务的代码。为了尽量减少这种重复，可以编写一个调用自身的函数。函数调用自身的情况称为递归，该函数称为递归函数。该函数会被反复调用，除非函数体中的代码通过在 `if` 语句中实现条件来终止调用链。以下是递归函数的语法：

```cpp
void recursion(arguments)
{
    statements1
    if (condition)

    recursion(arguments)
    statements2
}
```

在前面的语法中，recursion 是递归函数的名称，该函数包含一组特定语句，其中包括 `if` 语句。在 `if` 语句之后，会调用这个递归（recursion）函数。

递归函数必须有一个停止条件来停止递归函数，否则，该函数会继续调用自身，直到程序栈耗尽。正如

