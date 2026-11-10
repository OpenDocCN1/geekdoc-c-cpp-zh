

### 程序 14.13a：student_management.c（main 之前的部分与 main 部分）

```c
add_student(stud);
average = display_marks(stud);
printf("Average marks of class = %.2f\n", average);
fputs("\nEnter Roll No: ", stdout);
scanf("%d", &roll_no);
q = search_student(stud, roll_no);
if (q != NULL)
    printf("%-20s %4d %5hd %5hd %5hd %6hd\n", q->name, q->roll_no,
    q->marks[0], q->marks[1], q->marks[2], q->marks[3]);
else
    fputs("Not found", stdout);
return 0;
}
```

### 程序 14.13b：student_management.c（函数定义）

```c
void add_student(STUDENT p[])
{
    short i = 0;
    do {
        fputs("Name: ", stdout);
        if (scanf("%[^\n]", p->name) != 1)
            break;
        fputs("Roll No: ", stdout);
        scanf("%d", &p->roll_no);
        fputs("Marks in 3 subjects: ", stdout);
        scanf("%hd%hd%hd", &p->marks[0], &p->marks[1], &p->marks[2]);
        p->marks[3] = p->marks[0] + p->marks[1] + p->marks[2];
        FLUSH_BUFFER
        p++;                           /* Moves pointer to next element */
    } while (i++ < COLUMNS - 1);       /* Won't accept more than 50 records */
    return;
}

float display_marks(STUDENT p[])
{
    short i; int total_marks = 0;
    fputs("Name           Roll No Phys Chem Maths Total\n", stdout);
    for (i = 0; i < COLUMNS; i++, p++) {
        if (p->roll_no > 0) {
            printf("%-20s %4d %5hd %5hd %5hd %6hd\n", p->name, p->roll_no,
            p->marks[0], p->marks[1], p->marks[2], p->marks[3]);
            total_marks += p->marks[3];
        }
        else
            break;
    }
    return (float) total_marks / i;   /* Returns average of total marks */
}
```

```c
STUDENT *search_student(STUDENT p[], int f_roll_no)
{
    short i;
    for (i = 0; i < COLUMNS; i++, p++)
        if (p->roll_no == f_roll_no)
            return p;
    return NULL;
}
```

### 程序输出：student_management.c

```text
Name: Sohini Gupta
Roll No: 1111
Marks in 3 subjects: 70 85 90
Name: Shiksha Agarwal
Roll No: 2222
Marks in 3 subjects: 55 75 60
Name: Juhi Parekh
Roll No: 3333
Marks in 3 subjects: 95 90 98
Name: [Enter]
```

| 姓名 | 学号 | 物理 | 化学 | 数学 | 总分 |
|---|---:|---:|---:|---:|---:|
| Sohini Gupta | 1111 | 70 | 85 | 90 | 245 |
| Shiksha Agarwal | 2222 | 55 | 75 | 60 | 190 |
| Juhi Parekh | 3333 | 95 | 90 | 98 | 283 |

```text
Average marks of class = 239.33

Enter Roll No: 2222
Shiksha Agarwal     2222    55    75     60    190
```

**main 之前的部分与 main 部分** 数组 stud 首先通过将第一个元素设置为零来初始化。（仅使用 {""} 设置该元素的第一个成员就足够了。）程序现在可以通过检查 roll_no 字段来评估已使用数组元素的数量。随后依次调用三个函数（接下来讨论）。

**函数定义** 三个函数都使用参数 STUDENT p[] 表示结构体数组。然而，p 实际上是指向 main 中定义的数组 stud 起始位置的指针。这些函数使用 p 来遍历数组；每次执行 p++ 都会将指针推进到下一个数组元素。

**add_student** 函数在 **do-while** 循环中两次调用 **scanf** 来接收用户数据。由于 **scanf** 返回成功读取的项数，因此在未输入数据的情况下按 [Enter] 会终止该循环。否则，该循环将在输入 50 条记录后终止。**add_student** 还会将 marks 数组的第四个元素设置为前三个元素之和。

**display_marks** 函数使用 for 循环显示每条记录。尽管该循环最多可以迭代 50 次，但当 roll_no 不再为正整数时，它会提前终止。该函数还会返回班级的平均成绩。**search_student** 函数搜索学号，如果找到该学号，则返回指向匹配数组元素的指针。

## 14.11 联合体

当使用某人的 id 搜索数据库时，你肯定经常也希望按姓名搜索。如果这两个属性保存在一个联合体中，就可以做到这一点；联合体是一种在形式上类似于结构体的数据类型。联合体包含两个或更多共享同一内存的成员，任一时刻只有最近被赋值的成员是活动的。考虑以下联合体的声明和定义：

```c
union uemp {
    short emp_id;
    char name[30];
} u;
```

声明 uemp 类型的联合体  
定义 uemp 类型的联合体变量 u

联合体的声明、定义和访问方式与结构体完全相同。前面的语句声明了一个名为 uemp 的双成员联合体，并同时定义了联合体变量 u。成员通过 u.emp_id 和 u.name 访问。然而，两个成员共享同一块内存区域，任一时刻只能正确访问一个成员——即最后被赋值的那个成员。例如，可以按以下方式赋值并访问 emp_id：

```c
u.emp_id = 1234;
printf("%hd:\n", u.emp_id);
```

输出 1234

如果随后给 u.name 赋值，一切都会按预期工作：

```c
strcpy(u.name, "George Martin");
printf("%s:\n", u.name);
```

输出 George Martin

然而，u.name 会覆盖 u.emp_id 先前使用的内存段，所以现在无法访问后者（尽管编译器不会报错）：

```c
printf("%hd:\n", u.emp_id);
```

输出未定义

除了这一本质区别外，联合体的处理方式与结构体类似。可以将联合体的定义与其声明分开，typedef 对联合体的作用方式完全相同。可以创建指向联合体的指针，也可以创建联合体数组。由于这些相似性，联合体在作为结构体成员使用，或自身以结构体作为成员时最为有用。

> **要点：** 联合体的成员不能同时访问，因为它们共享同一块内存区域。只能正确访问最后被赋值的那个成员。

### 14.11.1 联合体的独特属性

除了结构体和联合体使用计算机内存的方式不同之外，联合体还有一些独有的特性。需要牢记以下特性：

- *联合体的所有成员不能同时初始化。* 这一点很明显，因为任一时刻只能正确访问一个成员。只能初始化第一个成员：

    ```c
    union uemp u2 = {1234};
    ```

    仅初始化 emp_id

- 联合体的大小由在内存中占用空间最大的成员的大小决定。对于 uemp，这个大小是 30，即 name 字段的大小。与结构体一样，与字边界对齐（14.3）相关的问题可能会增大这个数值。

- 当访问的不是最后被赋值的成员时，编译器不会输出错误。程序员必须跟踪任一时刻处于活动状态的成员。

- 可以使用联合体给一个成员赋值，再通过另一个成员将其读回。例如，可以将字符串存储在 char 数组中，然后通过读取联合体的 int 成员来检查其位模式。

联合体可以轻松判断一台机器是小端序还是大端序。在大端序机器中，最高有效位最先存储；而对于小端序机器则相反。不过，联合体主要用作节省内存的对象。

> 提示：通常有必要包含一个成员，用于保存当前存储在联合体中的信息类型。该值可以是 0、1、2 等，程序可以用它来确定当前活动的成员。

### 14.11.2 intro2unions：入门程序

程序 14.14 基于 ucust 模板定义了两个联合体变量 u1 和 u2。u1 未初始化，而 u2 使用单个值初始化，该值会自动赋给第一个成员（aadhar_id）。其余两个成员稍后赋值。请注意，在给 u2.name 赋值后，u2.aadhar_id 和 u2.cust_id 将求出不正确的值。

```c
/* intro2unions.c: Demonstrates basic features of unions. */
#include <stdio.h>
#include <string.h>

int main(void)
{
    union ucust {                         /* Declares union of type ucust */
        int aadhar_id;                    /* Only one of these three members ... */
        short cust_id;                    /* ... is active at any time. But ... */
        char name[30];                    /* ... this one determines size of u1. */
    } u1;                                 /* Defines union variable of type ucust */

    printf("Size of u1 is %d\n", sizeof(u1));

    union ucust u2 = {1234567890};        /* Initializes a second variable */
    printf("u2.aadhar_id = %d\n", u2.aadhar_id);

    u2.cust_id = 3456;
    printf("u2.cust_id = %d\n", u2.cust_id);
    strcpy(u2.name, "Paul McCartney");
```

