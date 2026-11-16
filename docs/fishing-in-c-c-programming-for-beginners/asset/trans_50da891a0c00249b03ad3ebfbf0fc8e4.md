

int main()
{
    uli a=5;
    cout<<a;
    return 0;
}

这里，我们将 unsigned long int 别名设置为 uli。这里，输出将是 5。

请考虑以下程序：

```
#include<iostream>
using namespace std;
struct student
{
    char*name;
    int roll;
};
typedef struct student stu;
int main()
{
    stu s1;
    s1.roll=5;
    s1.name="Aman";
    cout<<s1.roll<<"\n";
    cout<<s1.name;
    return 0;
}
```

输出
Aman

这里，我们使用了 struct student 的别名。

## #define

此宏可用于多种用途。它可以用于为任何常量、变量、函数甚至语句命名。我们还可以使用此术语生成函数！

请考虑以下程序：

```
#include<iostream>
using namespace std;
#define a 50
int main()
{
    cout<<a;
    return 0;
}
```

这里，输出将是 50。因此，您可以在程序中到处使用 a 来代替 50。

请考虑以下程序：

```
#include<iostream>
using namespace std;
#define a 50*2+3
int main()
{
    cout<<a;
    return 0;
}
```

这里，输出将是 103

请考虑以下程序

```
#include<iostream>
using namespace std;
#define a cout<<"It's amazing";
int main()
{
    a
    return 0;
}
```

这里，程序中没有错误，我们也没有使用分号，因为它已包含在 cout 语句中。其输出将是 **它太神奇了**

请考虑以下程序

```
#include<iostream>
using namespace std;
#define a cout<<("Enter a number"); \
int x; \
cin>>("%d",&x);\
cout<<("\nYour number is %d",x);
int main()
{
    a
    return 0;
}
```

输出
Enter a number
5
Your number is 5

这里，我们将整个块合并为 a。\ 用于将下一行包含到 a 中。由于我们不希望将 int main() 包含到 a 中，因此在最后一个 cout 语句中没有使用 \。现在，每当需要从用户获取输入时，我们可以做两件事。要么多次复制粘贴整个代码，要么多次使用 a。显然，多次使用 a 更简单，因为程序长度会非常短。

现在，让我们使用 #define 来创建一个函数。

请考虑以下程序

```
#include<iostream>
using namespace std;
#define square(x) x*x
int main()
{
    cout<<square(5);
}
```

这里，输出将是 25。现在，让我们创建一个更复杂的函数。

请考虑以下程序

```
#include<iostream>
using namespace std;
#define pow(a,b) int power=1;\
int i;\
for(i=0;i<b;i++)\
    power*=a;
int main()
{
    pow(2,3);
    cout<<power;
}
```

这里，pow(2,3) 计算 2 的 3 次幂并将值存储在 power 变量中。因此，存储的值将是 8。

#define 也可用于测试条件。让我们看看如何操作。

请考虑以下程序：

```
#include<iostream>
using namespace std;
#include<math.h>
#define a
int main()
{
#ifdef a
    cout<<("5+2=8\n");
    cout<<("\"Make Fool\" process was ON\n");
#endif
    cout<<("5+2=7");
}
```

由于 a 已定义，输出将是

5+2=8
“Make Fool” process was ON
5+2=7

这里使用了 \，这是因为如果我们想要显示，不能直接放置 “，因为程序会认为字符串已结束，当我们再次给出 “ 来结束字符串时，它会报错说“[Error] expected ’) before ’Make”。因此，我们使用 \ 来避免程序的混淆。请记住，这里 #endif 是必须的，否则会显示错误“Unterminated #ifdef”。另外，请注意这里 a 被定义为空。如果需要，您可以为其定义某个值。

现在，请考虑以下程序：

```
#include<iostream>
using namespace std;
#include<math.h>
/*#define a*/
int main()
{
#ifdef a
    cout<<("5+2=8\n");
    cout<<("\"Make Fool\" process was ON\n");
#endif
    cout<<("5+2=7");
}
```

由于这里的 define 语句已被注释，编译器会忽略它。因此，编译器将理解 a 未定义，因此输出将是 5+2=7

这里也可以使用 #ifdef...#elif...#else...#endif 条件。

请考虑以下程序

```
#include<iostream>
using namespace std;
#define a
int main()
{
#ifdef a
    cout<<("5+2=8\n");
#else
    cout<<("\"Make Fool\" process was ON\n");
#endif
    cout<<("5+2=7");
}
```

输出将是

5+2=8
5+2=7

请考虑以下程序：

```
#include<iostream>
using namespace std;
#define a
int main()
{
#ifdef b
    cout<<("5+2=8\n");
#elif 5==4+1
    cout<<("\"Make Fool\" process was ON\n");
#endif
    cout<<("5+2=7");
}
```

输出将是

Make Fool process was ON
5+2=7

我们还可以使用嵌套条件。在这里，elif 代表 elseif。我们还可以使用否定定义，即 #ifndef 表示如果未定义。

请考虑以下程序：

```
#include<iostream>
using namespace std;
#define a
int main()
{
#ifndef b
    cout<<("5+2=8\n");
#elif 5==4+1
    cout<<(" \"Make Fool\" process was ON\n");
#endif
    cout<<("5+2=7");
}
```

这里，输出将是

5+2=8

5+2=7

![](img/5340985153962870d4e4a3b9453b9146_134_0.png)

## 结构体

结构体是将不同数据类型集合到单个实体中的用户定义集合。

例如：

```
struct student
{
char*name;
char section;
int roll;
};
```

右花括号后应有分号。结构体是用户定义的数据类型，因此首先需要声明此数据类型的变量来存储数据。

例如：struct student s1;

要访问结构体的元素，我们使用点运算符。例如：

cout<<s1.roll;

以下程序对此进行了说明：

```
#include<iostream>
using namespace std;
struct student
{
    char*name;
    char section;
    int roll;
};
int main()
{
    struct student s1;
    s1.name="Aman";
    s1.roll=12;
    s1.section='D';
    return 0;
}
```

我们还可以在定义结构体时声明变量。例如

```
struct student
{
int roll;
char section;
char*name;
}s1,s2;
```

## 结构体中的输入//输出

结构体变量可以像普通变量一样用于输入和输出。迄今为止使用的所有函数都可以与结构体一起使用。例如，请考虑以下程序。

```
#include<iostream>
using namespace std;
struct student
{
     char name[50];
     char section;
     int roll;
};
int main()
{
    struct student s1;
    cout<<"Enter the name of student\n";
    gets(s1.name);
    cout<<"Enter the section of student\n";
    cin>>s1.section;
    cout<<("Enter the roll number of the student\n");
    cin>>s1.roll;
    cout<<("\nThe name of student is: ");
    puts(s1.name);
    cout<<"\nThe section of the student is:"<<s1.section;
    cout<<"\nRoll number of the student is: "<<s1.roll;
    return 0;
}
```

## 结构体数组

与其他数据类型一样，我们可以使用结构体数组。以下程序对此进行了说明：

```
#include<iostream>
using namespace std;
struct student
{
    char name[50];
    char section;
    int roll;
};
int main()
{
    struct student s1[5];
    int i;
    for(i=0;i<5;i++)
    {
        cout<<("Enter the name of student\n");
        gets(s1[i].name);
        cout<<("Enter the section of student\n");
        cin>>s1[i].section;
        cout<<("Enter the roll number of the student\n");
        cin>>s1[i].roll;
        fflush(stdin);
    }
    for(i=0;i<5;i++)
    {
        cout<<("\nThe name of student is: ");
        puts(s1[i].name);
        cout<<("\nThe section of the student is: "<<s1[i].section);
        cout<<("\nRoll number of the student is: "<<s1[i].roll);
    }
    return 0;
}
```

在这里，您可以看到我们使用了新函数 fflush(stdin)，为什么呢？事实是，一旦输入学号并按下回车键，学号就会被 s1[i].roll 接受，而回车键会保留在缓冲区中以供下一个输入。现在，会显示姓名查询并需要输入，由于回车键在缓冲区中以供下一个输入，因此它现在被当作姓名接收，并且部分查询会立即出现。因此，用户会认为程序跳过了输入。fflush(stdin) 会刷新输入缓冲区，因此程序会要求输入姓名，用户可以给出输入。只需删除 fflush(stdin); 语句并看看会发生什么。

