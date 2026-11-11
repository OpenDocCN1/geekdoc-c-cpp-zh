
在代码清单 7 中，创建了包含三个元素的结构体 Student。在 `main()` 函数中，创建了一个 Student 结构体数组（包含三项）。接下来，使用数组的每一项访问该结构体的所有三个元素。结构体的每个元素都被赋予用户在运行时指定的值，并显示在屏幕上。

## 测试你的知识

**问题 5.** 创建一个使用结构体显示书籍详细信息的程序。你必须在创建结构体实例时为结构体元素赋值。

**答案：**

```cpp
#include <iostream.h>
#include <string.h>

struct BookInfo
{
    char title[64];
    char publisher[64];
    char author[64];
    float price;
    int pages;
};

int main()
{
    BookInfo book = {"My Experiences", "ABCPress", "Ruby", 290.00,
    500 };

    cout << "Book: " << book.title << " by " <<book.author << endl;
    cout<< "Publisher: " << book.publisher << endl;
    cout<< "Book Rate: " << book.price<<endl;
    cout<< "Total Pages in book: " << book.pages;
    return 0;
}
```

**输出：**

```text
Book: My Experiences by Ruby
Publisher: ABCPress
Book Rate: 290
Total Pages in book: 500
```

**问题 6.** 使用结构体中的数组接受并显示 10 位客户的账号。

**答案：**

```cpp
#include <iostream.h>

struct account
{
    double AccNo[10];
};

int main()
{
    account a1;
    for (int i=0; i<10; i++)              //for accepting account numbers.
    {
        cout<<"Enter Account Number "<<(i+1)<<": ";
        cin>>a1.AccNo[i];
        cout<<endl;
    }
    for (int i=0; i<10; i++)              //for displaying account numbers
    {
        cout<<"The Account Number "<<(i+1)<<" is: "<<a1.AccNo[i];
        cout<<endl;
    }
    return 0;
}
```

**输出：**

```text
Enter Account Number 1: 15465

Enter Account Number 2: 64566

Enter Account Number 3: 25625

Enter Account Number 4: 36356

Enter Account Number 5: 36353

Enter Account Number 6: 36235

Enter Account Number 7: 36562

Enter Account Number 8: 35653

Enter Account Number 9: 98152

Enter Account Number 10: 65942

The Account Number 1 is: 15465
The Account Number 2 is: 64566
The Account Number 3 is: 25625
The Account Number 4 is: 36356
The Account Number 5 is: 36353
The Account Number 6 is: 36235
The Account Number 7 is: 36562
The Account Number 8 is: 35653
The Account Number 9 is: 98152
The Account Number 10 is: 65942
```

## 将结构体数组用作函数参数

与将数组作为参数传递给函数类似，你也可以将结构体数组作为参数传递给函数。这个数组参数可以在函数体内部用于初始化和访问结构体成员。现在，为了清楚地理解这个概念，请修改代码清单 7 中所示的程序。为此，创建一个单独的函数来接受学生记录并将其显示在屏幕上。代码清单 8 显示，用于接受和显示学生记录的函数将 `main()` 函数中创建的结构体数组作为它们的参数（你可以在 CD 的 code\chapter5 文件夹中找到 StructureArgument2.cpp 文件）：

**代码清单 8：** 将结构体数组作为函数参数传递

```cpp
#include <iostream.h>
#include <stdio.h>

struct Student
{
    char name[20];
    int age;
    float marks;
};

void Accept_Details (struct Student s1 [])   //accepting student details
{
    for (int i=0; i<3; i++)
    {
        cout<<"Enter the record of "<< (i + 1)<<" student\n";
        cout<<"Name: ";
        cin>>s1[i].name;
        cout<<"Age: ";
        cin>>s1[i].age;
        cout<<"Marks: ";
        cin>>s1[i].marks;
        cout<<"\n";
    }
}

void Display_Details (struct Student s2 [])  //displaying student details
{
    for (int i=0; i<3; i++)
    {
        cout<<"Displaying the record of "<< (i + 1)<<" student\n";
```

将结构体 student 的数组作为它们的参数，并使用该参数执行它们特定的操作。

## 测试你的知识

**问题 7.** 创建一个接受三台空调（AC）的详细信息并在屏幕上显示它们的程序。你必须创建单独的函数来接受和显示空调详细信息，这两个函数都将结构体实例作为参数。该结构体包含用于保存空调详细信息的变量。

**答案：**

```cpp
#include <iostream.h>
#include <stdio.h>

struct AC
{
    char name[20];
    int price;
    float capacity;
};

void Accept_Details (struct AC s1 [])        //accepting AC details
{
    for (int i=0; i<3; i++)
    {
        cout<<"Enter the Details of "<< (i + 1)<<" AC\n";
        cout<<"Company Name: ";
        cin>>s1[i].name;
        cout<<"Price: ";
        cin>>s1[i].price;
        cout<<"Capacity in Tonns: ";
        cin>>s1[i].capacity;
        cout<<"\n";
    }
}

void Display_Details (struct AC s2 [])       //displaying AC details
{
    for (int i=0; i<3; i++)
    {
        cout<<"Displaying the Details of "<< (i + 1)<<" AC\n";
        cout<<"Company Name: "<<s2[i].name<<"\n";
        cout<<"Price: "<<s2[i].price<<"\n";
        cout<<"Capacity in Tonns: "<<s2[i].capacity<<"\n";
    }
}

int main()
{
    cout<<"Enter the record of 3 ACs one by one"<<"\n";
    cout<<"------------------------------\n";
    AC s [3];

    Accept_Details (s);
    Display_Details (s);

    return 0;
}
```

**输出：**

```text
Enter the record of 3 ACs one by one
-----------------------------------------------
Enter the Details of 1 AC
Company Name: Hitachi
Price: 35000
Capacity in Tonns: 2

Enter the Details of 2 AC
Company Name: LG
Price: 25000
Capacity in Tonns: 1.5

Enter the Details of 3 AC
Company Name: Voltas
Price: 15000
Capacity in Tonns: 1.25
Displaying the Details of 1 AC
Company Name: Hitachi
Price: 35000
Capacity in Tonns: 2
Displaying the Details of 2 AC
Company Name: LG
Price: 25000
Capacity in Tonns: 1.5
Displaying the Details of 3 AC
Company Name: Voltas
Price: 15000
Capacity in Tonns: 1.25
```

## 将指针与结构体一起使用

你可以将指针与结构体一起使用，以存储结构体变量的地址。这个指针可用于初始化和访问结构体变量。此外，你可以为一个结构体创建多个指针，这些指针可以彼此独立使用，这意味着每个结构体指针都可以为结构体元素存储和访问不同的值，而不影响其他结构体指针定义的值。让我们考虑一个包含两个整数成员的结构体，例如 quantity 和 price。

这可以使用以下代码片段声明：

```cpp
struct bucket
{
    int quantity;
    int price;
};
```

现在，创建并初始化结构体变量 bucket1 和 bucket2，并使用点（.）运算符访问结构体成员，如下面的代码片段所示：

```cpp
bucket1.quantity = 1000;
bucket1.price = 10;
bucket2.quantity = 2000;
bucket2.price = 20;
```

带有上述结构体变量初始化的结构体变量 bucket1 和 bucket2 如图 3 所示：

![](img/8a6886c00caa6a1651a6c0e62bff341f_292_0.png)

▲ 图 3：结构体变量 bucket1 和 bucket2 的表示

在图 3 中，可以看到 bucket 结构体有两个变量：bucket1 和 bucket2。这两个变量用不同的值初始化结构体变量，而不影响另一个结构体变量的值。

代码清单 9 显示了使用点（.）运算符声明和访问结构体变量的方法（你可以在 CD 的 code\chapter5 文件夹中找到 DotOperator.cpp 文件）：

**代码清单 9：** 使用点（.）运算符声明和访问结构体变量

```cpp
#include <iostream.h>

struct bucket
{
        int quantity;
        int price;
};                          //declaring a structure
int main()
{
    bucket bucket1;                 // declaring a structure variable
    bucket bucket2;                 //declaring a structure variable
    bucket1.quantity = 1000;
    bucket1.price = 10;
    bucket2.quantity = 2000;
    bucket2.price = 20;
    cout<<"printing quantity of bucket1:"<<bucket1.quantity<<endl;
    cout<<"printing price of bucket1:"<<bucket1.price<<endl;
    cout<<"printing quantity of bucket2:"<<bucket2.quantity<<endl;
    cout<<"printing price of bucket2:"<<bucket2.price<<endl;
    return 0;
}
```

**输出：**

```text
printing quantity of bucket1:1000
printing price of bucket1:10
printing quantity of bucket2:2000
printing price of bucket2:20
```

声明结构体变量（bucket1）时，会分配复合内存，其大小等于所有成员大小之和。你可以声明结构体类型的指针变量来存储结构体变量的内存地址。现在，可以按如下方式声明 bucket 结构体的两个指针变量 ptr1 和 ptr2：

```cpp
bucket *ptr1,*ptr2;
```

现在，按如下方式将结构体变量 bucket1 和 bucket2 的地址赋给结构体指针变量 ptr1 和 ptr2：

```cpp
ptr1 = & bucket1;
ptr2 = & bucket2;
```

现在，指针变量 ptr1 指向 bucket1，如图 4 所示：

![](img/8a6886c00caa6a1651a6c0e62bff341f_293_0.png)

▲ 图 4：由 ptr1 指向的 bucket1 的表示

现在，ptr2 指向 bucket2，如图 5 所示：
