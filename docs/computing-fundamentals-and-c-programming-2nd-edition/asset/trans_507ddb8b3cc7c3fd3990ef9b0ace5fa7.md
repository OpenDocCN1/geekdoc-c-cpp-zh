

- 当数组作为参数传递给函数时，实际传递的是指针。在函数头中，我们必须以适当的大小声明此类数组，但第一个数组大小除外，它是可选的。LO 13.5
- 如果我们希望被调用函数改变调用函数中某个变量的值，就必须将该变量的地址传递给被调用函数。LO 13.6
- 当按地址传递参数时，相应的形式参数必须是指针变量。LO 13.6
- 在没有强制类型转换的情况下，将一种类型的指针赋给另一种类型的指针是错误的（void 指针除外）。LO 13.6

## 需要记住的关键术语

- **内存：** 它是存储单元的连续集合，每个单元都有一个与之关联的地址值。LO 13.1
- **指针：** 它用于将内存地址存储为值。LO 13.1
- **指针变量：** 它是存储另一个变量内存地址的变量。LO 13.2
- **按引用调用：** 它是使用指针传递变量地址来调用函数的过程。LO 13.6
- **按值调用：** 它是传递变量实际值的过程。LO 13.6

## 简要案例

### 1. 考试成绩处理 [LO 13.2, 13.5, 13.6 H]

一批学生在年度考试中获得的分数如下表所示：

| 学生姓名 | 所得分数 |
| --- | --- |
| S. Laxmi | 45 67 38 55 |
| V.S. Rao | 77 89 56 69 |
| ... | ... |

需要计算每个学生获得的总分，并基于总分打印排名表。

图 13.15 中的程序将学生姓名存储在数组 **name** 中，将分数存储在数组 **marks** 中。在计算完所有学生获得的总分后，程序生成并打印排名表。声明

```c
int marks[STUDENTS][SUBJECTS+1];
```

将 **marks** 定义为指向该数组第一行的指针。我们使用 **rowptr** 作为指向 **marks** 行的指针。**rowptr** 初始化如下：

```c
int (*rowptr)[SUBJECTS+1] = array;
```

注意，**array** 是形式参数，其值由实际参数 **marks** 的值替换。`*rowptr` 外面的括号使 **rowptr** 成为指向包含 **SUBJECTS+1** 个整数的数组的指针。请记住，语句

```c
int *rowptr[SUBJECTS+1];
```

会将 **rowptr** 声明为包含 **SUBJECTS+1** 个元素的数组。

当我们递增 **rowptr**（通过 **rowptr+1**）时，递增以 **array** 每一行的大小为单位进行，使 **rowptr** 指向下一行。由于 **rowptr** 指向特定行，**(*rowptr)[x]** 指向该行中的第 x 个元素。

### 程序

```c
#define STUDENTS   5
#define SUBJECTS   4
#include <string.h>

main()
{
    char name[STUDENTS][20];
    int marks[STUDENTS][SUBJECTS+1];

    printf("Input students names & their marks in four subjects\n");
    get_list(name, marks, STUDENTS, SUBJECTS);
    get_sum(marks, STUDENTS, SUBJECTS+1);
    printf("\n");
    print_list(name,marks,STUDENTS,SUBJECTS+1);
    get_rank_list(name, marks, STUDENTS, SUBJECTS+1);
    printf("\nRanked List\n\n");
    print_list(name,marks,STUDENTS,SUBJECTS+1);
}
    /* Input student name and marks       */
get_list(char *string[ ],
          int array [ ] [SUBJECTS +1], int m, int n)
{
    int  i, j, (*rowptr)[SUBJECTS+1] = array;
    for(i = 0; i < m; i++)
    {
        scanf("%s", string[i]);
        for(j = 0; j < SUBJECTS; j++)
            scanf("%d", &(*(rowptr + i))[j]);
    }
}
/* Compute total marks obtained by each student       */
get_sum(int array [ ] [SUBJECTS +1], int m, int n)
{
    int  i, j, (*rowptr)[SUBJECTS+1] = array;
    for(i = 0; i < m; i++)
    {
        (*(rowptr + i))[n-1] = 0;
        for(j = 0; j < n-1; j++)
            (*(rowptr + i))[n-1] += (*(rowptr + i))[j];
    }
}

/*  Prepare rank list based on total marks      */

get_rank_list(char *string [],
              int array [] [SUBJECTS + 1],
              int m,
              int n)
{
    int i, j, k, (*rowptr)[SUBJECTS+1] = array;
    char *temp;

    for(i = 1; i <= m-1; i++)
        for(j = 1; j <= m-i; j++)
            if( (*(rowptr + j-1))[n-1] < (*(rowptr + j))[n-1])
            {
                swap_string(string[j-1], string[j]);

                for(k = 0; k < n; k++)
                    swap_int(&(*(rowptr + j-1))[k], &(*(rowptr+j))[k]);
            }
}
/*          Print out the ranked list          */
print_list(char *string [],
           int array [] [SUBJECTS + 1],
           int m,
           int n)
{
    int i, j, (*rowptr)[SUBJECTS+1] = array;
    for(i = 0; i < m; i++)
    {
        printf("%-20s", string[i]);
        for(j = 0; j < n; j++)
            printf("%5d", (*(rowptr + i))[j]);
        printf("\n");
    }
}
/*      Exchange of integer values             */
swap_int(int *p, int *q)
{
    int temp;
    temp = *p;
    *p = *q;
    *q = temp;
}

/*      Exchange of strings             */
swap_string(char s1[ ], char s2[ ])
{
    char swaparea[256];
    int i;
    for(i = 0; i < 256; i++)
        swaparea[i] = '\0';
    i = 0;
    while(s1[i] != '\0' && i < 256)
    {
        swaparea[i] = s1[i];
        i++;
    }
    i = 0;
    while(s2[i] != '\0' && i < 256)
    {
        s1[i] = s2[i];
        s1[++i] = '\0';
    }
    i = 0;
    while(swaparea[i] != '\0')
    {
        s2[i] = swaparea[i];
        s2[++i] = '\0';
    }
}
```

### 输出

```text
Input students names & their marks in four subjects
S.Laxmi 45 67 38 55
V.S.Rao 77 89 56 69
A.Gupta 66 78 98 45
S.Mani 86 72 0 25
R.Daniel 44 55 66 77

S.Laxmi        45  67  38  55  205
V.S.Rao        77  89  56  69  291
A.Gupta        66  78  98  45  287
S.Mani         86  72   0  25  183
R.Daniel       44  55  66  77  242

Ranked List
V.S.Rao        77  89  56  69  291
A.Gupta        66  78  98  45  287
R.Daniel       44  55  66  77  242
S.Laxmi        45  67  38  55  205
S.Mani         86  72   0  25  183
```

**图 13.15** *班级学生排名表的生成*

### 2. 库存更新 [LO 13.2, 13.6 M]

商店中库存物品的价格和数量每天都在变化。它们可能增加或减少。图 13.16 中的程序读取价格和数量的增量值，并计算库存物品的总价值。

该程序演示了将结构体指针用作函数参数。结构体 **item** 的地址 **&item** 被传递给函数 **update()** 和 **mul()**。接收 **&item** 值的形式参数 **product** 和 **stock** 被声明为 **struct stores** 类型的指针。

### 程序

```c
struct stores
{
    char name[20];
    float price;
    int quantity;
};
main()
{
    void update(struct stores *, float, int);
```

```text
Price       : 35.750000
Quantity    : 24

Value of the item = 858.000000
```

**图 13.16** *将结构体指针用作函数参数。*

## 复习题

### 填空题

- 1. 指针变量作为其值包含另一个变量的 ______。(LO 13.1)
- 2. ______ 运算符返回其操作数所指向变量的值。(LO 13.2)
- 3. ______ 运算符与指针一起使用，以解引用指针中包含的地址。(LO 13.2)
- 4. 声明为 ______ 的指针不能被解引用。(LO 13.1)
- 5. 唯一可以赋给指针变量的整数是 ______。(LO 13.4)

### 判断题

- 1. 指针常量是内存位置的地址。(LO 13.1)
- 2. 指针变量的基础类型是 void。(LO 13.1)
- 3. 指针变量使用地址运算符声明。(LO 13.2)
- 4. 可以将指向 float 的指针强制转换为指向整数的指针。(LO 13.2)
- 5. 指向指针的指针是一个术语，用于描述其内容是另一个指针地址的指针。(LO 13.3)
- 6. 不能用一个指针减去另一个指针。(LO 13.4)
- 7. 可以将一个整数加到一个指针上。(LO 13.4)
- 8. 指针不能用作函数定义头中的形式参数。(LO 13.6)
- 9. 当数组作为参数传递给函数时，传递的是指针。(LO 13.6)
- 10. 函数中局部变量的值可以被另一个函数改变。(LO 13.6)

### 选择题

- 1. C 语言中的指针是 (LO 13.1)
  - (a) 某个位置的地址
  - (b) 可用于描述链表
  - (c) 可用于访问数组元素
  - (d) 以上所有。

### 难度等级

低；中；高

