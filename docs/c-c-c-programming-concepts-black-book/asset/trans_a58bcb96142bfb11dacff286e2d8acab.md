

![](img/43c5f409f9b17790a628c4b4df854b61_170_0.png)

## 第 5 章　C 语言的高级概念

| 如果需要了解以下信息： | 参见页码： |
|---|---|
| 结构体 | 130 |
| 声明结构体 | 131 |
| 联合体 | 148 |
| C 语言中的文件管理 | 150 |
| 二进制文件 | 160 |
| 文件管理函数 | 166 |
| 位运算符 | 169 |
| 类型限定符 | 176 |
| C 语言中的内存分段 | 178 |

## 第 5 章

使用函数和数组可能无法满足程序员在使用 C 语言时需要执行的所有实际任务。这类活动中的很大一部分需要高级且复杂的概念。其中一些概念是结构体、联合体和文件。

结构体是 C 语言中最常用的构造之一。它们使程序员能够将不同类型的信息组合在一起。与结构体类似，联合体也包含不同类型的信息。然而，与结构体不同，联合体的所有成员共享同一个内存位置。文件是另一种关键的信息管理类型。C 提供两种类型的文件：文本文件和二进制文件。文本文件由连续的字符组成，而二进制文件是字节的集合。C 还提供了多个文件管理函数，例如 fclose()、feof()、ferror()、fgetpos()、freopen() 和 ftell()，用于执行与文件相关的任务。

在本章中，我们将学习 C 语言编程中的一些高级概念。本章将深入讨论结构体和联合体及其实现。我们还将学习 C 语言中文件管理的概念。此外，我们还会学习 C 语言中的位运算及其实现。在本章末尾，我们将学习 C 语言中的类型限定符和内存分段。

让我们从详细讨论结构体开始本章。

### 结构体

C 语言提供了一些基本数据类型，如 int、float 和 char，用于存储少量信息。然而，在现实世界中，信息不会像基本数据类型那样只包含少量数据；相反，它表现为若干事物的集合，其中每个事物都有各自的属性。让我们来看一个现实生活中的实体——汽车。它可以包含车型名称和价格等信息，这些信息在性质上是不同的。也就是说，车型名称是字符串，而价格是整数。现在，为了对这些信息执行类似的操作，我们可以使用多个数组来保存相同类型的元素。清单 5.1 展示了存储汽车信息的数组：

清单 5.1：在数组中存储信息

```c
#include<stdio.h>

int main()
{
    char name[3][10];
    int price[3];
    int i;

    for(i=0;i<=2;i++)
    {
        printf("\n Enter Name and Price ");
        scanf("%s %d",&name[i],&price[i]);
    }

    printf("\n Information Entered is \n");
    for(i=0;i<=2;i++)
    {
        printf("\n Name [%s] and Price [%d] ",name[i],price[i]);
    }

    getch();
    return 0;
}
```

上述程序的输出如下：

```
Enter Name and Price   ALTO 300000
Enter Name and Price   INNOVA 900000
Enter Name and Price   MERCEDES 2500000

Information Entered is

Name [ALTO] and Price [300000]
Name [INNOVA] and Price [900000]
Name [MERCEDES] and Price [2500000]
```

虽然数组可以帮助存储许多信息，但其可扩展性不够强。在我们的场景中，我们可能需要存储更多与汽车相关的信息，但如果我们通过数组处理海量数据，数组可能会变得笨重。为了克服这个问题，C 提供了一种称为结构体的数据类型，它允许我们将不同类型的数据组合在一起。结构体可以包含数据类型各异的元素。结构体中的每个单独元素被称为结构体成员。

让我们先学习如何声明结构体。

### 声明结构体

声明结构体比声明数组更复杂，因为结构体包含许多独立的元素。声明结构体的通用形式如下：

```c
struct objectName {
    member 1;
    member 2;
    member 3;
    .................
    member n;
};
```

在上述声明中，struct 是关键字，objectName 是为该结构体指定的名称。各个成员由 member1、member2、... 和 member n 表示。这些成员可以是变量、指针、数组或任何其他结构体。结构体内的成员名称应各不相同。换句话说，同一个结构体不允许有两个成员同名。结构体声明完成后，我们可以按如下方式声明结构体类型的各个变量：

```c
struct objectName variable 1, variable 2,..............,variable n;
```

来看一个结构体声明的示例：

```c
struct Car {
    char name[20];
    float price;
    char model[20];
    int year;
};
```

对于上述声明，结构体变量可以声明如下：

```c
struct Car car1,car2,car3;
```

结构体变量声明会为每个变量预留内存。在我们的示例中，每个结构体变量将总共分配 52 字节的内存。请注意，这些字节总是分配在相邻的内存位置。

结构体类型和结构体变量的声明可以合并在一起，如下所示：

```c
struct car {
    char name[20];
    float price;
    char model[20];
    int year;
} car1, car2;
```

与变量和数组类似，结构体变量可以在声明时进行初始化。初始化结构体变量的格式如下：

```c
struct car car1 = {"HONDA", 1400000, "CITY", 2009};
```

在上述格式中，第一个值将赋给第一个成员变量，第二个值将赋给第二个成员变量，第三个值将赋给第三个成员变量，第四个值将赋给第四个成员变量。

声明结构体时需要牢记的一些要点如下：

- 结构体声明中的右花括号后必须跟一个分号
- 结构体类型声明不会告诉编译器任何有关内存分配的信息；它只是创建结构体
- 通常，结构体声明要先于程序中任何其他声明

接下来，让我们学习如何访问结构体的元素。

### 访问结构体元素

结构体的各个元素可以借助点运算符（.）访问。访问结构体成员的通用格式如下：

```c
variable.member;
```

在上述格式中，variable 指结构体类型变量的名称，member 表示结构体内部成员的名称。点运算符的结合性是从左到右。

清单 5.2 展示了如何存储和访问结构体的各个元素：

清单 5.2：存储和访问结构体中的各个元素

```c
#include<stdio.h>

struct Car             /* Declaring the structure */
{
    char name[50];
    char model[50];
    float price;
    int mfdate;
    int mileage;
};

struct Car varA;   /* Declaring structure type variables */

int main()
{
    int i;
    printf("\n Enter Name of the Car -> ");
    gets(varA.name);
    printf("\n Enter Model of the Car -> ");
    gets(varA.model);
    printf("\n Enter Price of the Car -> ");
    scanf("%f",&varA.price);
    printf("\n Enter Manufacturing Date of the Car -> ");
    scanf("%d",&varA.mfdate);
    printf("\n Enter Mileage of the Car -> ");
    scanf("%d",&varA.mileage);

    printf("\n Details Entered are \n");
    printf("\n Name of the Car -> %s",varA.name);
    printf("\n Address of Name of the Car -> %d",&varA.name);
    printf("\n Model of the Car -> %s",varA.model);
    printf("\n Address of Model of the Car -> %d",&varA.model);
    printf("\n Price of the Car -> %f",varA.price);
    printf("\n Address of Price of the Car -> %d",&varA.price);
    printf("\n Manufacturing Date of the Car -> %d",varA.mfdate);
    printf("\n Address of Manufacturing Date of the Car -> %d",&varA.mfdate);
    printf("\n Mileage of the Car -> %d",varA.mileage);
    printf("\n Address of Mileage of the Car -> %d",&varA.mileage);

    getch();
    return 0;
}
```

在清单 5.2 中，请注意，结构体的所有成员都是借助点运算符访问的。我们定义了一个名为 Car 的结构体。该结构体包含汽车的某些属性。结构体中提到的所有属性都被称为该结构体的成员变量。定义结构体之后，我们声明了一个名为 varA 的变量，其类型为 Car。在 main() 函数中，我们使用同一个结构体变量和点运算符访问了结构体的每个元素。上述程序的输出如下：

```
Enter Name of the Car -> MAHINDRA
Enter Model of the Car -> SCORPIO
Enter Price of the Car -> 900000
Enter Manufacturing Date of the Car -> 2008
Enter Mileage of the Car -> 12

Details Entered are

Name of the Car -> MAHINDRA
Address of Name of the Car -> 4210784
Model of the Car -> SCORPIO
Address of Model of the Car -> 4210834
Price of the Car -> 900000.000000
Address of Price of the Car -> 4210884
Manufacturing Date of the Car -> 2008
Address of Manufacturing Date of the Car -> 4210888
Mileage of the Car -> 12
Address of Mileage of the Car -> 4210892
```

