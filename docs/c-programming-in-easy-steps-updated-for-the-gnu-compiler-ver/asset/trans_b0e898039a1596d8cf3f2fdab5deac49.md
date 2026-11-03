
## 指向结构体

指向结构体数据类型的指针可以像指向常规数据类型的指针一样创建。在这种情况下，指针保存用于存储成员数据的内存区域的起始地址。

在 C 程序中使用指向结构体的指针非常普遍，因此甚至有一个专门的操作符来描述它。在结构体指针中，“.”点操作符可以被 "->" 替换，后者是一个连字符后跟大于号操作符。这种组合被称为箭头操作符。例如，指向结构体成员的指针 ptr->member 等价于 (*ptr).member。

![](img/d1dfb0563339ba187decb78799155b7f_131_0.png)

- 1. 使用预处理器指令包含标准输入/输出库函数开始一个新程序

```c
#include <stdio.h>
```

- 2. 接下来，声明一个未命名的结构体，定义一个包含两个字符指针成员和一个标签名的数据类型

```c
typedef struct {
  char *name; char *popn ;
} City ;
```

- 3. 现在，添加一个 main 函数，声明三个常规变量和一个指针变量，全部为结构体数据类型

```c
int main()
{
  City ny , la , ch , *ptr ;
}
```

- 4. 在 main 函数块内，为第一个变量的成员赋值然后显示存储的值，使用点操作符同时存储和检索值

```c
ny.name = "New York City" ;
ny.popn = "8,274,527" ;
printf( "\n%s , Population: %s\n", ny.name , ny.popn ) ;
```

- 5. 将第二个变量的地址赋给指针变量

```c
ptr = &la ;
```

![](img/d1dfb0563339ba187decb78799155b7f_131_1.png)

箭头操作符在 C 编程中很有用，可用于区分结构体指针和其他指针。

- 6. 现在，为第二个变量的成员赋值，然后显示存储的值，使用箭头操作符存储值并使用点操作符检索值

```c
ptr->name = "Los Angeles";
ptr->popn = "3,834,340";
printf( "\n%s, Population: %s\n" , la.name, la.popn );
```

- 7. 接下来，将第三个变量的地址赋给指针变量

```c
ptr = &ch ;
```

- 8. 现在，为第三个变量的成员赋值，然后显示存储的值，使用箭头操作符同时存储和检索值

```c
ptr->name = "Chicago";
ptr->popn = "2,836,658";
printf( "\n%s, Population: %s\n" , ptr->name, ptr->popn );
```

- 9. 在 main 函数块结束时，返回零整数值，如函数声明所要求

```c
return 0;
```

- 10. 保存程序文件，然后编译并执行程序以查看结构体成员中存储的值

本示例中的人口值被指定为字符串以保留逗号分隔。

![](img/d1dfb0563339ba187decb78799155b7f_132_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_132_1.png)

## 向函数传递结构体

结构体成员值可以像任何其他数据类型的数值一样存储在数组中。数组按通常方式声明，但为其元素赋值的方法略有不同。每个由逗号分隔的成员值列表必须用一对大括号括起来。

同样，结构体可以像任何其他变量一样作为参数传递给函数。结构体的 数据类型必须在函数原型声明及其定义中同时指定，并附带一个变量名，以便函数寻址其成员值。

但请记住，按值传递，仅使用常规变量，意味着函数将对结构体的副本进行操作——其原始成员值将保持不变。另一方面，按引用传递结构体，使用指针变量，意味着函数将对原始结构体成员进行操作——因此原始成员值将被更改。

![](img/d1dfb0563339ba187decb78799155b7f_133_0.png)

> 简单地将所有值作为逗号分隔列表赋值是无效的——每组值必须用自己的大括号对括起来。

![](img/d1dfb0563339ba187decb78799155b7f_133_1.png)

- 1. 使用预处理器指令包含标准输入/输出库函数开始一个新程序

```c
#include <stdio.h>
```

- 2. 接下来，声明一个未命名的结构体，定义一个包含两个成员和一个标签名的数据类型

```c
typedef struct
{
  char *name ;
  int quantity ;
} Item ;
```

- 3. 现在，声明一个结构体数据类型的数组，初始化三个结构体的每个成员

```c
Item fruits[3] =
{ { "Apple", 10 }, { "Orange", 20 }, { "Pear", 30 } };
```

- 4. 添加一个函数原型，该原型将传递一个结构体变量和一个指向结构体的指针变量作为参数

```c
void display( Item val , Item *ref );
```

## 联合中的分组

在 C 编程中，“union”允许在程序进行时将不同类型、任意数据类型的不同数据片段存储在同一内存位置——为联合赋值会覆盖之前存储在其中的内容。这允许高效使用内存。

联合类似于结构体，但使用 union 关键字声明，并且由于其特性，其成员只能在程序进行时单独赋予值。

联合数组可以像前一个示例中创建结构体数组的方式一样创建，但联合成员只能在声明时初始化，如果它们全部是相同的数据类型。指向联合的指针可以以与指向结构体的指针完全相同的方式创建，并且联合可以像任何其他变量一样传递给函数。

![](img/d1dfb0563339ba187decb78799155b7f_135_0.png)

- 1. 使用预处理器指令包含标准输入/输出库函数开始一个新程序

```c
#include <stdio.h>
```

- 2. 接下来，声明一个未命名的结构体，定义一个包含三个成员和一个标签名的数据类型

```c
typedef struct { int num ; char ltr , *str } Distinct ;
```

- 3. 现在，声明一个未命名的联合，定义一个包含三个成员和一个标签名的数据类型

```c
typedef union { int num ; char ltr , *str ; } Unified ;
```

- 4. 添加一个 main 函数，声明结构体数据类型的变量并初始化其每个成员

```c
int main()
{
Distinct sdata = { 10 , 'C' , "Program" } ;
}
```

- 5. 现在，在 main 函数块中，声明联合数据类型的变量

```c
Unified udata ;
```

![](img/d1dfb0563339ba187decb78799155b7f_135_1.png)

> 程序员有责任了解在程序执行过程中的任何时刻联合中存储的是哪种类型的数据。

- 6. 在变量声明之后，输出每个结构体成员的值和内存地址

```c
printf("\nStructure:\nNumber: %d", sdata.num );
printf("\tStored at: %p\n", &sdata.num );
printf("Letter: %c", sdata.ltr );
printf("\tStored at: %p\n", &sdata.ltr );
printf("String: %s", sdata.str );
printf("\tStored at: %p\n", &sdata.str );
```

![](img/d1dfb0563339ba187decb78799155b7f_136_0.png)

- 7. 现在，为第一个联合成员赋值然后输出其值和内存地址

```c
udata.num = 16 ;
printf( "\nUnion:\nNumber: %d" , udata.num );
printf( "\tStored at: %p\n" , &udata.num );
```

- 8. 接下来，为第二个联合成员赋值然后输出其值和内存地址

```c
udata.ltr = 'A' ;
printf( "Letter: %c" , udata.ltr );
printf( "\tStored at: %p\n" , &udata.ltr );
```

- 9. 最后，为第三个联合成员赋值然后输出其值和内存地址

```c
udata.str = "Union" ;
printf( "String: %s" , udata.str );
printf( "\tStored at: %p\n" , &udata.str );
```

- 10. 在 main 函数块结束时，返回零整数值，如函数声明所要求

```c
return 0 ;
```

- 11. 保存程序文件，然后编译并执行程序以查看结构体和联合成员中存储的值以及它们存储的地址

```text
C:\MyPrograms>gcc union.c -o union.exe
C:\MyPrograms>union
Structure:
Number: 10    Stored at: 0061FF24
Letter: C     Stored at: 0061FF28
String: Program Stored at: 0061FF2C

Union:
Number: 16    Stored at: 0061FF20
Letter: A     Stored at: 0061FF20
String: Union Stored at: 0061FF20
```
