
The contents of the variable `value`: 5234

The address of the pointer `ptrvalue1`: 20000

The contents of the pointer `ptrvalue1`: 10000

The address of the pointer `ptrvalue2`: 30000

The contents of the pointer `ptrvalue2`: 20000

The address of the pointer `ptrvalue3`: 40000

The contents of the pointer `ptrvalue3`: 30000

变量 `value` 中存储的整数 5234 可以通过指针 `ptrvalue1`、`ptrvalue2` 或 `ptrvalue3` 访问。以下语句显示了变量的地址和值。

```
printf("The address of the variable value: %u", &value);

printf("The contents of the variable value: %d", value);

printf("The address of the pointer ptrvalue1: %u", &ptrvalue1);

printf("The contents of the pointer ptrvalue1: %d", *ptrvalue1);

printf("The address of the pointer ptrvalue2: %u", &ptrvalue2);

printf("The contents of the pointer ptrvalue2: %d", **ptrvalue2);

printf("The address of the pointer ptrvalue3: %u", &ptrvalue3);

printf("The contents of the pointer ptrvalue3: %d", ***ptrvalue3);
```

（注：由于原文文本中存在部分重复的输出块，翻译时已根据逻辑进行了对齐，确保了所有内容的完整性。）

### 10.1.3 复习题

1. 判断以下陈述对错：
   a. 指针变量必须被其数据类型赋值。
   b. 指针包含一个符号整数的存储。
   c. 将变量赋值给指针时必须使用地址运算符。
   d. 要通过指针访问变量的内容，必须先为指针赋值变量地址，然后对其进行解引用。
   e. 指针变量没有自己的类型。
   f. 指针变量必须是一个无符号整数。

2. 以下代码段打印了什么？
   a.
```c
int x;
int *ptrx;
ptrx = &x;
x = 3950;
printf("%u\n", ptrx);
printf("%d\n", x);
printf("%d\n", *ptrx);
```
   b.
```c
int x;
int *ptr1, **ptr2;
ptr1 = &x;
ptr2 = &ptr1;
x = 8550;
printf("%u\n", ptr1);
printf("%d\n", x);
printf("%d\n", *ptr1);
printf("%d\n", **ptr2);
```

## 10.2 指针算术运算

指针算术运算必须小心进行。变量的值可以通过指针 `ptrvalue1`、`ptrvalue2` 或 `ptrvalue3` 访问。以下语句显示了程序员必须防止访问非法内存。计算机具有保护机制以防止未经授权的。

### 10.2.1 指针算术运算

指针算术运算必须小心进行。变量的值可以通过指针 `ptrvalue1`、`ptrvalue2` 或 `ptrvalue3` 访问。以下语句显示了程序员必须防止访问非法内存。计算机具有保护机制以防止未经授权的。

### 10.2.2 指针的解引用

数组名 `arr` 的值已经是一个地址，因此作为右值，它可以直接存储在 `ptrarr` 中而不需要地址运算符 `&`。此时数组名和指针都拥有数组地址。区别在于数组名是一个常量，不能更改，而指针变量的值是数组地址，它不需要解引用，但可以像使用数组名一样使用它。

```c
int arr[5];
int *ptrarr;
ptrarr = arr; /* 将 arr 的地址赋值给 ptrarr */
arr[2] = 7;
或者 ptrarr[2] = 7;
```

当指针变量被替代普通变量使用时，必须对其解引用。例如：

```
int x;
int *ptr;
```

```
... = x;               or ... = *ptr;
x = ...               or *ptr = ...
```

```
printf("%d", x);   or printf("%d", *ptr);
func(x);            or func(*ptr); // 按值传递
```

当指针变量用在普通变量需要使用地址运算符 "&" 的语文中时，不需要对其解引用。例如：

```
int x;
int *ptr;
```

```
scanf("%d", &x);   or scanf("%d", *ptr);
...ptr = &x;               or ...ptr = ptr;
```

当指针变量指向数组时，也会进行解引用，但它们像数组名一样进行下标运算或数组算术，例如：

```c
int arr[10];
int *ptr;
```

```
arr[6] = ...    or ptr[6] = ...;
... = arr[6];           or ... = ptr[6];
```

### 10.2.3 复习题

- 1. 判断以下陈述的对错。
   a. 指针变量不能被赋予标量常量。
   b. 指针变量可以与另一个指针变量相。
   c. 指针变量可以从另一个指针变量中减。
   d. 指针变量可以改变数组的地址。
   e. 两个指针变量可以指向同一个变量。
2. 编写代码来证明或反驳第1题中的陈述。

## 10.3 指针与数组

由于数组名是一个地址常量，因此数组名可以作为数组指针来访问数组。一旦知道了数组的起始地址，那么通过指针变量顺序访问和操作数组元素就变得相对简单。这对于存储在一维和多维数组中的数值和字符数据都是如此的。

### 10.3.1 一维数组

数组名是一个地址常量，如下所示。数组名可以赋值给指针变量，可以使用指针变量顺序或随机地访问数组元素。以下代码显示了数组 `ar` 的声明、数组指针 `ptrtr` 的声明以及将数组名赋值给指针变量 `ptrtr = ar`。

```
int ar[10];
int *ptr;
```

```
ptrtr = ar;
```

假设数组的地址为 1000，存储分配如下：

| ar[0] | 1000 | 数组的地址是 |
| ar[1] | 1004 | ar 的值 |
| ar[2] | 1008 | |
| ar[3] | 1012 | |
| ar[4] | 1016 | |
| ar[5] | 1020 | |
| ar[6] | 1024 | |
| ar[7] | 1028 | |
| ar[8] | 1032 | |
| ar[9] | 1036 | |

注意，数组第一个元素的地址从字节位置 1000 开始，其他每个元素的地址都高出四个字节。所示示例中其他元素的地址如下：

```
ar + 0 or ptrtr + 0 is 1000      or &ar[0] is 1000
ar + 1 or ptrtr + 1 is 1004      &ar[1] is 1004
ar + 2 or ptrtr + 2 is 1008      &ar[2] is 1008
ar + 3 or ptrtr + 3 is 1012      &ar[3] is 1012
ar + 4 or ptrtr + 4 is 1016      &ar[4] is 1016
ar + 5 or ptrtr + 5 is 1020      &ar[5] is 1020
ar + 6 or ptrtr + 6 is 1024      &ar[6] is 1024
ar + 7 or ptrtr + 7 is 1028      &ar[7] is 1028
ar + 8 or ptrtr + 8 is 1032      &ar[8] is 1032
ar + 9 or ptrtr + 9 is 1036      &ar[9] is 1036
```

如果数组名递增1，地址将按每个元素单元的大小递增。注意地址增加了四个字节，是因为对于 `int` 数据类型，每个单元被分配了四个字节的存储。每种数据类型的单元大小增如下：

| 数据类型 | 单元大小 |
| --- | --- |
| int | 4 字节 short int 或 short 是 2 字节 |
| float | 4 字节 |
| double | 8 字节 |
| char | 1 字节 |

以下代码和输出显示了数组 `ar` 的地址。

```c
#include <stdio.h>
int main() {
    int ar[10];
    int *aptr;
    aptr = ar;
    printf("Address using the array name: %u\n", ar);
    printf("Address of the first element: %u\n", &ar[0]);
    printf("Address using the pointer variable: %u\n", aptr);
    return 0;
}
```

输出如下：

Address using the array name: 1000
Address of the first element: 1000
Address using the pointer variable: 1000

## 指针与动态存储

注意 `ar` 是数组的名字，由于它是常量，不能被改变。数组名可以存储在指向数组数据类型的指针变量 `aprtr` 中。可以通过递增或递减指针变量来访问数组。

以下代码和输出显示了数组 `ar` 第一个元素的值。

```c
ar[0] = 57;
aprtr = ar;
printf("value using the array name: %d\n", ptrtr[0]);
```

两种情况下输出均为57。

以下代码和输出显示了数组 `ar` 最后一个元素的值。

两种情况下输出均为 -43。

### 使用数组指针输入输出

以下示例显示了 `int` 类型使用地址算术进行输入输出。数组名作为地址常量，本身就是一个指针，可以用于向数组输入数据。每个数组指针必须解引用才能输出数组。

### 整数的输入输出

使用数组名 `ar` 的整数存储如下：

| 索引 | 值 |
|---|---|
| ar + 0 | 45 |
| ar + 1 | 56 |
| ar + 2 | 76 |
| ar + 3 | 93 |
| ar + 4 | 15 |

![](img/8356e6c3bfe3b10354682c60b1e74b1d_647_0.png)

## 标准输入输出

```c
#include <stdio.h>
int main() {
    int ar[10];
    int *aptr;
    aptr = ar;
    for(int i=0; i<5; i++) {
        scanf("%d", &aptr[i]);
    }
    for(int i=0; i<5; i++) {
        printf("%d ", ar[i]);
    }
    return 0;
}
```

```c
bptr--;
}
  return 0;
```

# 之前

| a[0] | 12.75 | b[0] | uuuuuuu |
| a[1] | 18.34 | b[1] | uuuuuuu |
| a[2] | 9.85 | b[2] | uuuuuuu |
| a[3] | 23.78 | b[3] | uuuuuuu |
| a[4] | 16.96 | b[4] | uuuuuuu |

# 之后

| a + 0 | 12.75 | b + 0 | 16.96 |
| a + 1 | 18.34 | b + 1 | 23.78 |
| a + 2 | 9.85 | b + 2 | 9.85 |
| a + 3 | 23.78 | b + 3 | 18.34 |
| a + 4 | 16.96 | b + 4 | 12.75 |

注意数组 a 的元素是逆序复制到数组 b 中的。

使用数组偏移进行算术运算

可以使用数组偏移执行加法、乘法和除法等算术操作。以下程序代码展示了使用数组偏移的加法操作。

```c
#include <stdio.h>
int main() {
  int ar[5] = {5, 8, 4, 6, 12};
  int br[5] = {4, 9, 2, 3, 15};
  int i, cr[5];
  for (i = 0; i < 5; i++) {
    *(cr + i) = *(ar + i) + *(br + i);
  }
  printf("The elements of array cr are: %s");
  for (i = 0; i < 5; i++) {
    printf("%d ", *(cr+i));
  }
}
return 0;
}
```

输出如下：

The elements of array cr are: 9  17  6  9  27

注意数组的元素是逐个与数组 br 的元素相加的，结果存储在数组 cr 中。同样，可以使用数组偏移执行其他算术操作。

# 10.3.2 递增和递减操作

指针的递增和递减操作用于处理数值数组和字符串数组，无需使用下标。指向一维和多维数组的数组指针可以通过递增来从数组开始顺序访问元素。通过从数组末尾将数组指针减1，可以从数组末尾顺序访问元素。递增和递减操作在第二章中介绍。以下代码展示了字符串指针的递增操作。

```c
#include <stdio.h>
int main()
{
    char str[10] = "ELECTRON";
    char *strptr;
    int i;
    strptr = str;
    for(i = 0; i < 8; i++)
    {
        printf("%c ", strptr);
        strptr++;
    }
    return 0;
}
```

输出如下：

ELECTRON

注意，数组名 strname 不能像使用 strptr 那样的方式来扫描数组，因为数组名是一个常量，不能更改。

> **程序警告：** 如果将数组名赋值给指针变量，并对该指针进行递增，它将不再指向数组的开头；指针必须重置为指向数组的开头。

# 10.3.3 二维数组

二维数组按行存储在连续的内存位置中。数组在内存中起始的内存位置作为其值存储在数组名中。

可以使用偏移配合数组名处理二维数组。以下示例展示了数组偏移和数组的存储情况。

假设数组地址从位置 1000 开始。由于 `int` 数据类型分配了4字节的单元大小，元素的地址增加了4。如果有四列，则行的地址增加了 16，因为每行的四个元素需要 16 字节的存储空间。第一行的地址是 a + 0，第二行的地址是 a + 1，第三行的地址是 a + 2。对应这些行的地址分别为 1000、1016 和 1032。

| 索引 | 地址 | 行地址 |
| :--- | :--- | :--- |
| 数组指针 | a[0][0] | 1000 | a + 0 |
| | a[0][1] | 1004 |
| | a[0][2] | 1008 |
| | a[0][3] | 1012 |
| | a[1][0] | 1016 | a + 1 |
| | a[1][1] | 1020 |
| | a[1][2] | 1024 |
| | a[1][3] | 1028 |
| | a[2][0] | 1032 | a + 2 |
| | a[2][1] | 1036 |
| | a[2][2] | 1040 |
| | a[2][3] | 1044 |

第一行的地址是 a + 0，即 1000。第 0 行元素的地址如下：

*(a + 0) + 0 1000
*(a + 0) + 1 1004
*(a + 0) + 2 1008
*(a + 0) + 3 1012

第 1 行元素的地址如下：

*(a + 1) + 0 1016
*(a + 1) + 1 1020
*(a + 1) + 2 1024
*(a + 1) + 3 1028

第 2 行元素的地址如下：

*(a + 2) + 0 1032
*(a + 2) + 1 1036
*(a + 2) + 2 1040
*(a + 2) + 3 1044

注意行地址表示行的起始。要获取行元素的地址，必须对行地址进行引用并加上偏移量。使用行地址和列偏移访问数组内容，必须进行引用。以下示例展示了二维数组的引用。

第 0 行元素的内容如下：

*(a + 0) + 0
*(a + 0) + 1
*(a + 0) + 2
*(a + 0) + 3

第 1 行元素的内容如下：

*(a + 1) + 0
*(a + 1) + 1
*(a + 1) + 2
*(a + 1) + 3

# 636 指针与动态存储

第 2 行元素的内容如下：

```c
*(a + 2) + 0
*(a + 2) + 1
*(a + 2) + 2
*(a + 2) + 3
```
