
```cpp
char str1 [16], str2 [16];
char *JoinedString;

cout << "Enter the first String you want to Concatenate, not greater than 15 characters \n";
cin >> str1;

cout << "\nEnter the second String you want to Concatenate, not greater than 15 characters";
cin >> str2;

JoinedString = JoinString (str1, str2);
cout<<"\nThe result of joined strings is :" << JoinedString;

return 0;
}
```

**输出：**

```text
Enter the first String you want to Concatenate, not greater than 15 characters
Kogent

Enter the second String you want to Concatenate, not greater than 15 characters
Solutions

The result of joined strings is :KogentSolutions
```

- **Q4.** 创建一个程序，从用户处接收两个整数值，并在屏幕上显示它们的和。必须使用一个使用指针的独立函数来将两个数相加。

**答案。**

```cpp
#include <iostream.h>

void add (int *num1, int *num2)
{
*num1 = *num1 + *num2;
}

int main()
{
int a,b;
cout<<"Enter the first Number you want to add ";
cin >>a;
cout<<"\nEnter the second Number you want to add ";
cin >>b;
int *x,*y;
x=&a;
y=&b;
add(x,y);
cout<<"\nThe sum of two numbers you entered is: "<<x;
return 0;
}
```

**输出：**

```text
Enter the first Number you want to add 57

Enter the second Number you want to add 84

The sum of two numbers you entered is: 141
```

- **Q5.** 编写一个程序，使用 for 循环计算 n 个数的和（n 可以是用户在运行时提供的任意整数）。使用通过指针实现的独立函数来获得结果。在我们的例子中，用户为 n 输入了 50。

**答案。**

```cpp
#include <iostream.h>

void sumOfn (int *num)
{
    *num = (*num * (*num+1))/2;
}
int main()
{
    int *sum, n1, n=0;
    cout<<"Enter the value of n: ";
    cin>>n;
    n1 = n;
    sum = &n;
    sumOfn (sum);
    cout<<"Sum of "<<n1<<" number is: "<<n;
    return 0;
}
```

**输出：**

```text
Enter the value of n: 50
Sum of 50 number is: 1275
```

现在，让我们看看如何将指针与函数一起使用。

## 4.3 将指针用作函数参数

函数是一组具有名称的语句，用于在运行时执行特定操作。函数还可以接受参数，这些参数对于从程序的其他任何部分调用该函数是必不可少的。我们已经在第 3 章*《使用数组和函数》*中讨论过函数。在 C++ 中，我们可以将指针用作函数参数。将指针作为函数参数传递的主要目的是反映在函数体内部对变量所做的更改，并使这些更改从调用该函数的位置可见。将指针用作函数参数称为按引用调用方法。这与按值调用方法形成对比，在按值调用方法中，对函数体内数据所做的任何更改都不会反映到函数体外部。清单 12 展示了一个将指针作为函数参数传递的程序（你可以在 CD 的 `code\chapter4` 文件夹中找到 `PointerArgument.cpp` 文件）：

### ▶ 清单 12：使用指针按引用传递变量

```cpp
#include<iostream.h>

void add(int *p1);//function prototype declaration
int main()
{
    int n1=10;
    cout<<"Initial value of n1 is "<<n1<<endl;// value before function call
    add(&n1);//calling function with arguments matching the pointer variables
    cout<<"Value of n1 after adding 5 is: "<<n1<<endl;

    return 0;
}

void add(int *p1)
{
    *p1=*p1+5;//change the value at the address passed
}
```

**输出：**

```text
Initial value of n1 is 10
Value of n1 after adding 5 is: 15
```

在清单 12 中，我们的主要目的是将指针变量作为函数参数传递。首先，我们声明一个整型变量 `n1`。现在，我们使用 `&` 运算符传递该变量的地址。在函数体内部，我们通过指针变量 `*p1` 所引用的地址，将 `n1` 的值更改 5。调用 `add()` 函数后，`n1` 的值通过指针被更改，并且更改后的值会被打印出来。

## 4.4 从函数返回指针

我们知道，一个函数只能返回单个值。然而，它可以通过使用指针返回多个值。我们必须将指针声明为函数的返回类型，以便该函数可以返回多个值。然而，只有当函数必须使用指针变量，并初始化该指针变量以引用其函数体结构中的数组元素时，函数才能返回指针变量。我们知道，指针变量包含数组第一个元素的地址。因此，函数返回数组第一个元素的地址，以便我们可以轻松访问并操作其余元素。因为通过递增数组第一个元素的索引值，就可以轻松访问数组第二个元素的地址。清单 13 展示了一个用于演示从函数返回数组的程序（你可以在 CD 的 `code\chapter4` 文件夹中找到 `ReturnPointer.cpp` 文件）：

### ▶ 清单 13：从函数返回数组

```cpp
#include <iostream.h>

int* count(int x)
{
    int *arr = new int[x];
    int element;
    for (int i=0; i<x; i++)
    {
        cout<<"Enter arr["<<i<<"] :";
        cin>>element;
        arr[i] = element;
    }
    return arr;
}

int main()
{
    int j;
    cout<<"Enter number of element: ";
    cin>>j;
    int *arr=0;
    arr = count(j);
    cout<<"Element of arr are :"<<endl;
    for (int i=0; i<j; i++)
    cout <<arr[i]<<endl;
    delete [] arr;
    return 0;
}
```

**输出：**

```text
Enter number of element: 5
Enter array[0] :6
Enter array[1] :8
Enter array[2] :4
Enter array[3] :2
Enter array[4] :15
Element of arr are:
6
8
4
2
15
```

在清单 13 中，我们创建了一个函数——count()。count() 函数的返回类型是整型指针数组，即 arr。count() 函数还接受一个整型参数 x。当为该参数（x）传递值时，整型指针数组（arr）被初始化为一个数组。在 count() 函数内部，使用 for 循环为数组元素取值。然后，count() 函数返回这个整型数组。在 main() 函数中，我们从用户处接受一个整数，并将该数字作为参数值传递，以调用 count() 函数。最后，count() 函数返回的值被显示到屏幕上。

正如我们所知，函数返回单个值。它可以是整数值、char 值、float 值或任何其他类型的值。字符串包含多个 char 值。因此，我们不能从函数返回字符串。在这种情况下，我们使用 char 类型的指针变量，它返回该字符串第一个字符的地址。我们可以通过使用 char 类型的指针变量访问整个字符串。清单 14 展示了一个返回字符串值的程序（你可以在 CD 的 code\chapter4 文件夹中找到 ReturnString.cpp 文件）：

### 清单 14：从函数返回字符串值

```cpp
#include <iostream.h>
#include <string.h>
char* count(char *str)
{
    char *ch="Welcome ";
    strcat(ch, str);
    return ch;
}
int main()
{
    char *arr, str[50];
    cout<<"Enter name :";
    cin>>str;
    arr = count(str);
    cout<<endl;
    cout<<"The string value returned by count() function is : ";
    cout<<arr;
    return 0;
}
```

**输出：**

```text
Enter name :Dheeraj
The string value returned by count() function is : Welcome Dheeraj
```

> 在前面的程序中，如果你输入的字符串包含空格，那么空格之后的字符将不会显示。

在清单 14 中，count() 函数返回字符串变量（ch）的地址，该地址存储在 main() 函数中声明的指针 *arr 变量中。这个指针变量（*arr）用于显示存储在指针 arr 变量中的字符串数据。

## 测试你的知识

- **Q6.** 编写一个程序，首先询问用户想要输入的总数，然后接受这些数字，并使用指向数组的指针计算所有数字的和。

**答案。**

```cpp
#include <iostream.h>

int* count(int x)
{
    int *arr = new int[x];
    int element;
    for (int i=0; i<x; i++)
    {
        cout<<"\nEnter number "<<(i+1)<<": ";
        cin>>element;
        arr[i] = element;
    }
    return arr;
}
int main()
{
    int j, sum = 0;
    cout<<"Enter number of digits you want to add: ";
    cin>>j;
    int *arr=0;
    arr = count(j);
    cout<<"Sum of the Numbers you entered is :"<<endl;
    for (int i=0; i<j; i++)
    {
        sum = sum + arr[i];
```

