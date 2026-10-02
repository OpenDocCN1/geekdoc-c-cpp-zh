
## 归并排序实现

```c
printf("%d", List[i]);

}

}

void mergeSort(int List[], int lb, int ub) {

    int mid;

    if (lb < ub) {

        mid = (lb + ub)/2;

        mergeSort(List, lb, mid);

        mergeSort(List, mid + 1, ub);

        merge(List, lb, mid, ub);

    }

}

void merge(int List[], int lb, int mid, int ub) {

    int i, j;

    int mergeList[20];

    int ptr1, ptr2, ptr3;

    ptr1 = lb;

    ptr2 = mid;

    ptr3 = lb;

    while (ptr1 < mid && ptr2 <= ub) {

      if (List[ptr1] <= List[ptr2]) {

        mergeList[ptr3] = List[ptr1];

        ptr1++;

        ptr3++;

      }

      else {

        mergeList[ptr3] = List[ptr2];

        ptr2++;

        ptr3++;

      }

    }

    while (ptr1 < mid) {

      mergeList[ptr3] = List[ptr1];

      ptr1++;

      ptr3++;

    }

    while (ptr2 <= ub) {

      mergeList[ptr3] = List[ptr2];

      ptr2++;

      ptr3++;

    }

    for (i = lb; i < ptr3; i++) {

      List[i] = mergeList[i];

    }

}
```

## 6.52 数组、指针与字符串

| 8 | 5 | 6 | 9 | 4 | 19 | 7 | 2 |
|---|---|---|---|---|---|---|---|
| 8 | 5 | 6 | 2 | 4 | 7 | 19 | 9 |

小于基准值 | 大于基准值

| 8 | 5 | 6 | 2 | 4 | 7 | 19 | 9 |
|---|---|---|---|---|---|---|---|
| 7 | 5 | 6 | 2 | 4 | 8 | 19 | 9 |

小于基准值 | 大于基准值

**图 6.29 |** 快速排序

快速排序的算法如下：
在此算法中，存储在名为 `list[N]` 数组中的列表元素按升序排序。该算法包含两个部分——`quickSort` 和 `partition`。`partition` 算法围绕基准值（pivot）将其分为两个子列表。`quickSort` 算法接收一个列表并将其存储在名为 `list[N]` 的数组中。它使用两个变量 `lb` 和 `ub` 来跟踪列表或子列表的下限和上限。它采用 `partition` 算法对子列表进行排序。

```
Algorithm quickSort()

  Step

  1. lb = 0; /*设置下界 */

  2. ub = N - 1; /*设置上界 */

  3. pivot = List[lb];

  4. lb++;

  5. partition(pivot, lb, ub);
```

```
Algorithm partition (pivot, List, lb, ub)

  Step

  1. i = lb;

  2. j = ub;

  while (i<j)

    {

      /*从 lb 开始遍历列表直到找到大于基准值的元素 */

      3. while (List[i] <= pivot) i++;

      /* 从 ub 开始遍历列表直到找到小于基准值的元素 */
      3.2 while (List[j] > pivot) j--;
      3.3 if (i < j) /* 交换元素 */

      {

          temp = List[i];

          List[i] = List[j];

          List[j] = temp;

      }

    }

  4. temp = List[j]; /* 将基准值置于子列表中间 */
  5. List[j] = List[ub - 1];
  6. List[lb - 1] = temp;
  7. if (j > lb) quicksort(List, lb, j - 1); /* 排序左子列表 */
  8. if (j < ub) quicksort(List, j + 1, ub); /* 排序右子列表 */
```

**示例 7**: 给定一个包含 N 个随机数字的列表。编写一个程序使用快速排序将列表按升序排序。

**解答**: 所需程序同时使用了两种算法——`quickSort()` 和 `partition()`。在程序中，使用了一个名为 `Key` 的变量作为基准值。

```
/* 此程序使用快速排序按升序对数字列表 */

#include <stdio.h>

#include <conio.h>

#define N 20

void partition(int Key, int List[], int lb, int ub);

void quicksort(int List[], int lb, int ub);

void main()

{

    int List[N];

    int i, size, Pos, temp;

    int lb, ub;

    printf("\nEnter列表的大小 (<%d):\n", N);

    scanf("%d", &size);

    printf("\n逐一输入列表:\n");

    for (i = 0; i < size; i++)

    {

        scanf("%d", &List[i]);

    }

    /* 使用快速排序对列表 */

    quicksort(List, 0, size - 1);

    /* 打印排序后的列表 */

    printf("\n排序后的列表为 ....n");

    for (i = 0; i < size; i++)

    {

        printf("%d ", List[i]);

    }

}
```

## 6.54 数组、指针与字符串

```
}

void quicksort(int List[], int lb, int ub) {

    int Key; /* 基准值 */

    Key = List[lb]; lb++;

    partition(Key, List, lb, ub);

}

void partition(int Key, int List[], int lb, int ub) {

    int i, j, temp;

    i = lb;

    j = ub;

    while (i<=j) {

        while (List[i] <= Key) i++;

        while (List[j] > Key) j--;

        printf("ni=%d, j=%d\n", i, j);

        getch();

        if (i<=j) {

            temp = List[i];

            List[i] = List[j];

            List[j] = temp;

        }

    }

    temp = List[j];

    List[j] = List[lb-1];

    if (j > lb) quicksort(List, lb, j, j-1);

    if (j < ub) quicksort(List, j+1, ub);

}
```

## 6.4.6 壳排序

它是插入排序的改进。给定一个 `List[N]` 列表，将其分为 k 组，每组包含 N/k 个元素。k 的值假设为 {1, 3, 5...}。因此第 i 个组将包含以下元素：`List[i]`, `List[i+2k]` ...。考虑图 30 所示的列表。对于 k = 5，列表被分为若干组：
组 0 = 8, 7
组 1 = 5, 19
组 2 = 6, 3
组 3 = 2
组 4 = 4

| 8 | 5 | 6 | 2 | 4 | 7 | 19 | 3 |
|---|---|---|---|---|---|---|---|
**图 30 | k = 5 时的列表** |

| 7 | 5 | 3 | 2 | 4 | 8 | 19 | 6 |
|---|---|---|---|---|---|---|---|
**图 31 | 第一轮后的列表** |

现在对每个组应用插入排序，得到图 31 所示的结果。对于 k = 3，列表被分为若干组：
组 0 = 7, 2, 19
组 1 = 5, 4, 6
组 2 = 3, 8

现在对每个组应用插入排序，得到图 32 所示的结果。对于 k = 1，列表被分为若干组：
组 0 = 2, 4, 3, 7, 5, 8, 19, 6。

| 2 | 4 | 3 | 7 | 5 | 8 | 19 | 6 |
|---|---|---|---|---|---|---|---|
**图 32 | 第二轮后的列表** | 

| 2 | 3 | 4 | 5 | 6 | 7 | 8 | 19 |
|---|---|---|---|---|---|---|---|
**图 33 | 第三轮后的列表** | 

可以注意到，在第三轮之后，列表已经完成排序。由于变量 k 取值为 5, 3, 和 1；壳排序也被称为**递减排序**。

壳排序的算法如下。在此算法中，存储在数组 `list[N]` 中的元素列表按升序排序。算法根据上述描述将列表分为组。递减组值存储在名为 `dimStep` 的列表中。使用变量 `s` 将插入操作移动到下一个组。变量 `k` 从 `dimStep` 获取步长，并将组内的索引从一个移动到另一个。

```
Algorithm shellSort()

{

  Step

  1. 初始化 dimStep 为 1,3,5....

   /* 使用壳排序对列表 */

  2. for (step = 0; step < 3; step++)

  {

   2.1 k = dimStep[step]; /* 递减步长 */

   2.2 s = O; /* 从列表末尾开始 */

   2.3 for (i = s + k; i<size; i = k)

   {

     temp = List[i]; /* 保存组中的元素 */

     j = i - k;

     /* 寻找插入位置 */

     while ((temp < List[j]) && (j >= 0))

     {

       List[j] = List[j];

       j = j - k;

     }

     List[j] = temp; /* 将保存的元素插入位置 */

     s++; /* 进入下一步 */

   }

  }

  3. 打印排序后的列表

  4. 停止

}
```

**示例 8**: 给定一个包含 N 个随机数字的列表。编写一个程序使用壳排序将列表按升序排序。

**解答**: 所需程序使用了 `shellSort()` 算法。

```
/* 此程序使用壳排序按升序给出数字列表 */

#include <stdio.h>

#define N 20

void main()

{

   int List[N];

   int size;

   int i, j, k, step;

   int temp, s;

   int dimStep[] = {5,3,1}; /* 递减步长 */

   printf("\n输入列表的大小 (<20)");

   scanf("%d", &size);

   printf("\n逐一输入列表:");

   for (i = 0; i<size; i++)

   {

     scanf("%d", &List[i]);

   }

}
```

## 6.14.7 基数排序

壳排序的分析超出了本书的范围。

这是一种适用于整数排序的非比较型算法。它按数字对元素进行排序。它从元素的最低有效位开始排序。这个部分有序的列表随后根据次低有效位进行排序，依此类推。

注意：该算法适合通过链表实现。因此，基数排序目前被推迟，将在书后部分讨论。

## 6.15 总结

1. 数组用于存储同质数据，即相同类型的数据。
2. 数组的所有元素具有相同的名称，即数组名。它们根据其在数组中的位置进行区分。位置通过使用称为索引或下标的整数值值来指定。
3. C 语言中的数组索引从 `[` 开始。
4. C 语言不提供数组越界检查。
5. 数组存储在连续（即交叉）的内存位置上。

## 6.58 数组、指针与字符串

7. 数组被分为一维数组和多维数组。
8. 下标运算符用于访问数组的元素。
9. 数组名是指数组第一个元素的地址，并且是一个常量对象。
10. 数组不能与另一个数组相等或初始化。
11. 如果一个数组与另一个数组相等，其求值始终为假（false）。
12. 指针是一个存储变量或函数地址的变量。
13. 指针上可以应用受限算术。指针的算术受指针算术的支配。
14. 不允许两个指针相加、指针加浮点数或双精度数，也不允许对指针使用乘法和除法运算符。
15. `void` 指针是一种通用指针，可以指向任何类型的对象。
16. 不允许对指针进行解引用并对其应用指针算术。
17. 空指针是一个特殊的指针，它不指向任何地方。
18. 解引用空指针会导致运行时错误。
19. n 维数组是 (n-1) 维数组的数组。
20. 形式为 `E[i][j]` 的表达式被隐式转换为形式为 `*(E+i)+j` 的表达式。

# 练习题

## 概念性问题与解答

### 1. 什么是指针？它在哪里使用？
指针是一个存储另一个对象地址的对象。指针用于间接操作操纵它所指向的对象的值。

### 2. 我知道 C 语言中的基本数据类型，但什么是指针类型？
除了基本数据类型外，C 语言允许从基本数据类型派生类型。这些被称为衍生数据类型。指针类型是派生数据类型之一。

### 3. 下述代码的输出是什么？

```c
{
int *a;
float *b;
char *c;
printf("%d %d %d ", sizeof(a),sizeof(b),sizeof(c));
}
```

给定代码的输出取决于执行环境和编译器。如果使用 DOS 的 Borland TC 3.0 编译器执行，输出为 2 2 2。如果使用 Windows 的 Borland TC 4.5 编译器或 Microsoft VC++6.0 编译器执行，输出为 4 4 4。

这里需要注意的一点是，所有指针在内存中占用 2 或 4 字节（取决于执行环境和使用的编译器），无论它们是 `int`、`float`、`char` 还是其他数据类型的指针。不同数据类型指针之间的区别既不在于指针的表示，也不在于它们的值。区别在于所指向对象的类型。

### 4. 为什么下面的代码在使用 DOS 的 Borland TC 3.0 编译器执行时输出为 21 而不是 22，而在使用 Windows 的 Borland TC 4.5 编译器或 Microsoft VC++ 6.0 编译器执行时输出 41 而不是 44？

```c
main()
{
    char *a, *b;
    printf("%d.%d", sizeof(a),sizeof(b));
}
```

该代码实际上给出了正确的输出。与指针声明相关的语法规定：“*指针通过在标识符前加标点符号来声明*”。在逗号分隔的声明列表中，“标点符号必须位于每个旨在作为指针的标识符之前”。

因此，在声明语句 `char *a, *b` 中，`a` 被声明为指向 `char` 类型对象的“指针”，而 `b` 被声明为 `char` 类型“数据对象”，而不是指针。

### 5. 位按与运算符 (&) 和乘法运算符 (*) 是二元运算符。在接下来的代码中，这些运算符仅与一个操作数使用。尽管如此，代码仍然成功编译。这怎么可能？

```c
main()
{
    int a=10, b=20;
    int *ptr;
    ptr=a;
    printf("The object to which ptr points has value %d",ptr);
    ptr=b;
    printf("The object to which ptr points now has value %d",ptr);
}
```
