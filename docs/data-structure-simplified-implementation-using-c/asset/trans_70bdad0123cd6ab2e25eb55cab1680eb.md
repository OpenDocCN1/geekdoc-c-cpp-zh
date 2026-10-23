

这里的第一个参数表示要输入的名字数量，而第二个参数[length]表示名字可以取的最大长度。

输入10个名字的程序已经在这里讨论过了。

程序：编写一个程序，可以接受10个名字，并显示输出

## 解决方案

```
char name[10][40];
void main
{
int i=0, j=0;
cout<<"enter 10 names";
for(i=0;i<=9;i++)
cin>>name[i];
cout<<" here is the output of names";
for(i=0;i<=9;i++)
cout<<name[i]<<endl;
}
```

读者应当重点了解，二维字符数组的元素可以借助指针轻松访问。

## 2.4 指针

指针是一种变量，能够保存另一个变量的地址。在许多情况下需要保存另一个变量的地址，包括：

-   访问数组元素
-   从函数中改变变量的值
-   动态分配内存
-   在复杂编程中，如链表、树、B树等

为了表示某个变量是指针，它们前面会加上符号“*”。例如，`int *x`，这里的指针是整数类型。这意味着该指针可以保存整数类型变量的地址。

### 2.4.1 声明指针

如前所述，指针是一种能够保存另一个变量地址的变量，相应地，我们需要一个变量，其地址可以存储在指针中，从而我们可以借助指针访问该变量。要声明指针，变量名前面加上星号（*）符号，下面的程序已经演示了这一点。

```
int x=8;
int *p;// variable that is pointer of int type
p=&x; //p now holds the address of variable x
cout<<p;   // print the address of x;
cout<<*p;   // print the value pointed by p;
```

上述语句的工作方式已在图2.5中说明。最初，声明变量“x”，并假设它被分配了地址位置1000。类似地，当声明 `int *p` 时，它也像其他任何变量一样被分配地址。这里我们假设指针“p”被分配了一个新地址，位于内存位置1010。因此，我们可以得出结论：两者是不同的变量，适用于变量的定义仍然适用于指针变量。此外，适用于指针变量的操作也可以应用于它们。

### 2.4.2 访问指针变量

指针也是一个变量，但它不是保存值，而是保存另一个变量的地址。我们假设它保存的是变量“x”的地址，即地址1000。现在，它的值部分将包含1000这个地址，如图2-5所示。当用户显示这个指针的值时，他会得到这个地址作为值。

![](img/9b7c80a1312a664ae505ba138aa3306b_49_0.png)

然而，它便于访问指针所保存地址对应的变量。要访问指针所保存地址中存储的值，我们使用解引用运算符。为了表示解引用，使用语句 `*p`。因此，它会显示存储在该地址的值。指针的用法已在下面的程序中描述。

```
// Program to display the use of pointer
int x=8;
int *p;
p=&x;
cout<<" value of x "<<x // 8
cout<<" value of p="<<p //1000
cout<<" value pointed by *p"<<*p;   // 8 will be printed
```

## 数据结构简化

```
```cpp
*p=30;

cout<<" value of x"<<x; // 30

cout<<" value of p="<<p;          1000

cout<<" value of *p="<<*p;    // 30
```
```

指针广泛用于字符数组（字符串）。同样，指针也用于整数数组。指针在数组中的用法将在后续章节中描述。

### 2.4.3 指针的指针

有时，我们需要存储一个指针的地址，这可以借助指针的指针来完成。指针的指针是一个变量，它保存另一个指针类型变量的地址。

#### 声明指针的指针

声明指针的指针与普通指针类型不同。在指针的指针表示法中，标识符前有两个星号（**）。

-   `int **pp;`             (2.4.1)
-   `int *p;`                (2.4.2)
-   `pp=&p;`                 (2.4.3)

在第2.4.1行中，声明的变量是指针的指针类型。它能够存储另一个指针变量的地址。在第2.4.3行中描述了将指针的地址存储到“指针的指针”中的表示法。指针的指针类型的用法通过以下示例说明。

```
```cpp
// Program to display the use of double pointer
#include<iostream.h>
#include<conio.h>
int main()
{
int v=20;
int *p;
int **pp;
// Assigning address to pointer
p=&v;
pp=&p;
cout<<"value of v="<<v<<endl;
cout<<"Address of v="<<&v<<endl;
cout<<"Address held by p="<<p<<endl;
cout<<" Address of p="<<&p<<endl;
```

```
cout<<"Valued de-referenced of p:"<<*p<<endl;
cout<<" Address of pp:"<<&pp<<endl;
cout<<"Address hold by pp:"<<pp<<endl;
cout<<"Valued de-referenced of *pp:"<<*pp<<endl;
cout<<"Valued de-referenced of **pp:"<<**pp<<endl;
getch();
return 0;
}
```

## 输出

Value of v=20;

Address of v=0xfc1fff4

Address of *p=0xfc1fff2 // Now address of p

Address held by p=0xfc1fff4   //Address hold by p (i.e. of v)

Valued de-referenced of p=20  //de-referencing the value of p (i.e. of v)

Address of pp=0xfc1fff0      // Now address of pp

Address held by pp=0xfc1fff4  //Address hold by pp (i.e. of p)

Valued de-referenced of pp=20 // de-referencing the value of pp(i.e. of v)

### 2.4.4 指针在数组中的使用

指针广泛用于数组。要访问数组元素，我们可以将数组的索引初始化给一个指针变量。例如，在数组“a”中，我们用一个数字列表对其进行了初始化。借助指针访问数组元素已在下面的程序中描述。

```
// Program to access the array element with the help of pointers
int main()
{
int a[]={10,50,20,40,70};
int *x;
x=&a[0];
cout<<x<<endl;
cout<<*x;        //output 10
cout<<*(x+2);        // output 20
cout<<a[2];     // output 20
cout<<*(x+3);        // output 40
```

```
```cpp
cout<<a[3];        // output 40

return 0;
}
```
```

在上面的程序中，指针用数组的基地址进行初始化。因此，语句 `*x` 显示存储在索引“0”处的元素。当使用语句 `*(x+2)` 时，它表示将2加到基地址上，结果得到 `x[2]`。因此，`*(x+2)` 和 `x[2]` 访问的元素结果是相同的。同样，语句 `*(x+3)` 将得到0+3，即第3个索引。相应地，将访问存储在第3个索引处的元素。

### 2.4.5 动态数组的创建

在创建数组时，数组大小可以在运行时或编译时分配。相应地，它可以分为：

-   静态数组
-   动态数组

在编译时分配大小的数组称为静态数组。前面章节中讨论的数组都属于静态数组的范畴。

另一种类型的数组是动态数组，动态数组的空间在运行时分配。在C++中，创建动态数组是借助 `new` 运算符来完成的。下面的示例对此进行了说明。

```
```cpp
程序：创建动态数组并讨论其各种初始化方式。

解决方案：

#include<iostream.h>

#include<conio.h>

int main()
{
int *x;

int *y;
y=new int(45);
x=new int[4];
clrscr();
// elements initialization will follow
x[0]=90;
x[1]=55;
x[2]=32;
```

```
```cpp
x[3]=67;

// From this statement onwards dynamic array will be created.
int i=0;
cout<<"Dynamic array elements are"<<endl;
while(i<3)
{
cout<<"x[i] i="<<i<<"  "<<x[i]<<endl;
i++;
}
cout<<"y ="<<*y<<endl;
getch();
return 0;
}
```
```

```
```cpp
// Program to initialize the dynamic pointer.
#include<conio.h>
int main()
{
int *y;
clrscr();
y=new int(45);
int i=0;
cout<<"y ="<<*y<<endl; //Output will be 45
getch();
return 0;
}
```
```

### 2.4.6 指针数组

指针数组是一个保存指针（地址）的数组。在需要存储多个相似类型指针的地址时，指针数组的使用非常重要。指针数组便于访问，同时提高了所编写程序的效率。指针数组主要用于处理二维数组类型的问题。例如，如果我们打算存储两个或更多数组，那么我们可以使用指针数组。使用指针数组访问三个数组的示例已在下面的程序中描述。

